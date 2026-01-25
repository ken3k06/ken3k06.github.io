---
layout: post
category: crypto
title: Basic Concepts in Algebraic Geometry
---
* This will become a table of contents (this text will be scrapped).
{:toc}

## Vành đa thức
Ta sẽ quy ước giả thiết các vành đang xét sau này đều là các vành giao hoán có đơn vị. 

Cho $A$ là vành và $x$ là biến số. Ta gọi một biểu thức $f$ có dạng $c_0+c_1x+...+c_rx^r$ với $c_i\in A$ là đa thức của biến $x$ với hệ số trong $A$. Hệ số cao nhất $c_r \neq 0$ và $r$ được gọi là bậc của đa thức. 

Vành đa thức $A[x]$ của biến $x$ trên $A$ là tập hợp tất cả các đa thức trong đó phép cộng và phép nhân được thực hiện như thông thường. Một đa thức chuẩn hay đa thức monic là đa thức có hệ số cao nhất bằng 1. 

**Bổ đề 1.** Cho $g\in A[x]$ là đa thức monic. Ta có thể viết mọi đa thức $f\in A[x]$ dưới dạng $f=gh+v$ với $\deg v <\deg g$. 

Vành đa thức $n$ biến trên $A$ được định nghĩa bằng quy nạp như sau:

<center>$A[x_1,...,x_n]:=A[x_1,...,x_{n-1}][x_n]$</center>

Có nghĩa là $A[x_1,...,x_n]$ là vành đa thức của biến $x_n$ trên vành $A[x_1,...,x_{n-1}]$.

Ta quy ước $A[X]=A[x_1,...,x_n]$.

Các phần tử của $A[X]$được gọi là đa thức $n$ biến. Vành $A[X]$ không phụ thuộc vào thứ tự các biến vì mọi đa thức $n$ biến đều có dạng (sau này ta cần quan tâm tới thứ tự của chúng thông qua khái niệm gọi là thứ tự từ điển):



<center>$\displaystyle f(X)=\sum_{r_1+...+r_n \leq r} c_{r_1,...,r_n} x_1^{r_1}\dots x_n^{r_n}$</center>


Với $r$ là một số tự nhiên và $c_{r_1,...,r_n}\in A$ là các hệ số.

Bậc của mỗi đơn thức  $x_1^{r_1}\dots x_n^{r_n}$ là tổng các số mũ $r_1+...+r_n$. Bậc của $f$ là bậc lớn nhất trong số các bậc của đơn thức tạo thành $f$. 

Khi viết một đa thức nhiều biến người ta thường viết theo một thứ tự nào đó của đơn thức (chưa cần quan tâm).

**Định nghĩa.** Vành $A$ được gọi là miền nguyên nếu như $A$ không có ước của 0 có nghĩa là $cd \neq 0$ với mọi $c, \ d\neq 0 \in A$.

**Bổ đề 1.** Nếu $A$ là miền nguyên thì $\deg fg = \deg f + \deg g$. 


**Bổ đề 2.** Nếu $A$ là miền nguyên thì $A[X]$ là miền nguyên và các phần tử khả nghịch của $A[X]$ là các phần tử khả nghịch của $A$

Đối tượng nghiên cứu chính của môn hình học đại số là tập nghiệm của các hệ phương trình đa thức. Ta gọi các tập này là “tập đại số affine” hay ngắn gọn là “tập đại số”

Ta kí hiệu tập nghiệm của đa thức $f$ là $Z(f)$. Tương tự, tập nghiệm của hệ đa thức $S$ là $Z(S)$ và được hiểu như sau:

<center>$\displaystyle Z( S) =\bigcap _{f\in S} Z( f)$</center>


## Idean

Nhắc lại: tập đại số được gọi là tập nghiệm của một hệ đa thức. Hai hệ đa thức được gọi là tương đương nhau nếu chúng có cùng tập nghiệm. Idean cung cấp cho ta một công cụ để thay đổi hệ đa thức ban đầu thành một hệ đa thức tương đương nhưng có cấu trúc tốt hơn.

Cho $A$ là vành và tập $I$ trong $A$ được gọi là Idean nếu $0 \in I$ và $I$ thỏa mãn các điều kiện:

- Nếu $f,g\in I$ thì $f+g \in I$ 
- $hf \in I$ với mọi $f \in I, h \in A$. 

Như vậy idean là tập đóng đối với phép cộng và phép nhân với một phần tử của vành. 

Song song với idean ta cũng có khái niệm module như sau: 

Cho $A$ là vành. Tập $M$ được gọi là $A$-module hay module trên $A$ nếu $M$ là nhóm abel được trang bị phép nhân với các phần tử của $A$ với các phần tử của $M$ sao cho với mọi $u,v \in M, f,g\in A$ thì ta có

<center>
$f(u+v)=fu +fv$ 
</center>
<center>
$(fg)u = f(gu)$
</center>
<center>
$1u = u$ 
</center>

Ta sẽ đi sâu về khái niệm này trong các phần sau. 

Khái niệm idean mở rộng tính chia hết trong số học. Thật vậy, tập các phần tử chia hết cho một phần tử $f$ trong $A$ là tập: 

<center>
$(f):= \lbrace hf \mid h \in A \rbrace$
</center>

$(f)$ ở đây là một idean. Tổng quát hơn, với mọi hệ phần tử $S$ trong $A$ ta có thể coi tập sau đây là tập các phần tử chia hết cho $S$: 

<center>
$
(S):=\lbrace h_1f_1+...+h_rf_r \mid h_i \in A, f_j \in S, r \geq 1  \rbrace
$
</center>

Nhận xét: $(S)$ là idean nhỏ nhất chứa $S$. Tiếp theo ta định nghĩa tổng và tích của các idean. 

Cho $I$ và $J$ là hai idean tùy ý trong $A$. Idean sinh bởi các phần tử của $I$ và $J$ được gọi là tổng của $I$ và $J$ và kí hiệu là $I+J$. Tương tự, idean sinh bởi các phần tử của tích $fg$ với mọi $f \in I$ và $g \in J$ được gọi là tích của $I$ và $J$ và kí hiệu là $IJ$.

## Idean căn 
Cho $V$ là một tập điểm tùy ý trong $\mathbb{A}^n$. Kí hiệu 
<center>
$
I_V:= \lbrace f \in k[X] \mid \ f(a) = 0  , \forall a \in V\rbrace
$
</center>
Về ý nghĩa hình thức: $I_V$ là tập các đa thức nhận các điểm trong tập điểm $V$ làm nghiệm.
Có thể thấy ngay $I_V$ là idean và là idean lớn nhất có tập nghiệm chứa $V$. Ta gọi $I_V$ là idean của tập điểm $V$ trong $k[X]$. Nếu $V$ chỉ gồm một điểm $a$ thì ta dùng kí hiệu $I_a$. 

Ví dụ: $I_a = (x_1-\alpha_1,x_2-\alpha_2,...,x_n-\alpha_n)$ với mọi điểm $a=(\alpha_1,\alpha_2,...,\alpha_n)$. 
Thật vậy, dùng liên tiếp thuật toán Euclid thì ta có thể viết mọi đa thức $f \in k[X]$ dưới dạng:

<center>
$
f = h_1(x_1-\alpha_1)+...+h_n(x_n-\alpha_n) + \alpha
$
</center>

với $\alpha \in k$ thì $f(a)=0$ khi và chỉ khi $\alpha = 0$
Một ví dụ khác: Xét $V \subset \mathbb{A}^2$ là một tập vô hạn các điểm trên đường cong $x^3-y^2=0$ thì $I_V= (x^3-y^2)$. Ta chỉ cần chứng minh $I_V \subseteq (x^3-y^2)$. 
Coi mọi đa thức $f \in k[x,y]$ như là đa thức của biến $y$ với hệ số trong $k[x]$. Dùng thuật toán Euclid ta có thể viết: 

<center>
$f = h(x^3-y^2)+uy+v$
</center>


với $u,v \in k[x]$. Do $V\subset V(x^3-y^2)=\lbrace(\alpha^2,\alpha^3)  \mid \alpha \in k\rbrace$  nên nếu $f \in I_V$ thì $f(\alpha^2, \alpha^3)=u(\alpha^2)\alpha^3+v(\alpha^2)$ với mọi $\alpha$ thuộc vào một tập vô hạn trong $k$. Từ đây suy ra $u(x^2)x^3+v(x^2) = 0$. Do đa thức $u(x^2)x^3$ chỉ chứa các đơn thức bậc lẻ và đa thức $v(x^2)$ chỉ chứa các đơn thức bậc chẵn, nên ta phải có $u(x^2)x^3=0$ và $v(x^2)=0$. Từ đây suy ra $u=0$ và $v=0$. Do đó có điều phải chứng minh. 

Cho $V$ và $W$ là hai tập điểm tùy ý trong $\mathbb{A}^n$. Dễ thấy rằng $I_V \supseteq I_W$ nếu $V \subseteq W$ và 

<center>
$
I_V \cap I_W = I_{V \cup W}
$
</center>

Ta biết rằng giao của các tập đại số chứa $V$ cũng là tập đại số. Đây là tập đại số nhỏ nhất chứa $V$, kí hiệu là $\overline{V}$. Ta gọi $\overline{V}$ là bao đóng của $V$. 
**Bổ đề.** Cho $W$ là một tập tùy ý trong $\mathbb{A}^n$. Ta có
a/ $\overline{W} = V(I_W)$
b/ $I_{\overline{W}} = I_W$

Nếu $J$ là tập đại số thì $\overline{J}=J$ và do đó $J=V(I_J)$. 
Tóm lại ta có hai mối quan hệ $J\rightarrow V(J)$ và $J \rightarrow I_J$ giữa các idean trong $k[X]$ và tập điểm trong $k^n$. Hai mối quan hệ này cho ta một mối tương ứng 1-1 giữa các tập đại số và các idean dạng $I_J$. 

<center>
$
J \rightarrow I_J \rightarrow V(I_J)=J 
$
</center>
Bây giờ ta sẽ chuyển hướng nghiên cứu sang các idean dạng $I_V$. Đầu tiên ta có định nghĩa về idean căn. 

**Định nghĩa.** Cho $I$ là một idean tùy ý trong vành $A$. Ta gọi tập tất cả các phần tử $f \in A$ có một lũy thừa $f^r \in I$ là căn của $I$, kí hiệu là $\sqrt{I}$ (radical ideal)

Ta sẽ chứng minh $\sqrt{I}$ là một idean.
Để chứng minh nó là idean thì nó cần đảm bảo hai tính chất. Một là với mỗi $f,g \in \sqrt{I}$ thì ta phải có $f+g\in \sqrt{I}$ và $hf \in \sqrt{I}$ với mỗi $h \in A$. 

Đầu tiên, với $f,g\in \sqrt{I}$ thì tồn tại $r,s$ sao cho $f^r,g^s\in I$. Khi đó 
<center>
$
\displaystyle (f+g)^{r+s} = \sum_{i=1}^{r+s}\binom{r+s}{i}f^{r+s-i}g^i
$
</center>
Rõ ràng $r+s-i\geq r$  hoặc $i \geq s$ cho nên $f^{r+s-i}g^i$ chia hết cho $f^r$ hay $g^s$ với mọi $i$. Suy ra $(f+g)^{r+s}\in I$ cho nên $f+g\in \sqrt{I}$ . Còn $hf \in \sqrt{I}$ làm tương tự.

**Bổ đề.** $I_V$ là idean căn.
Chứng minh: Nếu $f^r\in I_V$ thì $f^r(a)=0$ với mọi $a\in V$. Suy ra $f(a)=0$ với mọi $a\in V$ và do đó $f\in I_V$.  (một đa thức bậc hữu hạn thì không thể có vô hạn nghiệm).

**Lưu ý:** Không phải idean căn nào trong $k[X]$ cũng là idean của một tập đại số. Giả sử $k[X]$ chứa một idean $I \neq k[X]$ vô nghiệm. Khi đó $\sqrt{I}$ cũng vô nghiệm. Nếu $\sqrt{I}=I_V$ là idean của một tập đại số $V$ nào đó thì ta phải có $V =\emptyset$ .  Suy ra $I_V=I_\emptyset=k[X]$ tức là  $1\in I$ và suy ra $I = k[X]$ là mâu thuẫn. 

Cho $I$ là idean thực sự của vành $A$. Ta gọi $I$ là một idean cực đại nếu $I$ không nằm trong một idean thực sự nào khác của $A$. 
Với mọi chuỗi tăng các idean thực sự $I_1 \subseteq I_2 \subseteq I_2 \subseteq... \subseteq I_j \subseteq ...$ ta thấy $\bigcup I_j$ cũng là một idean thực sự. Vì vậy ta có thể áp dụng bổ đề Zorn để thấy mọi idean thực sự đều nằm trong ít nhất một idean cực đại.

Ví dụ: $I_a = (x_1-\alpha_1,...,x_n-\alpha_n)$ là idean cực đại trong $k[X]$. 
Từ nhận xét ở trên thì ta biết được rằng $f = \sum_{i=1}^{n} h_i(x_i-\alpha_i)+\alpha$ với $\alpha \in k$ cho nên $\alpha \in (I_a,f)$ và nếu $f \notin I_a$ thì $\alpha \neq 0$ và do đó $(I_a,f) = k[X]$


Note: 
$(I,f)$ là idean sinh bởi $I$ và $f$ tức là tập các đa thức dạng $g+hf$ với $g \in I$ và $h\in R$ ). 
