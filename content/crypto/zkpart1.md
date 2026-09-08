+++
date = '2026-08-17'
title = 'Intro to ZKP - Part 1 : Basic Concepts'
draft = true 
toc = true
math = true 
+++


## Zero-Knowledge Proofs 


Imagine you are at a convenience store trying to buy a beer. The cashier asks you for your identity card to verify that you are over 18. While this is a standard procedure in many countries, it is actually somewhat uncomfortable. By handing over your ID, you are not just proving your age but also exposing your exact date of birth, your address, ...

So we want to develop a way to prove that someone is over 18 without revealing any other information about their birthday. 

For example, you can show the cashier a picture that you took in 2008, which is 18 years ago. By looking at the picture we know that you are 18+ without knowing your exact date of birth or any private information. 

In fact, this is how Zero-Knowledge Proof (ZKP) deals with the problem of proving a statement.


Formally, ZKPs are two-party cryptographic primitive that allows a $\text{Prover}$ to prove a statement about a secret to a $\text{Verifier}$ without revealing any information about the secret, except for the statement we want to prove. 

For convenience, we will denote a prover by $\mathcal{P}$ and a verifier by $\mathcal{V}$ 

A ZKP need to satisfy three properties: 

1. **Completeness**: A correct proof will convince the verifier that the statement is true. 
2. **Soundness**: If the prover is dishonest, they can not create a proof for a false statement (that convinces the verifier).
3. **Zero-Knowledge**: The verifier learns nothing about the secret other than the fact that the statement is true or false.

To understand ZKPs better, we first need to understand what a commitment scheme is. A commitment scheme is a two-step protocol in which one party commits to a chosen value while keeping it secret from others and later reveals, or opens the value. The other parties can verify whether the value corresponds to the commitment. Every commitment scheme needs to satisfy two properties:

1. **Hiding**: The commitment should not reveal any information about the committed value. 
2. **Binding**: Once the commitment is made, it should be computationally infeasible for the committer to change the value they committed to.



For example, when you play a rock-paper-scissors game with a friend, to ensure that neither player can cheat, you can use a simple commitment scheme like this: First, you pick your choice, it is either rock , paper or scisssors. Then you choose a random value $r$ and compute the commitment $C = H(\text{choice} || r)$, where $H$ is a cryptographically secure hash function. Later when your friend wants to see your choice, you reveal both your choice and the random value $r$. Your friend can compute the hash value once again to verify that it matches your commitment. Since $H$ is a one-way function, it satisfies the hiding property. Also $H$ is collision-resistant, so it satisfies the binding property.


Lastly, we can classify ZKPs into two main categories: interactive and non-interactive. In an interactive ZKP, the prover and verifier have to communicate in rounds to complete the proof. While in a Non-interactive ZKP (NIZK), the prover can generate a proof that can be verified by the verifier without any interaction.




## Sigma protocol

Next, we will have a look at sigma protocols, which are a special type of interactive ZKP. Sigma protocols are a class of three-move interactive proof systems where a prover $\mathcal{P}$ convinces a verifier $\mathcal{V}$ that they know a secret witness without revealing the witness itself. The sigma symbol $\Sigma$ illustrates the three moves of the protocols: Commitment, Challenge, and Response

A well-known Sigma protocol is the Schnorr protocol, which is used to prove knowledge of a discrete logarithm. The protocol works as follows: 

Let $\mathbb{G}$ be a cyclic group of prime order $q$ with generator $g$. The prover $\mathcal{P}$ has a secret $s \in \mathbb{Z}_q$ and wants to prove to the verifier $\mathcal{V}$ that they know $s$ such that $t = g^s$ without revealing $s$.

The prover picks a random value $y$ from $\mathbb{Z}_q$ and computes the commitment $w = g^y$. The prover sends $w$ to the verifier.

The verifier picks a random challenge $c$, send it to $\mathcal{P}$, and after that $\mathcal{P}$ computes the response $z = y+cs$ and sends it to $\mathcal{V}$. $\mathcal{V}$ can verify the proof by checking if $g^z = w \cdot t ^c = g^y \cdot g^{sc}$

$$
\begin{equation*}
\begin{array}{ c c c }
\mathcal{P} (g,s) &  & \mathcal{V} (g,t)\\
\hline
\text{pick } y\xleftarrow{R}\mathbb{Z}_{q} ,\ \ w\leftarrow g^{y} & \xrightarrow{\ \ w\ \ } & \\
 & \xleftarrow{\ \ c\ \ } & \text{pick challenge } c\xleftarrow{R}\mathbb{Z}_{q}\\
z\leftarrow y+cs & \xrightarrow{\ \ z\ \ } & g^{z}\stackrel{?}{=} w\cdot t^{c}
\end{array}
\end{equation*}
$$

Now we will see how the Schnorr protocol satisfies the three properties of ZKPs.

**Completeness**. Completeness ensures that an honest verifier always accept an honest prover. This is true for the Schnorr protocol by substituting the values of $(w,c,z)$ into the equation $g^z = w \cdot t^c$:

**Zero-Knowledge**. Goldwasser, Micali, and Rackoff have found a way to formalize this property of proof systems. A proof systems achieves ZKs if there exists a simulator that produces transcripts indistinguishable from real ones, without knowing the witness and security holds when the verifier follows the protocol honestly.s

This can be done by constructing a simulator that generates a transcript $(w,c,z)$ as follows: Given $(g,t,c)$, we sample $z$ at random and then compute $\displaystyle w = \frac{g^z}{t^c}$. This notion of ZK is known as special honest-verifier zero-knowledge, as it assumes that the challenge $c$ is sampled honestly from a uniformly random distribution. Because $\mathcal{V}$ does not know anything about the witness $s$, it cannot distinguish between a transcript generated by the simulator and a real transcript generated by an honest prover.

**Special-Soundness**. Given two accepting transcripts $(w,c_1,z_1)$ and $(w,c_2,z_2)$ with the same commitment $w$ but different challenges, we can extract the witness $s$. In real life, this can be understand that if someone know about the secret, then there must be way to extract that secret from her/him. In proof systems, we show that if a Prover can convince a Verifier  then there exists an algorithm, called Extractor, that can extract the witness from the Prover. In our case, the extractor can compute the witness $s$ as follows: 

$$
\begin{gather*}
\ \left( w=g^{y} ,c_{1} ,z_{1} =y+c_{1} s\right) ,\left( w=g^{y} ,c_{2} ,z_{2} =y+c_{2} s\right)\\
\Longrightarrow ( c_{1} -c_{2}) s=z_{1} -z_{2}\\
\Longrightarrow s=\frac{z_{1} -z_{2}}{c_{1} -c_{2}}
\end{gather*}
$$

## Fiat-Shamir Heuristic

The Fiat-Shamir transformation is a heuristic method to convert $\Sigma$-protocols into non-interactive zero-knowledge proofs. It proceeds as follows: to prove the membership of an instance $\displaystyle s$ to a language $\displaystyle \mathcal{L}$, $\displaystyle \mathcal{P}$ first computes the commitment and denotes it by $\displaystyle w$. Then the prover set $\displaystyle c\leftarrow \text{RO}( s,w)$ where $\displaystyle \text{RO}$ is some hash function modeled by a random oracle and computes the last round using $\displaystyle c$ as the challenge. 

We will take a look at the Schnorr protocol and see how we can apply the Fiat-Shamir transformation to it.


Given the public parameters $t=g^{s}$, $\mathcal{P}$ computes $w=g^{y}$, where $y$ is a random number. Then, $\mathcal{P}$ computes $c=\text{RO} (g,t,w)$ and uses $c$ as the challenge by setting $z=y+c\cdot s$. Finally, $\mathcal{P}$ outputs a proof $\pi =(w,z)$ and sends it to $\mathcal{V}$.Any $\mathcal{V}$ can verify the proof by computing $c=\text{RO} (g,t,w)$, since $t$ and $g$ are public parameters and $w$ was sent by $\mathcal{P}$. Then, $\mathcal{V}$ checks whether $g^{z} =t^{c} \cdot w$.

So why do we even need the Fiat-Shamir transformation? Because we need to reduce the communication complexity of the protocol. For example, in some real life system, the Verifier can not be online all the time to generate the challenge. But in Fiat-Shamir transformation, the challenge is generated independently by the Prover and can be verified later by the Verfier. 



