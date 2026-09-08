+++
date = '2026-08-09'
title = 'China MO 2017'
toc = true
math = true 
+++

*Bài toán.* Hai dãy $\displaystyle \{u_{n}\}$ và $\displaystyle \{v_{n}\}$ gồm các số nguyên được định nghĩa bởi $\displaystyle u_{0} =u_{1} =1,u_{n} =2u_{n-1} -3u_{n-2} ,\forall n\geqslant 2$ và $\displaystyle v_{0} =a,v_{1} =b,v_{2} =c$ và $\displaystyle v_{n} =v_{n-1} -3v_{n-2} +27v_{n-3} ,\forall n\geqslant 3$. Biết rằng tồn tại một số nguyên dương $\displaystyle N$ đủ lớn để với mọi $\displaystyle n\geqslant N$ thì $\displaystyle u_{n} |v_{n}$. Chứng minh rằng $\displaystyle 3a=2b+c$.



*Lời giải.*

Xét phương trình đặt trưng của dãy $\displaystyle u_{n}$ là $\displaystyle x^{2} -2x+3=0$ ta tìm được hai nghiệm là $\displaystyle 1+\sqrt{-2}$ và $\displaystyle 1-\sqrt{-2}$. Từ đây ta tính được công thức tổng quát của $\displaystyle u_{n}$ sẽ là 

$$
\begin{equation*}
u_{n} =\frac{\sqrt{3}^{n}\left( e^{in\theta } +e^{-in\theta }\right)}{2}
\end{equation*}
$$

trong đó $\displaystyle \theta $ là góc sao cho $\displaystyle \cos \theta =\frac{1}{\sqrt{3}} ,\sin \theta =\frac{\sqrt{2}}{\sqrt{3}}$. Tương tự ta tính được công thức tổng quát của $\displaystyle v_{n}$ sẽ là 

$$
\begin{equation*}
v_{n} =3^{n}\left( Ae^{2in\theta } +Be^{-2in\theta } +C\right)
\end{equation*}
$$

Từ giả thiết của bài toán thì $\displaystyle u_{n} |v_{n}$ với mỗi $\displaystyle n\geqslant N$ cho nên dãy $\displaystyle v_{n}$ sẽ gồm các số nguyên kể từ một lúc nào đó trở đi. Mặt khác ta xét dãy 

$$
\begin{gather*}
l_{n} =\frac{v_{n}}{u_{n}} =2\sqrt{3}^{n}\left(\frac{Ae^{2in\theta } +Be^{-2in\theta } +C}{e^{in\theta } +e^{-in\theta }}\right)\\
=2\sqrt{3}^{n}\left(\frac{Ae^{in\theta }\left( e^{in\theta } +e^{-in\theta }\right) +Be^{-in\theta }\left( e^{in\theta } +e^{-in\theta }\right) +C-A-B}{e^{in\theta } +e^{-in\theta }}\right)\\
=2\sqrt{3}^{n}\left( Ae^{in\theta } +Be^{-in\theta } +\frac{C-A-B}{e^{in\theta } +e^{-in\theta }}\right)\\
=2\left( A\left(\sqrt{3} e^{i\theta }\right)^{n} +B\left(\sqrt{3} e^{-i\theta }\right)^{n} +\frac{2( C-A-B) 3^{n}}{u_{n}}\right)
\end{gather*}
$$


Đặt $\displaystyle A'=3^{N} .Ae^{2iN\theta } ,B'=3^{N} .Be^{-2iN\theta }$ và $\displaystyle C'=3^{N} C$ thì dãy mới 

$$
\begin{equation*}
v'_{n} =3^{n}\left( A'e^{2in\theta } +B'e^{-2in\theta } +C'\right)
\end{equation*}
$$


sẽ gồm các số hạng đều là số nguyên theo nhận xét trên. Bằng tính toán trực tiếp với $\displaystyle v'_{0} ,v'_{1} ,v'_{2}$ là các số nguyên thì ta có 

$$
\begin{gather*}
A'+B'+C'=a'\in \mathbb{Z}\\
-( A'+B') +( B'-A') 2i\sqrt{2} +3C'=b'\in \mathbb{Z}\\
-7( A'+B') +( B'-A') 4i\sqrt{2} +9C'=c'\in \mathbb{Z}
\end{gather*}
$$

Suy ra $\displaystyle -2( A+B) +( B'-A') 4i\sqrt{2} +6C'=2b'\in \mathbb{Z}$ hay $\displaystyle -5( A'+B') +6C'=c'-2b'\in \mathbb{Z}$ và đồng thời $\displaystyle -5( A'+B') -5C'=-5a'\in \mathbb{Z}$ cho nên suy ra $\displaystyle 11C'=c'-2b'+5a'\in \mathbb{Z}$ cho nên $\displaystyle C'\in \mathbb{Q}$. Điều này dẫn tới $\displaystyle A'+B'\in \mathbb{Q}$.

Đồng thời 

$$
\begin{gather*}
( B'-A')\left( i\left( 14\sqrt{2} -4\sqrt{2}\right)\right) =7b'-c'-11C'\\
\Longrightarrow B'-A'=\frac{7b'-c'-11C'}{-14\sqrt{2} +4\sqrt{2}} i\in \mathbb{C}
\end{gather*}
$$


Suy ra ta có $\displaystyle A',B'$ là hai số phức liên hợp với nhau

Ta có một nhận xét như sau : Xét vành giao hoán $\displaystyle \mathbb{Q}\left(\sqrt{-2}\right) =\left\{a+b\sqrt{-2} |a,b\in \mathbb{Q}\right\}$ là một vành đóng đối với phép cộng và nhân cho nên từ hệ 

$$
\begin{gather*}
A'+B'+C'=a'\in \mathbb{Z}\\
-2( A'+B') +( B'-A') 2i\sqrt{2} +3C'=b'\in \mathbb{Z}\\
-7( A'+B') +( B'-A') 4i\sqrt{2} +9C'=c'\in \mathbb{Z}
\end{gather*}
$$


ta cũng suy ra được $\displaystyle A',B',C'\in \mathbb{Q}\left(\sqrt{-2}\right)$ và xét ngược lại từ cách xác định $\displaystyle A',B'$ ta cũng có $\displaystyle A,B\in \mathbb{Q}\left(\sqrt{-2}\right)$ và $\displaystyle A,B$ cũng là hai số phức liên hợp với nhau. Bây giờ ta có 

$$
\begin{equation*}
v_{n} =2\left( A\left(\sqrt{3} e^{i\theta }\right)^{n} +B\left(\sqrt{3} e^{-i\theta }\right)^{n} +\frac{2( C-A-B) 3^{n}}{u_{n}}\right)
\end{equation*}
$$

Không mất tính tổng quát ta có thể đặt $\displaystyle A=a+b\sqrt{-2}$ và $\displaystyle B=a-b\sqrt{2}$ còn $\displaystyle \left(\sqrt{3} e^{i\theta }\right)^{n} =c+d\sqrt{-2} ,\left(\sqrt{3} e^{-i\theta }\right)^{n} =c-d\sqrt{-2}$ 

trong đó $\displaystyle a,b$ là các số hữu tỉ còn $\displaystyle c,d$ là các số nguyên theo cách xác định trên. Do đó tồn tại $\displaystyle k$ nguyên dương để mà $\displaystyle ka,kb$ đều là các số nguyên. Ta có thể xét

$$
\begin{equation*}
\ v_{n} k=2\left( Ak\left(\sqrt{3} e^{i\theta }\right)^{n} +Bk\left(\sqrt{3} e^{-i\theta }\right)^{n} +k\frac{2( C-A-B) 3^{n}}{u_{n}}\right)
\end{equation*}
$$


Bây giờ đặt $\displaystyle a'=ka,b'=kb$ thì đưa về xét tổng 

$$
\begin{gather*}
\left( a'+b'\sqrt{-2}\right)\left( c+d\sqrt{-2}\right) +\left( a'-b'\sqrt{2}\right)\left( c-d\sqrt{-2}\right)\\
=a'c+a'd\sqrt{-2} +b'c\sqrt{-2} -2b'd+a'c-a'd\sqrt{-2} -b'c\sqrt{-2} +2b'd\\
=2a'c\in \mathbb{Z}
\end{gather*}
$$

tương tự với trường hợp $\displaystyle A=a-b\sqrt{-2} ,B=a+b\sqrt{-2}$. Do đó cụm $\displaystyle 2\left( Ak\left(\sqrt{3} e^{i\theta }\right)^{n} +Bk\left(\sqrt{3} e^{-i\theta }\right)^{n}\right) \in \mathbb{Z}$ và để $\displaystyle l_{n} \in \mathbb{Z}$ thì ta cần 

$$
\begin{equation*}
\frac{2k( C-A-B) 3^{n}}{u_{n}} \in \mathbb{Z}
\end{equation*}
$$

Xét $\displaystyle u_{n} \equiv -u_{n-1}(\bmod 3)$ và từ $\displaystyle u_{0} =u_{1} =1$ nên ta suy ra $\displaystyle ( u_{n} ,3) =1$. Cho nên điều kiện viết lại thành
$$ 
\begin{equation*}
u_{n} |2k( C-A-B)
\end{equation*}
$$

Nhưng $\displaystyle u_{n} =\sqrt{3}^{n}\cos( n\theta )$ từ công thức tổng quát nên suy ra $\displaystyle \lim u_{n} =+\infty $ kéo theo $\displaystyle C-A-B=0$ hay $\displaystyle C=A+B$. Thay ngược lại $\displaystyle v_{n}$ ta có 

$$
\begin{gather*}
v_{0} =a=2( A+B)\\
v_{1} =b=\left( 2+2\sqrt{-2}\right) A+\left( 2-2\sqrt{-2}\right) B\\
v_{2} =c=\left( 2-4\sqrt{-2}\right) A+\left( 2+4\sqrt{-2}\right) B\\
\Longrightarrow 3a=2b+c
\end{gather*}
$$

Vậy ta có điều phải chứng minh. 
