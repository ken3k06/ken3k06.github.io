+++
date = '2026-07-20'
title = 'Về định lý không điểm tổ hợp'
toc = true
math = true 
+++

Trước khi đi sâu vào chứng minh định lí không điểm tổ hợp và ứng dụng của nó thì ta cần trang bị một số kiến thức về đa thức. 

## Đa thức


Cho $\displaystyle \mathbb{K}$ là một vành giao hoán bất kì. Ta kí hiệu $\displaystyle \mathbb{K}[ x]$ là một vành các đa thức 1 biến $\displaystyle x$ với hệ số là các phần tử của $\displaystyle \mathbb{K}$. Ngoài đa thức $\displaystyle 0$ ra thì các đa thức này đều có dạng 

$$
\begin{equation*}
a=a_{n} x^{n} +...+a_{0}
\end{equation*}
$$

trong đó $\displaystyle a_{n} \neq 0$ và $\displaystyle \deg a=n$. Trường hợp $\displaystyle a=0$ thì ta đặt $\displaystyle \deg a=-\infty $. 

Nếu $\displaystyle \mathbb{K}$ là một miền nguyên thì vành đa thức $\displaystyle \mathbb{K}[ x]$ cũng là một miền nguyên. 



Tiếp theo ta chỉ ra rằng có thể thực hiện chia có dư với hai đa thức có hệ số trên trường $\displaystyle \mathbb{K}$. Và từ đây đến cuối bài viết ta sẽ xét $\displaystyle \mathbb{K}$ là một trường. 

Xét hai đa thức ${\displaystyle A(x),B(x)\in \mathbb{K} [x],B(x)\neq 0}$.



Ta chứng minh tồn tại duy nhất một cặp đa thức ${\displaystyle (Q(x),R(x))\in \mathbb{K} [x]\times }\mathbb{K}[ x]$ mà ${\displaystyle \deg (R)< \deg (B)}$ sao cho 

$$
\begin{equation*}
A(x)=Q(x)B(x)+R(x)
\end{equation*}
$$

Nếu ${\displaystyle R(x)=0}$ thì ta sẽ nói rằng ${\displaystyle A(x)}$ chia hết cho ${\displaystyle B(x)}$ hay ${\displaystyle B(x)}$ là ước của ${\displaystyle A(x)}$. Ta sẽ quy nạp theo ${\displaystyle \deg (A)}$



Nếu ${\displaystyle \deg (A)< \deg (B)}$, ta chọn ${\displaystyle Q(x)=0}$ và ${\displaystyle R(x)=A(x)}$ thỏa mãn đẳng thức trên.

Ngược lại, xét ${\displaystyle a,b}$ lần lượt là hệ số cao nhất của ${\displaystyle A(x)}$ và ${\displaystyle B(x)}$. Ta chọn được ${\displaystyle c\in \mathbb{K}}$ sao cho ${\displaystyle a=cb}$. 

Tiếp theo lấy ${\displaystyle d=\deg (A)-\deg (B)}$ và ${\displaystyle A'(x)=A(x)-cx^{d} B(x)}$ thì lúc này hệ số bậc ${\displaystyle \deg (A)}$ của ${\displaystyle A'(x)}$ sẽ là 0 cho nên ${\displaystyle \deg (A')< \deg (A)}$. Theo quy nạp, tồn tại ${\displaystyle Q',R'}$ trên $\mathbb{{\displaystyle K}}$ và ${\displaystyle \deg R'< \deg B}$ thỏa mãn 

$$
\begin{equation*}
A'(x)=Q'(x)B(x)+R'(x)
\end{equation*}
$$

Khi đó ta có 
$$
\begin{gather*}
A(x)=A'(x)+cx^{d} B(x)=Q'(x)B(x)+R'(x)+cx^{d} B(x)\\
=\left( Q'(x)+cx^{d}\right) B(x)+R'(x)
\end{gather*}
$$

và thu được một cặp đa thức thỏa mãn các yêu cầu. 

Ta sẽ chứng minh cặp đa thức này là duy nhất. Thật vậy, giả sử tồn tại ${\displaystyle A(x),B(x)}$ sao cho tồn tại 2 cặp đa thức ${\displaystyle (Q_{1} (x),R_{1} (x)),(Q_{2} (x),R_{2} (x))}$ thỏa mãn 

$$
\begin{gather*}
A(x)=Q_{1} (x)B(x)+R_{1} (x)=Q_{2} (x)B(x)+R_{2} (x)\\
\Longrightarrow (Q_{1} (x)-Q_{2} (x))B(x)+(R_{1} (x)-R_{2} (x))=0
\end{gather*}
$$


Nếu ${\displaystyle Q_{1} (x)\neq Q_{2} (x)}$ thì ta có ${\displaystyle \deg (R_{1} (x)-R_{2} (x))< \deg (B)}$ trong khi đó ${\displaystyle \deg (Q_{1} (x)-Q_{2} (x))B(x)\geqslant \deg (B)}$

Như vậy ${\displaystyle \deg (VT) >\deg (B)}$ trong khi ${\displaystyle \deg (0)=−\infty }$ là điều vô lí. 

Vậy không thể xảy ra trường hợp trên. 

Ta có điều phải chứng minh. 



**Hệ quả 1.** Với mọi đa thức $\displaystyle B\in \mathbb{K}[ x]$ có bậc dương, khi đó vành thương $\displaystyle \mathbb{K}[ x] /\langle B\rangle $ là một không gian vector trên trường $\displaystyle \mathbb{K}$ có số chiều hữu hạn đúng bằng bậc của $\displaystyle B$.

*Chứng minh.*

Từ nhận xét ở trên ta có với mỗi $\displaystyle A\in \mathbb{K}[ x]$ thì tồn tại $\displaystyle Q,R$ sao cho $\displaystyle A=BQ+R$ với $\displaystyle \deg( R) < \deg( B)$ cho nên các đơn thức $\displaystyle 1,x,...,x^{\deg( B) -1}$ là một cơ sở của không gian vector $\displaystyle \mathbb{K}[ x] /\langle B\rangle $.



**Hệ quả 2.** Vành $\displaystyle \mathbb{K}[ x]$ các đa thức một biến $\displaystyle x$ với các hệ số trong trường $\displaystyle \mathbb{K}$ là một vành chính. Có nghĩa là mọi ideal của nó đều được sinh ra bởi một phần tử. Hơn nữa, mọi ideal khác 0 của $\displaystyle \mathbb{K}[ x]$ đều được sinh bởi duy nhất một đa thức monic.



*Chứng minh.*

Cho $\displaystyle I$ là một ideal của $\displaystyle \mathbb{K}[ x]$. Nhắc lại tính chất của ideal thì $\displaystyle I$ là mộtt ập con của $\displaystyle \mathbb{K}[ x]$ thỏa mãn với mọi $\displaystyle a,b\in I$ và $\displaystyle m,n\in \mathbb{K}[ x]$, ta có $\displaystyle am+bn\in I$. Chọn $\displaystyle d$ là đa thức có bậc nhỏ nhất trong $\displaystyle d$. Khi đó với mỗi $\displaystyle a\in I$ ta có $\displaystyle a=dq+r$. Do $\displaystyle a\in I$ và $\displaystyle dq\in I$ cho nên $\displaystyle r=a-dq\in I$. Mà bậc của $\displaystyle r$ nhỏ hơn bậc của $\displaystyle d$ cho nên điều này chỉ có thể xảy ra khi $\displaystyle r=0$ hay $\displaystyle a=dq$. Như vậy $\displaystyle d$ là phần tử sinh của $\displaystyle I$ và $\displaystyle I$ là ideal chính. Nếu $\displaystyle d=d_{n} x^{n} +...+d_{0}$ với $\displaystyle d_{n} \neq 0$ thì $\displaystyle d_{n}^{-1} d$ là phần tử sinh duy nhất của $\displaystyle I$ và là monic. 






## Định lí Chevalley-Warning

Cho $\displaystyle p$ là số nguyên tố. Xét $\displaystyle \mathbb{K} =\mathbb{F}_{p}$ và $\displaystyle P\in \mathbb{F}_{p}[ x]$ là một đa thức với hệ số trên $\displaystyle \mathbb{F}_{p}$ thì ta gọi $\displaystyle P_{0}$ là dạng rút gọn của $\displaystyle P$ nếu 


- Đa thức $\displaystyle P_{0}$ là một đa thức có bậc nhỏ hơn hoặc bằng $\displaystyle p-1$
- Với mọi $\displaystyle \alpha \in \mathbb{F}_{p}$ ta luôn có $\displaystyle P_{0}( \alpha ) =P( \alpha )$


Theo định lí Fermat nhỏ thì ta có $\displaystyle \alpha ^{p} =\alpha \ (\bmod p)$ cho nên bằng cách thay $\displaystyle x^{p}$ thành $\displaystyle x$ trong $\displaystyle P$ ta có được $\displaystyle P_{0}$. Nói cách khác với $\displaystyle I$ là Ideal của $\displaystyle \mathbb{F}_{p}[ x]$ sinh bởi đa thức $\displaystyle x^{p} -x$ thì với mọi $\displaystyle P\in I$ và với mọi $\displaystyle \alpha \in \mathbb{F}_{p}$ ta có $\displaystyle P( \alpha ) =0$. Như vậy với mọi đa thức $\displaystyle P\in \mathbb{F}_{p}[ x]$, ta có đa thức rút gọn $\displaystyle P_{0}$ của nó chính là phần dư Euclid trong phép chia của $\displaystyle P$ cho $\displaystyle x^{p} -x$. 



**Định lí 1.** Cho $\displaystyle P,Q\in \mathbb{F}_{p}[ x]$ là hai đa thức một biến $\displaystyle x$. Khi đó $\displaystyle P\equiv Q\ \bmod x^{p} -x$ khi và chỉ khi $\displaystyle P( \alpha ) =Q( \alpha )$ với mọi $\displaystyle \alpha \in \mathbb{F}_{p}$. 


Bây giờ ta sẽ mở rộng ra trường hợp nhiều biến như sau: Cho $\displaystyle P\in \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ là một đa thức $\displaystyle n$ biến với hệ số trong $\displaystyle \mathbb{F}_{p}$. Đa thức $\displaystyle P_{0} \in \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ được gọi là dạng rút gọn của $\displaystyle P$ nếu như 

- $\displaystyle \deg_{x_{i}} P_{0} \leqslant p-1$ với mọi $\displaystyle x_{i}$. Tức là bậc của $\displaystyle P_{0}$ theo $\displaystyle x_{i}$ không vượt quá $\displaystyle p-1$
- Với mọi $\displaystyle ( x_{1} ,...,x_{n}) \in \mathbb{F}_{p}^{n}$ ta có $\displaystyle P_{0}( x_{1} ,...,x_{n}) =P( x_{1} ,...,x_{n})$


**Định lí 2.** Cho hai đa thức $\displaystyle P,Q\in \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ nhận cùng giá trị trên tập $\displaystyle \mathbb{F}_{p}^{n}$ khi và chỉ khi 
$$
\begin{equation*}
P\equiv Q\ \bmod \ \langle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n} \rangle 
\end{equation*}
$$

với $\displaystyle \langle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n} \rangle $ là ideal của vành $\displaystyle \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ sinh bởi các đa thức $\displaystyle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n}$. Hơn nữa, mỗi đa thức $\displaystyle P\in \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ tồn tại duy nhất $\displaystyle P_{0}$ thỏa mãn $\displaystyle \deg_{x_{i}} P_{0} \leqslant p-1$ với mọi $\displaystyle x_{1} ,...,x_{n}$.

*Chứng minh.*

Các đa thức $\displaystyle x_{i}^{p} -x_{i}$ triệt tiêu trên $\displaystyle \mathbb{F}_{p}^{n}$ cho nên các phần tử của ideal mà chúng sinh ra cũng có tính chất đấy. 

Từ đó suy ra rằng nếu $\displaystyle P\equiv Q\ \bmod \ \langle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n} \rangle $ thì ta có $\displaystyle P( \alpha ) =Q( \alpha )$ với mọi $\displaystyle \alpha \in \mathbb{F}_{p}^{n}$. 

Ta sẽ chứng minh chiều ngược lại. 


Bây giờ với đa thức $\displaystyle f\in \mathbb{F}_{p}[ x_{1} ,x_{2} ,...,x_{n}]$ ta coi nó như là một đa thức theo biến $\displaystyle x_{1}$ với các hệ số trong $\displaystyle \mathbb{F}_{p}[ x_{2} ,...,x_{n}]$. Ta thực hiện phép chia Euclid cho $\displaystyle f$ với đa thức $\displaystyle x_{1}^{p} -x_{1}$ thì được một đa thức dư \ $\displaystyle f_{1} \in \mathbb{F}_{p}[ x_{2} ,...,x_{n}]$ thỏa mãn $\displaystyle \deg_{x_{1}} f_{1} \leqslant p-1$. Tức là $\displaystyle f=g_{1}\left( x_{1}^{p} -x_{1}\right) +f_{1}$. Giả sử ở bước thứ $\displaystyle i$ ta thu được đa thức $\displaystyle f_{i} \in \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ thỏa mãn $\displaystyle \deg_{x_{j}} \leqslant p-1$ với mọi $\displaystyle 1\leqslant j< i$. Khi đó ta xem $\displaystyle f_{i}$ như đa thức biến $\displaystyle x_{i+1}$ rồi thực hiện chia tiếp cho $\displaystyle x_{i+1}^{p} -x_{i+1}$. Kết quả của phép chia sẽ là phần dư $\displaystyle f_{i+1}$ thỏa mãn tính chất $\displaystyle \deg_{x_{j}} f_{i+1} \leqslant p-1$ với $\displaystyle 1\leqslant j\leqslant i+1$. Lặp lại các bước như trên ta thu được đa thức $\displaystyle f_{n} \in \mathbb{F}_{p}[ x_{1} ,...,x_{n}]$ thỏa mãn $\displaystyle \deg_{x_{i}} f_{n} \leqslant p-1$ với mọi $\displaystyle i=1,...,n$. Hơn nữa từ cách xây dựng của $\displaystyle f_{n}$ ta có 

$$
\begin{equation*}
f\equiv f_{n} \ \bmod \ \langle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n} \rangle 
\end{equation*}
$$

Tiếp theo ta cần bổ đề sau đây:

**Bổ đề.** Cho $\displaystyle P\in \mathbb{K}[ x_{1} ,...,x_{n}]$ là đa thức với $\displaystyle n$ biến $\displaystyle x_{1} ,...,x_{n}$ và hệ số trong một trường $\displaystyle \mathbb{K}$. Gọi $\displaystyle d_{i}$ là bậc của $\displaystyle P$ như đa thức với biến $\displaystyle x_{i}$ và với hệ số là đa thức của các biến còn lại. Giả sử với mọi $\displaystyle i$, tồn tại tập con $\displaystyle S_{i} \subset \mathbb{K}$ với $\displaystyle d_{i} +1$ phần tử sao cho $\displaystyle P( \alpha _{1} ,...,\alpha _{n}) =0$ với mọi $\displaystyle ( \alpha _{1} ,...,\alpha _{n}) \in S_{1} \times ...\times S_{n}$. Khi đó ta có $\displaystyle P=0$. 



Bổ đề có thể được xem như một mở rộng cho tính chất về nghiệm của đa thức một biến $\displaystyle f( x)$: Một đa thức $\displaystyle f( x)$ có bậc là $\displaystyle d$ thì có không quá $\displaystyle d$ nghiệm. 

Chứng minh. 

Ta chứng minh bằng quy nạp theo $\displaystyle n$. 

Viết lại $\displaystyle P$ dưới dạng đa thức một biến $\displaystyle x_{n}$ với các hệ số là những đa thức của các biến còn lại

$$
\begin{equation*}
P=Q_{d_{n}} x^{d_{n}} +Q_{d_{n-1}} x^{d_{n-1}} +...+Q_{0}
\end{equation*}
$$

với $\displaystyle Q_{d_{i}} \in \mathbb{K}[ x_{1} ,...,x_{n-1}]$.

$\displaystyle P$ là đa thức một biến, có bậc không vượt quá $\displaystyle d_{n}$ và hơn nữa với mọi $\displaystyle ( \alpha _{1} ,...,\alpha _{n-1})$ thì ta có $\displaystyle d_{n} +1$ giá trị của $\displaystyle x$ sao cho $\displaystyle P( \alpha _{1} ,...,\alpha _{n-1} ,x) =0$. Tức là $\displaystyle P$ có ít nhất $\displaystyle d_{n} +1$ nghiệm trong khi bậc của nó không lớn hơn $\displaystyle d_{n}$ cho nên các hệ số của nó là $\displaystyle Q_{d_{i}}( \alpha _{1} ,...,\alpha _{n-1}) \in \mathbb{K}$ đều bằng không với mọi $\displaystyle ( \alpha _{1} ,...,\alpha _{n-1})$. Đến đấy ta có thể áp dụng giả thiết quy nạp vào các đa thức này và có điều phải chứng minh. 



Quay trở lại bài toán, ta áp dụng cách xây dựng $\displaystyle f_{n}$ tương tự cho đa thức $\displaystyle P-Q$ thì được 

$$
\begin{equation*}
P-Q\equiv G_{n}( x) :=( P-Q)_{n}( x) \ \bmod \langle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n} \rangle 
\end{equation*}
$$


Ở đây giả sử $\displaystyle P( \alpha ) =Q( \alpha )$ và áp dụng bổ đề cho $\displaystyle G_{n}( x)$ với $\displaystyle d_{i} =p-1\ và\ S_{i} =\mathbb{F}_{p}$ thì ta có $\displaystyle G_{n}( x) =0$. Vậy $\displaystyle P\equiv Q\ \bmod \langle x_{1}^{p} -x_{1} ,...,x_{n}^{p} -x_{n} \rangle $.



Giả sử $\displaystyle P$ có hai dạng rút gọn là $\displaystyle P_{0} ,P_{0}^{'}$ thì $\displaystyle \left( P_{0} -P_{0}^{'}\right)( \alpha ) =0$ và $\displaystyle \deg\left( P_{0} -P_{0}^{'}\right) \leqslant p-1$. Một lần nữa áp dụng bổ đề ta có $\displaystyle P_{0} =P_{0}^{'}$ và hoàn tất chứng minh. 