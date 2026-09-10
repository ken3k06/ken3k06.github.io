+++
date = '2026-09-08T15:55:04+07:00'
title = 'Game theory and Cryptography - Part 2'
toc = true
math = true 
+++
Trong bài này ta sẽ bàn về các trò chơi có thông tin đầy đủ. Nhắc lại từ bài trước thì trò chơi có thông tin đầy đủ (**complete information game**) là dạng trò chơi mà tại đó các thông tin về số người chơi, tập hợp các hành động của mỗi người chơi và hàm thu hoạch của mỗi người chơi ứng với các chiến lược của trò chơi được công khai. Các người chơi sẽ đồng thời thực hiện hành động mà mình chọn và không ai biết người kia chọn gì cho tới khi có kết quả. 




## Trò chơi có chiến lược chuẩn

Trò chơi có chiến lược chuẩn được xem là dạng đơn giản nhất của trò chơi, trong đó các hành động của các người chơi có tác động qua lại để dành thu hoạch tốt nhất. Trò chơi diễn ra với các hành động được tiến hành đồng thời hay là các hành động tuần tự của các bên, mà người chơi này ra quyết định thì người kia không biết. 

Để xác định một trò chơi có chiến lược chuẩn, ta quan tâm đến các yếu tố như: 
- Tập hợp các người chơi tham gia
- Tập hợp các hành động của tất cả các bên trong cuộc chơi
- Các trạng thái quyết định được mô tả
- Cuối cùng là hàm thu hoạch ứng với mỗi người chơi xác định trên tập hợp các chiến lược của tất cả các bên
bên


### Các yếu tố cơ bản
Để bắt đầu một trò chơi, số người chơi ít nhất phải là 2 người. Thông thường, mỗi người chơi được kí hiệu bởi các chữ cái $A,B,C,...$ hay các số $I,II,III,...$

Để chỉ tập hợp các quyết định của người chơi, ta sẽ dùng các tập hợp $A_1,...,A_n$ trong đó $A_i$ là tập hợp các quyết định ứng với người chơi thứ $i$. 

Lúc này, không gian tích $A=A_1 \times A_2 \times ... \times A_n$ là không gian mô tả tập tất cả các chiến lược được thi hành giữa các người chơi. 

$$
A = \prod^n_{i=1}A_i=\{(a_1,...,a_n) | a_i \in A_i, i=1,...,n\}
$$

Bộ $(a_1,...,a_n)$ là một bộ trong tập hợp các bộ các chiến lược của tất cả các người chơi, trong đó $a_i$ chỉ quyết định của người chơi thứ $i$. 

Hàm thu hoạch dùng để đánh giá hiệu quả của người chơi thông qua quyết định được chọn ứng với các bộ chiến lược của tất cả các người chơi. 

Như vậy, với trò chơi có $n$ người tham gia thì sẽ có $n$ hàm thu hoạch. Mỗi hàm có dạng 

$$
U_i : A \to \mathbb{R}, i = 1,...,n
$$

Ta có định nghĩa cụ thể như sau

**Định nghĩa.** Ta gọi một trò chơi có chiến lược chuẩn (normal form game) là một trò chơi hội tụ đủ các yếu tố sau đây 

i) Có tập hợp số người chơi $n \geq 2$ 
ii) Có tập hợp các quyết định $A_i$ ứng với người chơi thứ $i$, $i=1,...,n$

iii) Có hàm thu hoạch $U_i : A \to \mathbb{R}$ cho mỗi người chơi $i=1,...,n$

Trong đó các hàm thu hoạch $U_i: A \to \mathbb{R}$ cho mỗi người chơi $i=1,...,n$ đều có cùng miền xác định là không gian các chiến lược $A=A_1 \times A_2 \times ... \times A_n$ 

Hàm thu hoạch ở đây mang ý nghĩa như sau 
- Đầu tiên, hàm thu hoạch cho ta biết giá trị của hành động mà người chơi đã thực hiện so với các hành động khác của họ và so với những người chơi khác. Nó thể hiện cho ta biết rằng, hiệu quả của việc chọn một hành động của người chơi không chỉ phụ thuộc vào chính người chơi mà còn phụ thuộc vào tất cả các người chơi còn lại đối với một chiến lược

- Giả sử bây giờ ta có hai bộ chiến lược $(a_1,a_2,...,a_n)$ và $(\overline{a_1},\overline{a_2},...,\overline{a_n})$, ta có bất đẳng thức liên quan tới người chơi thứ $i$: 

$$
U_i(a_1,...,a_n) < U_i(\overline{a_1},...,\overline{a_n})
$$

Bất đẳng thức trên cho ta biết sự hiệu quả của chiến lược này so với chiến lược kia đối với người chơi thứ $i$. 


- Tương tự, với cùng một bộ chiến lược $(a_1,...,a_n)$, các người chơi có thể so sánh hiệu quả cách chơi với nhau. Chẳng hạn ta có thể đánh giá 

$$
U_i(a_1,...,a_n) < U_j(a_1,...,a_n)
$$

thì bất đẳng thức trên cho ta biết chiến lược đang xem xét đối với người chơi $j$ là tốt hơn người chơi $i$ theo một nghĩa nào đó. 

## Trò chơi ma trận

Trò chơi ma trận là thuật ngữ được dùng để chỉ các trò chơi có ma trận thu hoạch ở dạng đơn ma trận. Ở bài trước, ta có nhắc đến trò chơi tung đồng xu. $A$ và $B$ cùng chơi một trò chơi đặt đồng xu, nếu hai đồng xu cùng mặt thì $A$ được 1 điểm, $B$ mất 1 điểm và ngược lại. 

$$\displaystyle \begin{array}{ c c|c|c }
 &  & B & \\
 &  & S & N\\
\hline
A & S & ( 1,-1) & ( -1,1)\\
\hline
 & N & ( -1,1) & ( 1,-1)
\end{array}$$


Ta nhận thấy rằng tổng thu hoạch của hai người chơi bao giờ cũng bằng 0. Ứng với thu hoạch dương của người này là thu hoạch âm của người kia và ngược lại. Như vậy, chỉ với đơn ma trận cũng đủ để ta mô tả về trò chơi này, bằng cách quy ước thu hoạch trên ma trận luôn được tính cho người $A$.

$$
\begin{array}{ c|c|c }
 & S & N\\
\hline
S & 1 & -1\\
\hline
N & -1 & 1
\end{array}
$$

Tổng quát hơn, với trò chơi có hai người chơi $I$ và $II$. Người chơi thứ $I$ có $m$ hành động và người chơi thứ $II$ có $n$ hành động. Nếu người thứ $I$ chọn hành động thứ $i$ và người thứ $II$ chọn hành động thứ $j$ thì điểm thưởng cho người thứ $I$ được kí hiệu là $a_{ij}$. Tương tự, thu hoạch này cũng được xem là điểm phạt cho người thứ $II$. 


Ma trận thu hoạch lúc này sẽ có dạng 

$$
\begin{equation*}
A=\begin{bmatrix}
a_{11} & a_{12} & \dotsc  & a_{1n}\\
a_{21} & a_{22} & \dotsc  & a_{2n}\\
\vdots  & \vdots  & \vdots  & \vdots \\
a_{m1} & a_{m2} & \dotsc  & a_{mn}
\end{bmatrix}
\end{equation*}
$$

## Phương án tối ưu trên ma trận

Bây giờ ta sẽ phân tích phương án tối ưu trên ma trận.

Một phương án tối ưu sẽ là phương án như thế nào? Đối với người chơi $I$, khi chọn hành động thứ $i$ thì sẽ nhận được một mức thưởng $a_{ij}$ bất kì với $j=1,...,n$, trong đó $j$ sẽ phụ thuộc vào hành động của người chơi $II$. Như vậy cho dù $II$ chọn giá trị $j$ nào thì $I$ cũng sẽ nhận được lượng điểm thưởng không nhỏ hơn $\min_{1 \leq j \leq n}a_{ij}$ 

Ta muốn tối ưu cho $I$ thì cần chọn $i$ sao cho đại lượng trên là lớn nhất. Tức là chọn $i$ sao cho điểm thuởng phạt nhận được không thấp hơn giá trị sau đây:

$$
\max_{1 \leq i \leq m} \min_{1 \leq j \leq n} a_{ij}
$$

Đây được gọi là giải thuật Max-Min

Chi tiết như sau: 

**Giải thuật Max-Min**

B1: Trên mỗi dòng của ma trận thu hoạch, chọn ra phần tử bé nhất
B2: Duyệt qua tất cả các phần tử đã chọn và chọn phần tử lớn nhất


Tương tự ta cũng sẽ có giải thuật Min-Max


Người chơi $II$ cũng sẽ làm tương tự, cố gắng đạt được điểm phạt thấp nhất có thể. Như vậy, nếu người chơi $II$ chọn hành động $j$ thì điểm phạt tối đa mà họ có thể nhận được là 

$$
\max_{1 \leq i \leq m}a_{ij}
$$

Người chơi $II$ mong muốn đạt được điểm phạt thấp nhất cho nên họ sẽ chọn $j$ sao cho giá trị trên đạt thấp nhất (duyệt qua các cột thay vì các dòng như ở Max-Min). Tức là ngừoi chơi $II$ sẽ chọn $j$ sao cho điểm phạt không vượt quá giá trị 

$$
\min_{1\leq j \leq n} \max_{1\leq i \leq m} a_{ij}
$$

Giải thuật Min-Max lúc này sẽ như sau

**Giải thuật Min-Max**

B1: Trên mỗi cột của ma trận thu hoạch, chọn ra phần tử lớn nhất
B2: Duyệt qua tất cả các phần tử vừa chọn để chọn ra phần tử bé nhất

Một câu hỏi tự nhiên được đặt ra là hai đại lượng này được sắp xếp với nhau như thế nào. Điều này dẫn đến định lý sau đây

**Định lí Minimax (Maximin)** Với trò chơi ma trận được cho bởi ma trận $A$ như trên , ta luôn có 

$$
\max_{1 \leq i \leq m} \min_{1 \leq j \leq n} a_{ij} \leq \min_{1 \leq j \leq n} \max_{1 \leq i \leq m} a_{ij}
$$

*Chứng minh.*

Với mỗi $i=1,...,m$ ta luôn có 

$$
\min_{1 \leq j \leq n} a_{ij} \leq a_{ij}
$$

Vậy 

$$
\max_{1 \leq i \leq m} \min_{1 \leq j \leq n} a_{ij} \leq a_{ij}
$$

Với mỗi $j=1,...,n$ ta lại có 

$$
a_{ij} \leq \max_{1 \leq i \leq m} a_{ij}
$$

Cho nên 

$$
a_{ij} \leq \min_{1 \leq j \leq n} \max_{1 \leq i \leq m}a_{ij}
$$


Kết hợp 2 vế ta có điều phải chứng minh. 



$$
\max_{1 \leq i \leq m} \min_{1 \leq j \leq n} a_{ij} \leq \min_{1 \leq j \leq n} \max_{1 \leq i \leq m} a_{ij}
$$

## Điểm yên ngựa và giá trị của trò chơi ma trận

Trong trường hợp dấu bằng ở bất đẳng thức trên xảy ra, tức là ma trận của trò chơi có giá trị tại các điểm Maximin và Minimax bằng nhau, ta gọi giá trị bằng nhau đó là $v$. Lúc này 


$$
\max_{1 \leq i \leq m} \min_{1 \leq j \leq n} a_{ij} =v=\min_{1 \leq j \leq n} \max_{1 \leq i \leq m} a_{ij}
$$

Xét cụ thể từng phần ta có:

$$
\max_{1 \leq i \leq m} \min_{1 \leq j \leq n} a_{ij} = \max_{1 \leq i \leq m}( \min_{1 \leq j \leq n} a_{ij})=v
$$

Cho nên phải tồn tại một chỉ số $i'$ sao cho $\min_{1\leq j \leq n} a_{i'j}=v$
Tương tự 

$$
\min_{1 \leq j \leq n} \max_{1 \leq i \leq m} a_{ij} = \min_{1 \leq j \leq n} (\max_{1 \leq i \leq m} a_{ij}) = v
$$
cho nên tồn tại chỉ số $j'$ để $\max_{1\leq i \leq m}a_{ij'}=v$

Suy ra 

$$
\min_{1\leq j \leq n} a_{i'j}=v=\max_{1\leq i \leq m}a_{ij'}
$$


Mặt khác ta luôn có 

$$
\begin{equation*}
a_{i'j'} \leqslant \max_{1\leqslant i\leqslant m} a_{ij'} ,\ \min_{1\leqslant j\leqslant n} a_{i'j} \leqslant a_{i'j'}
\end{equation*}
$$

mà $\displaystyle \max_{1\leqslant i\leqslant m} a_{ij'} =\min_{1\leqslant j\leqslant n} a_{i'j}$ cho nên 

$$
\begin{equation*}
\begin{cases}
a_{i'j'} \leqslant \min_{1\leqslant j\leqslant n} a_{i'j}\\
\max_{1\leqslant i\leqslant m} a_{ij'} \leqslant a_{i'j'}
\end{cases}
\end{equation*}
$$

Cặp chỉ số $\displaystyle ( i',j')$ lúc này thỏa mãn 

$$
\begin{equation*}
a_{ij'} \leqslant a_{i'j'} \leqslant a_{i'j} ,\forall i=1,2,...,m;\forall j=1,2,...,n
\end{equation*}
$$


Điểm $(i',j')$ được gọi là điểm yên ngựa của trò chơi ma trận và thu hoạch $a_{i'j'}$ được gọi là giá trị của trò chơi ma trận. 

**Mệnh đề.** Ma trận của trò chơi có giá trị Minimax và Maximin trùng nhau khi và chỉ khi ma trận đó có điểm yên ngựa

Để tìm điểm yên ngựa, ta có thể dùng thuật toán Min-Max hoạc Max-Min. Ta có thể tìm, tại đó điểm có giá trị là nhỏ nhất trên dòng nhưng lại là lớn nhất trên cột. 

## Giải trò chơi có chiến lược chuẩn

