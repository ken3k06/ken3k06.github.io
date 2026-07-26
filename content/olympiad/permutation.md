+++
date = '2026-07-20'
title = 'Một số bài toán về hoán vị'
toc = true
math = true 
+++


## Tính chất cơ bản

Ở đây, ta sẽ trình bày một góc nhìn sơ cấp về hoán vị. 

Cho tập hợp $X$, một hoán vị của $X$ có thể hiểu là một song ánh từ $X$ vào chính nó. Tập hợp tất cả các hoán vị của $X$ cùng với phép toán hợp thành hàm $\circ$ tạo thành một nhóm.


Cụ thể hơn, ta coi hoán vị $(a_1,a_2,...,a_n)$ là một song ánh $\sigma : [n] \to [n]$ cho bởi $\sigma(i)=a_i$ trong đó $[n]=\{1,2,...,n\}$.

Để thuận tiện cho việc tính toán hợp thành của hai ánh xạ, ta sẽ kí hiệu hoán vị như sau: 

$$
\begin{equation*}
\sigma =\begin{pmatrix}
1 & 2 & \dotsc  & n\\
\sigma ( 1) & \sigma ( 2) & \dotsc  & \sigma ( n)
\end{pmatrix}
\end{equation*}
$$

Gọi $\displaystyle S_{n}$ là tập tất cả các song ánh trên $\displaystyle [ n]$ thì khi đó $\displaystyle \sigma \in S_{n}$ được gọi là một phép thế bậc $\displaystyle n$ và hơn nữa, cấp của nhóm này sẽ là $\displaystyle n!$

Khi coi hoán vị như song ánh thì ta có thể phân tích hoán vị như hợp thành của các hoán vị đơn giản hơn. Một dạng phân tích hoán vị là phân tích thành các xích. Cụ thể ta có định nghĩa của xích như sau: 

**Định nghĩa.** Giả sử $\displaystyle i_{1} ,i_{2} ,...,i_{k}( k >1)$ là những phần tử khác nhau của $\displaystyle [ n]$. Kí hiệu $\displaystyle ( i_{1} i_{2} \dotsc i_{k})$ là một phép thế bậc $\displaystyle n$ sao cho $\displaystyle i_{1}\rightarrow i_{2} ,i_{2}\rightarrow i_{3} ,...,i_{k}\rightarrow i_{1}$ và các phần tử còn lại của $\displaystyle [ n]$ biến thành chính nó. Khi đó ta nói rằng $\displaystyle ( i_{1} i_{2} \dotsc i_{k})$ là một vòng xích cấp $\displaystyle k$. Một vòng xích cấp 2 được gọi là một chuyển vị. Hai vòng xích 

$$
\begin{equation*}
\sigma =( i_{1} i_{2} \dotsc i_{k}) ,\ \tau =( j_{1} j_{2} \dotsc j_{r})
\end{equation*}
$$

được gọi là độc lập nếu $\displaystyle \{i_{1} ,i_{2} ,...,i_{k}\} \cap \{j_{1} ,j_{2} ,...,j_{r}\} =\emptyset$. Phép thế đồng nhất được coi là một vòng xích cấp 1 và kí hiệu là $\displaystyle id$. 

Để phân tích hoán vị thành các xích ta xét một đồ thị có $n$ đỉnh, đánh số từ $1$ đến $n$. Ta vẽ cạnh có hướng đi từ đỉnh $i$ đến $\sigma(i)$. Từ tính chất song ánh của $\sigma$ thì ta suy ra tại mỗi đỉnh có đúng 1 cạnh đi vào và 1 cạnh đi ra. Do đó đồ thị nhận được có dạng hợp thành của các chu trình rời nhau. 

Ví dụ: 

$$
\begin{equation*}
\sigma =\begin{pmatrix}
1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10\\
8 & 6 & 5 & 9 & 3 & 10 & 4 & 7 & 1 & 2
\end{pmatrix}
\end{equation*}
$$

Bắt đầu từ $\displaystyle 1\rightarrow \sigma ( 1) =8$, sau đó ta lại xét $\displaystyle \sigma ( 8) =7,\sigma ( 7) =4,\sigma ( 4) =9,\sigma ( 9) =1$. Như vậy chu trình sẽ là $\displaystyle 1\rightarrow 8\rightarrow 7\rightarrow 4\rightarrow 9\rightarrow 1$. Tiếp tục ta xét $\displaystyle 2\rightarrow \sigma ( 2) =6\rightarrow \sigma ( 6) =10\rightarrow \sigma ( 10) =2$ và có một chu trình khác $\displaystyle 2\rightarrow 6\rightarrow 10$. Tương tự $\displaystyle 3\rightarrow 5$ và ta viết lại $\displaystyle \sigma =( 1\ 8\ 7\ 4\ 9)( 2\ 6\ 10)( 3\ 5)$

![image](https://hackmd.io/_uploads/SkQqKC-EMe.png)


Có thể dùng SymmetricGroup trong Sagemath để tính toán:

```python
G = SymmetricGroup(10)
g = G([8,6,5,9,3,10,4,7,1,2])
g.cycles()
# [(1,8,7,4,9),(2,6,10),(3,5)]
```
Hoặc bằng Python:

```python
def get_disjoint_cycles(arr):
    n = len(arr)
    visited = [False] * (n+1)
    cycles = []
    for i in range(1,n+1):
        if not visited[i]:
            cycle = []
            curr = i 
            while not visited[curr]:
                visited[curr] = True
                cycle.append(curr)
                curr = arr[curr-1]
            cycles.append(tuple(cycle))
    return cycles
```

![image](https://hackmd.io/_uploads/S1ZIAGGVfl.png)

Một số tính chất của hoán vị  
**Định lí 1.** Nếu $\displaystyle \sigma =( i_{1} i_{2} \dotsc i_{k})$ và $\displaystyle \tau =( j_{1} j_{2} \dotsc j_{r})$ là hai xích độc lập thì $\displaystyle \sigma \tau =\tau \sigma$.

*Chứng minh.*

Vì $\displaystyle \sigma$ và $\displaystyle \tau$ là hai xích độc lập cho nên $\displaystyle \{i_{1} ,\dotsc ,i_{k}\} \cap \{j_{1} ,\dotsc ,j_{r}\} =\emptyset$. Với $\displaystyle i$ nằm ngoài hai tập trên thì ta có $\displaystyle \sigma ( \tau ( i)) =\tau ( \sigma ( i)) =i$ vì $\displaystyle \sigma ( i) =\tau ( i) =1$. Tương tự nếu $\displaystyle i\in \{i_{1} ,\dotsc ,i_{k}\}$ thì $\displaystyle \sigma ( i) \in \{i_{1} ,\dotsc ,i_{k}\}$ và $\displaystyle \tau ( i) =i$ cho nên $\displaystyle \sigma ( \tau ( i)) =\sigma ( i) =\tau ( \sigma ( i))$. Xét tương tự với $\displaystyle j\in \{j_{1} ,\dotsc ,j_{r}\}$.


**Định lí 2.** Mọi phép thế $\sigma \in S_n$ đều phân tích được thành một tích những chuyển vị

*Chứng minh.* Thật vậy, chẳng hạn với $\displaystyle ( i_{1} i_{2} \dotsc i_{k}) =( i_{1} i_{k})( i_{1} i_{k-1}) \dotsc ( i_{1} i_{3})( i_{1} i_{2})$

Gọi $\displaystyle s_{i} =( i\ i+1)$ là các phép chuyển vị đổi chỗ hai số $\displaystyle i$ và $\displaystyle i+1$. Khi đó ta có thể phân tích các phép chuyển vị thành tích của các $\displaystyle s_{i}$


$$
\begin{equation*}
( k\ l) =( k\ k+1)( k+1\ k+2) \dotsc ( l\ -1\ l)( l-2\ l-1) \dotsc ( k+1\ k+2)( k\ k+1)
\end{equation*}
$$

Sau đây là một số bài toán có sử dụng hoán vị để xử lí. 

## Ví dụ

### Bài 1

**Đề bài.** Tìm số nguyên dương $\displaystyle N$ lớn nhất thỏa mãn tồn tại một bảng ô vuông gồm 100 cột và $\displaystyle N$ hàng thỏa mãn đồng thời 2 điều kiện sau 


i/ Mỗi hàng chứa các số $\displaystyle 1,2,...,100$ theo một thứ tự nào đó

ii/ Với mỗi hàng $\displaystyle r,s$ phân biệt bất kì, thì luôn tồn tại một cột $\displaystyle c$ sao cho $\displaystyle |T( r,c) -T( s,c) |\geqslant 2$. Trong đó $\displaystyle T( r,c)$ là giá trị của số nằm ở hàng $\displaystyle r$, cột $\displaystyle c$. 

*Giải.* 

Trước khi bắt đầu, ta định nghĩa lại một số khái niệm như sau : 

*Định nghĩa.* Một hoán vị được gọi là hoán vị chẵn nếu như nó được biểu diễn dưới dạng tích của một số chẵn các phép chuyển vị. Tương tự cho hoán vị lẻ. 

Ví dụ cho hoán vị 312 của 123 thì hoán vị này là hoán vị chẵn vì 312=(23)(12), tức 312 thu được từ 123 bằng lần lượt các phép chuyển vị giữa số hạng thứ 2 và thứ 3, rồi sau đó chuyển vị số hạng thứ 1 và thứ 2. 


Quay trở lại bài toán. 

Ta sẽ coi mỗi hàng của bảng như là một hoán vị của bộ số $\displaystyle 1,2,...,100$ và viết $\displaystyle \pi _{r}$ là bộ hoán vị của hàng $\displaystyle r$. 

Tiếp theo ta xét 50 cặp $\displaystyle s_{k} =( 2k-1,2k) ,k=1,2,...,50$. Thì mỗi hàng $\displaystyle r$ như vậy là kết quả của các phép chuyển vị liên tiếp các cặp $\displaystyle s_{k}$ như trên. Bây giờ ta sẽ xét hai hàng $\displaystyle r,s$ sao cho $\displaystyle \pi _{s}$ thu được từ $\displaystyle \pi _{r}$ bằng cách thực hiện các phép chuyển vị các cặp $\displaystyle s_{k}$ trong $\displaystyle \pi _{r}$. Tức là trong $\displaystyle \pi _{r}$ ta sẽ chọn ra các số trong cặp $\displaystyle s_{k}$ như vậy, rồi hoán đổi vị trí của chúng cho nhau. Bằng cách này ta sẽ có $\displaystyle |\pi _{r}( i) -\pi _{s}( i) |\leqslant 1$ với mọi $\displaystyle i$. Bởi lẽ, các cột không được chuyển thì sẽ giữ nguyên giá trị còn 2 số $\displaystyle 2k-1$ và $\displaystyle 2k$ đổi vị trí cho nhau cho nên tồn tại $\displaystyle c$ để $\displaystyle |\pi _{r}( c) -\pi _{s}( c) |=|2k-2k+1|=1$. 

Đến đây ta có thể đánh giá được $\displaystyle N$ như sau. Đầu tiên có tổng cộng $\displaystyle 100!$ hoán vị được tạo nên từ 100 số như trên. Xét một hoán vị $\displaystyle \pi$ bất kì. Lúc này ta sẽ loại ra tất cả các bộ hoán vị khác thu được từ $\displaystyle \pi$ bằng cách thực hiện các phép chuyển vị cho 2 số trong các cặp $\displaystyle s_{k}$ như trên. Có tổng cộng $\displaystyle 2^{50}$ bộ như vậy vi phạm điều kiện ii/ của bài toán cho nên ta sẽ có tối đa $\displaystyle N\leqslant \frac{100!}{2^{50}}$ hàng. 

Bây giờ ta sẽ chỉ ra rằng $\displaystyle N$ như trên là lớn nhất có thể

**Bước 1.** Xây dựng 1 bảng thỏa mãn


Ý tưởng là thực hiện liên tiếp các quá trình để mở rộng bảng. Đầu tiên, với $\displaystyle n=2$ thì bảng chỉ có 1 hàng và 2 cột. Ta điền 2 số 1,2 vào. Tiếp theo ta xét $\displaystyle n=4$ và thêm 2 số 3,4 vào. Cứ như vậy cho tới $\displaystyle n=2k$ thì ta thêm 2 số trong cặp $\displaystyle s_{k}$ vào. 

Thuật toán như sau : Ta sẽ thêm 2 số trong cặp $\displaystyle s_{k}$ dựa vào vị trí của $\displaystyle 2k-2$. Cụ thể ta sẽ thêm $\displaystyle 2k-1,2k$ sao cho chúng cùng tạo với $\displaystyle 2k-2$ các hoán vị con có cùng tính chẵn lẻ. Ta không cần chúng đứng liền nhau mà chỉ cần dựa vào thứ tự xuất hiện của chúng trên mỗi hàng. 

Ví dụ, ta đã có số 1 trên bảng và cần điền 2 số 2 và 3 vào. Lúc này ta mong muốn tạo ra các hoán vị con đều là hoán vị chẵn của 3 số trên. Cụ thể 3 hoán vị chẵn của 3 số trên lần lượt là 123,231,312. Cách sắp xếp như vậy là tối ưu vì nếu như xếp chồng 2 hoán vị chẵn và lẻ lên nhau thì ta không thể thêm bất cứ hoán vị con nào vào nữa và chỉ được tối đa 2 bộ, trong khi cách sắp xếp trên ta có thể thêm tối đa 3 bộ hoán vị. Ví dụ ta điền 123 là hoán vị chẵn cùng vói 321 là hoán vị lẻ vào bảng thì không thể điền thêm bất cứ hoán vị nào khác nữa. Vì cho dù có điền bộ nào đi nữa thì cũng vi phạm điều kiện ii/ của bài toán 



<p align="center">
  <img src="https://hackmd.io/_uploads/HJf-KmzNGg.png" alt="Description">
</p>

Vậy cách điền trên là hợp lí. 

Ta cứ xây dựng dần dần lên như vậy là được. Cách điền sẽ tóm gọn lại như sau : 

Dựa vào vị trí của $\displaystyle 2k-2$ ta sẽ có 2 trường hợp

i/ Nếu như $\displaystyle 2k-2$ xuất hiện sau hoặc trước vị trí của 2 ô trống trên hàng đó thì ta sẽ điền $\displaystyle 2k-1,2k$ vào 2 ô trống theo thứ tự đó. 

ii/ Nếu như $\displaystyle 2k-2$ xuất hiện ở ngay giữa vị trí 2 ô trống thì ta điền $\displaystyle 2k$ trước, sau đó điền $\displaystyle 2k-1$ sau theo chiều từ trái sang phải.

Minh họa thử 1 cách điền như sau : đầu tiên ta xét 2 số có sẵn trên bảng là 1,2 và ta giữ nguyên thứ tự xuất hiện của 2 số này trên mỗi hàng kể từ giờ về sau. Xét một bảng gồm 4 cột và 6 hàng đồng thời thỏa mãn yêu cầu bài toán. Thứ tự của bộ $\displaystyle \{2,3,4\}$ sẽ là $\displaystyle \{2,3,4\} ,\{3,4,2\} ,\{4,2,3\}$



<p align="center">
  <img src="https://hackmd.io/_uploads/HkJQKmM4Gg.png" alt="Description">
</p>

Theo quy nạp, bảng gồm $\displaystyle 2k-2$ cột sẽ có tối đa $\displaystyle N=\frac{( 2k-2) !}{2^{k-1}}$ và chọn ra mỗi hàng như vậy, ta điền 2 số $\displaystyle 2k-1,2k$ vào 2 ô bất kì theo cách như trên thì sẽ có tổng cộng $\displaystyle N=\frac{( 2k-2) !}{2^{k-1}} .\binom{2k}{2} =\frac{( 2k) !}{2^{k}}$ hàng. 


**Bước 2.** Chứng minh rằng bảng được xây dựng như trên thỏa mãn yêu cầu bài toán. 

Từ cách xây dựng bảng như trên ta có nhận xét rằng trên mọi hàng thì ta luôn có các hoán vị con của $\displaystyle \{1,2\} ,\{2,3,4\} ,...,\{98,99,100\}$ đều là hoán vị chẵn. 

Tiếp theo ta chứng minh một bổ đề như sau :

*Bổ đề.* Cho $\displaystyle \pi _{1}$ và $\displaystyle \pi _{2}$ là hai hoán vị của $\displaystyle \{1,2,...,100\}$ sao cho $\displaystyle |\pi _{1}( i) -\pi _{2}( i) |\leqslant 1$ với mọi $\displaystyle i$. Khi đó tồn tại tập $\displaystyle S$ gồm các cặp $\displaystyle ( i,i+1)$ sao cho $\displaystyle \pi _{2}$ thu được từ $\displaystyle \pi _{1}$ bằng cách thực hiện các phép chuyển vị các cặp $\displaystyle ( i,i+1)$ trong $\displaystyle \pi _{1}$.

Bổ đề trên có thể được chứng minh khá đơn giản bằng quy nạp.

Quay trở lại bài toán, giả sử trong bảng được xây dựng như trên tồn tại hai hàng $\displaystyle \pi _{1}$ và $\displaystyle \pi _{2}$ thỏa mãn $\displaystyle |\pi _{1}( c) -\pi _{2}( c) |\leqslant 1,\forall c$. 

Từ bổ đề ta suy ra tồn tại một tập $\displaystyle S$ sao cho mỗi phần tử trong $\displaystyle S$ chênh lệch nhau ít nhất là 2 đơn vị và đồng thời với mỗi $\displaystyle j\in S$ thì $\displaystyle \pi _{2}$ thu được từ $\displaystyle \pi _{1}$ bằng cách thực hiện các phép chuyển vị các phần tử $\displaystyle ( j,j+1)$ trong $\displaystyle \pi _{1}$. 

Bây giờ gọi $\displaystyle r=\min S$ thì sẽ có 2 trường hợp. Trường hợp đầu tiên $\displaystyle r=2k-1$ là số lẻ. Thì khi đó ta sẽ chuyển vị cặp $\displaystyle ( 2k-1,2k)$. Nhưng để ý rằng trong $\displaystyle \pi _{1} ,\pi _{2}$ thì các hoán vị con của $\displaystyle ( 2k-2,2k-1,2k)$ đều cùng tính chẵn lẻ (với $\displaystyle k=1$ thì ta sẽ chuyển vị cặp $\displaystyle ( 1,2)$ cũng sẽ tạo ra điều vô lí). Nếu muốn tạo ra 2 hoán vị con cùng chẵn thì cần phải có $\displaystyle 2k-3\in S$ để thực hiện phép chuyển vị chứa $\displaystyle 2k-2$. Nhưng điều này là không thể vì $\displaystyle r=\min S$. Cho nên trường hợp này loại.

Tiếp theo ta xét $\displaystyle r=2k$ thì tương tự như vậy $\displaystyle \pi _{1} ,\pi _{2}$ cảm sinh 2 hoán vị con của $\displaystyle \{2k,2k+1,2k+2\}$ cùng tính chẵn lẻ cho nên cần có $\displaystyle 2k+2\in S$ và tương tự $\displaystyle 98\in S$. Nhưng khi đó ta lại có điều mâu thuẫn vì $\displaystyle \pi _{1} ,\pi _{2}$ cảm sinh hai hoán vị con khác tính chẵn lẻ của $\displaystyle \{98,99,100\}$. Và từ đây ta có điều phải chứng minh. 


### Bài 2

**Đề bài.** Với mọi dãy hữu hạn $\displaystyle ( x_{1} ,x_{2} ,...,x_{n})$, kí hiệu $\displaystyle N( x_{1} ,x_{2} ,...,x_{n})$ là số lượng cặp chỉ số $\displaystyle ( i,j)$ sao cho $\displaystyle 1\leqslant i< j\leqslant n$ và $\displaystyle x_{i} =x_{j}$. Cho $\displaystyle p$ là một số nguyên tố lẻ thỏa mãn $\displaystyle 1\leqslant n< p$ và $\displaystyle a_{1} ,a_{2} ,...,a_{n}$ và $\displaystyle b_{1} ,b_{2} ,...,b_{n}$ là các lớp thặng dư theo tùy ý theo modulo $\displaystyle p$. Chứng minh rằng tồn tại một hoán vị $\displaystyle \pi $ của các chỉ số $\displaystyle 1,2,...,n$ sao cho 

$$
\begin{equation*}
N( a_{1} +b_{\pi ( 1)} ,a_{2} +b_{\pi ( 2)} ,...,a_{n} +b_{\pi ( n)}) \leqslant \min( N( a_{1} ,a_{2} ,...,a_{n}) ,N( b_{1} ,b_{2} ,...,b_{n}))
\end{equation*}
$$



*Giải.* 

Tương tự bài trước, ta có các kí hiệu như sau: $\displaystyle S_{m}$ để chỉ tập các hoán vị của $\displaystyle \{1,2,...,m\}$ và với mỗi $\displaystyle \sigma \in S_{m}$ ta có $\displaystyle \operatorname{sgn} \sigma $ để chỉ dấu của hoán vị. Nếu $\displaystyle \sigma $ là hoán vị chẵn thì $\displaystyle \operatorname{sgn} \sigma =+1$ và ngược lại, nếu $\displaystyle \sigma $ là hoán vị lẻ thì $\displaystyle \operatorname{sgn} \sigma =-1$

Trường hợp đơn giản nhất, ta sẽ thử chứng minh bài toán với dãy $\displaystyle a_{1} ,a_{2} ,...,a_{n}$ đôi một phân biệt. Như vậy $\displaystyle N( a_{1} ,a_{2} ,...,a_{n}) =0$ dẫn tới $\displaystyle \min( N( A) ,N( B)) =0$ với $\displaystyle A=( a_{1} ,a_{2} ,...,a_{n})$ và $\displaystyle B=( b_{1} ,b_{2} ,...,b_{n})$. Vì vai trò của $\displaystyle A$ và $\displaystyle B$ là như nhau cho nên ta chỉ cần chứng minh với $\displaystyle A$ là đủ. 



Ta cần chỉ ra rằng tồn tại một hoán vị $\displaystyle \pi $ sao cho $\displaystyle \{a_{i} +b_{\pi ( i)}\}_{i=1}^{n}$ gồm các lớp thặng dư phân biệt theo modulo $\displaystyle p$.

Để chứng minh ta sẽ dùng tới định lý không điểm tổ hợp như sau: 

**Bổ đề.** Cho $\displaystyle \mathbb{R}$ là một trường bất kì và $\displaystyle P( x_{1} ,x_{2} ,...,x_{n}) \in \mathbb{R}[ x_{1} ,x_{2} ,...,x_{n}]$ là một đa thức có bậc $\displaystyle \deg P=t_{1} +t_{2} +...+t_{n}$ với $\displaystyle t_{i}$ là các số nguyên không âm và hệ số của đơn thức $\displaystyle x_{1}^{t_{1}} x_{2}^{t_{2}} ...x_{n}^{t_{n}}$ khác $\displaystyle 0$. Nếu $\displaystyle S_{1} ,S_{2} ,...,S_{n} \subset \mathbb{R}$ sao cho $\displaystyle |S_{i} | >t_{i}$ thì tồn tại bộ $\displaystyle ( s_{1} ,s_{2} ,...,s_{n}) \in S_{1} \times S_{2} \times ...\times S_{n}$ sao cho $\displaystyle P( s_{1} ,s_{2} ,...,s_{n}) \neq 0$.


*Chứng minh.*

Ta chứng minh quy nạp theo $\displaystyle \deg P$. Trường hợp $\displaystyle \deg P=1$ thì không mất tính tổng quát giả sử $\displaystyle t_{1} =1$, lúc này hệ số của $\displaystyle x_{1}^{t_{1}}$ khác 0 cho nên khẳng định của định lí là hiển nhiên.

Giả sử bổ đề đúng với mọi đa thức $\displaystyle P$ sao cho $\displaystyle \deg P< d$. Ta chứng minh bổ đề vẫn đúng với $\displaystyle \deg P=d$.

Giả sử phản chứng rằng tồn tại một đa thức $\displaystyle P( s_{1} ,s_{2} ,...,s_{n}) =0$ với mọi $\displaystyle ( s_{1} ,s_{2} ,...,s_{n}) \in S_{1} \times S_{2} \times ...\times S_{n}$. Do $\displaystyle \deg P=t_{1} +t_{2} +...+t_{n}  >0$ cho nên không mất tính tổng quát, ta có thể giả sử $\displaystyle t_{1}  >0$. Cố định $\displaystyle s_{1} \in S_{1}$. Lúc này ta coi $\displaystyle P$ như một đa thức theo biến $\displaystyle x_{1}$ với các hệ số thuộc $\displaystyle \mathbb{R}[ x_{2} ,...,x_{n}]$. Thực hiện thuật toán chia đa thức ta được 

$$
\begin{equation*}
P=( x_{1} -s_{1}) Q+R
\end{equation*}
$$

trong đó $\displaystyle \deg_{x_{1}} Q=\deg_{x_{1}} P-1$. Vì bậc của $\displaystyle R$ theo biến $\displaystyle x_{1}$ là bé hơn $\displaystyle x_{1} -s_{1}$ nên ta có $\displaystyle \deg_{x_{1}} R\leqslant 0$ và đa thức $\displaystyle R$ không chứa biến $\displaystyle x_{1}$. Do giả thiết, đa thức $\displaystyle Q$ phải chứa đơn thức $\displaystyle x_{1}^{t_{1} -1} x_{2}^{t_{2}} ...x_{n}^{t_{n}}$ với hệ số khác $\displaystyle 0$. Thay $\displaystyle x_{1} =s_{1}$ và $\displaystyle ( s_{2} ,...,s_{n}) \in S_{2} \times ...S_{n}$ vào đẳng thức trên và áp dụng giả thiết phản chứng ta có 

$$
\begin{gather*}
P( s_{1} ,...,s_{n}) =( s_{1} -s_{1}) Q( s_{1} ,s_{2} ,...,s_{n}) +R( s_{2} ,...,s_{n})\\
\Longrightarrow 0=R( s_{2} ,...,s_{n})
\end{gather*}
$$

hay $\displaystyle R( s_{2} ,...,s_{n}) =0$ với mọi $\displaystyle ( s_{2} ,...,s_{n}) \in S_{2} \times ...\times S_{n}$ 

Điều này dẫn tới 

$$
\begin{gather*}
P\left( s_{1}^{'} ,s_{2} ,...,s_{n}\right) =0=\left( s_{1}^{'} -s_{1}\right) Q\left( s_{1}^{'} ,s_{2} ,...,s_{n}\right)\\
\Longrightarrow Q\left( s_{1}^{'} ,s_{2} ,...,s_{n}\right) =0,\forall \left( s_{1}^{'} ,s_{2} ,...,s_{n}\right) \in ( S_{1} \backslash \{s_{1}\}) \times S_{2} \times ...\times S_{n}
\end{gather*}
$$

Do $\displaystyle \deg Q=( t_{1} -1) +t_{2} +...+t_{n}$ và hệ số của $\displaystyle x_{1}^{t_{1} -1} x_{2}^{t_{2}} ...x_{n}^{t_{n}}$ khác 0 cho nên theo giả thiết quy nạp với $\displaystyle t_{1}^{'} =t_{1} -1$ và $\displaystyle S_{1}^{'} =S_{1} \backslash \{s_{1}\}$ thì ta có điều mâu thuẫn. 

Từ đây ta có điều phải chứng minh. 

Bây giờ ta sẽ chứng minh nhận xét: Tồn tại một hoán vị $\displaystyle \pi $ sao cho $\displaystyle \{a_{i} +b_{\pi ( i)}\}_{i=1}^{n}$ gồm các lớp thặng dư phân biệt theo modulo $\displaystyle p$.

*Chứng minh.* 

Ta kí hiệu đa thức Vandermonde cho các biến $\displaystyle x_{1} ,...,x_{n}$ như sau

$$
\begin{gather*}
V( x_{1} ,x_{2} ,...,x_{n}) =\prod _{1\leqslant i< j\leqslant n}( x_{j} -x_{i})\\
=\det\begin{pmatrix}
1 & x_{1} & x_{1}^{2} & \dotsc  & x_{1}^{n-1}\\
1 & x_{2} & x_{2}^{2} & \dotsc  & x_{2}^{n-1}\\
\vdots  & \vdots  & \vdots  & \ddots  & \vdots \\
1 & x_{n} & x_{n}^{2} & \dotsc  & x_{n}^{n-1}
\end{pmatrix}\\
=\sum _{\sigma \in S_{n}}\left(\operatorname{sgn} \sigma \right) x_{1}^{\sigma ( 1) -1} x_{2}^{\sigma ( 2) -1} \dotsc x_{n}^{\sigma ( n) -1}
\end{gather*}
$$

Ta nhận thấy rằng nếu như $\displaystyle x_{i} \neq x_{j} ,\forall i,j$ thì đa thức Vandermonde sẽ khác $\displaystyle 0$. Hơn nữa nó còn là đa thức luân phiên, tức là với mỗi $\displaystyle \pi \in S_{n}$ thì ta có 

$$
\begin{equation*}
V( x_{\pi ( 1)} ,...,x_{\pi ( n)}) =\left(\operatorname{sgn} \pi \right) V( x_{1} ,...,x_{n})
\end{equation*}
$$


Xét đa thức sau với các hệ số trong trường $\displaystyle \mathbb{F}_{p}$ 

$$
\begin{equation*}
f( x_{1} ,...,x_{n}) =V( x_{1} ,...,x_{n}) \cdot V( x_{1} +b_{1} ,...,x_{n} +b_{n})
\end{equation*}
$$

$\displaystyle \deg f=t_{1} +...+t_{n} =n( n-1)$ và $\displaystyle t_{1} =...=t_{n} =n-1$ và $\displaystyle S_{1} =...=S_{n} =\{a_{1} ,...,a_{n}\}$. Để áp dụng được bổ đề ta cần tính hệ số của $\displaystyle x_{1}^{n-1} ...x_{n}^{n-1}$ để đảm bảo nó khác $\displaystyle 0$.Khai triển $\displaystyle f$ ta có 

$$
\begin{gather*}
f( x_{1} ,...,x_{n}) =\left(\sum _{\sigma \in S_{n}}\left(\operatorname{sgn} \sigma \right) \cdot \prod _{i=1}^{n} x_{i}^{\sigma ( i) -1}\right)\left(\sum _{\tau \in S_{n}}\left(\operatorname{sgn} \tau \right) \cdot \prod _{i=1}^{n}( x_{i} +b_{i})^{\tau ( i) -1}\right)\\
=\sum _{\sigma \in S_{n}}\sum _{\tau \in S_{n}}\left(\operatorname{sgn} \sigma \right) \cdot \left(\operatorname{sgn} \tau \right) \cdot \left(\prod _{i=1}^{n} x_{i}^{\sigma ( i) -1}\right)\left(\prod _{i=1}^{n}( x_{i} +b_{i})^{\tau ( i) -1}\right)
\end{gather*}
$$

Nhận xét rằng đơn thức $\displaystyle x_{1}^{n-1} ...x_{n}^{n-1}$ chỉ xuất hiện tại các hoán vị thỏa mãn $\displaystyle \sigma ( i) -1+\tau ( i) -1=n-1$ tương đương với $\displaystyle \sigma ( i) +\tau ( i) =n+1$

Xét $\displaystyle \varphi \in S_{n}$ là một hoán vị thỏa mãn $\displaystyle \varphi ( i) =n+1-i$ thì lúc này $\displaystyle \varphi ( \sigma ( i)) =\varphi ( n+1-\tau ( i)) =( n+1) -( n+1-\tau ( i)) =\tau ( i)$ cho nên $\displaystyle \tau =\varphi \circ \sigma$ dẫn tới 

$$
\begin{gather*}
\sigma \cdot \tau ^{-1} =\sigma \cdot \left( \sigma ^{-1} \cdot \varphi ^{-1}\right) =\varphi ^{-1}\\
\Longrightarrow \operatorname{sgn}\left( \sigma \cdot \tau ^{-1}\right) =\operatorname{sgn}\left( \varphi ^{-1}\right) =\operatorname{sgn}\left( \varphi ^{-1}\right) =\operatorname{sgn}( \sigma \cdot \tau )
\end{gather*}
$$

vì $\displaystyle \operatorname{sgn}\left( \phi ^{-1}\right) =\operatorname{sgn}( \phi )$. Điều nãy dẫn tới hệ số của $\displaystyle x_{1}^{n-1} ...x_{n}^{n-1}$ sẽ là $\displaystyle n!\operatorname{sgn}( \varphi )$. Vì với mỗi hoán vị $\displaystyle \sigma $ như vậy ta chọn được duy nhất một hoán vị $\displaystyle \tau $ thỏa mãn $\displaystyle \sigma ( i) +\tau ( i) =n+1$ và có $\displaystyle n!$ hoán vị $\displaystyle \sigma $ cho nên ta có $\displaystyle n!\times \operatorname{sgn}( \varphi )$. Rõ ràng hệ số này khác 0 vì $\displaystyle n< p$ cho nên $\displaystyle n!$ không chia hết cho $\displaystyle p$. 



Theo bổ đề thì tồn tại các phần tử $\displaystyle s_{1} ,s_{2} ,...,s_{n} \in \{a_{1} ,a_{2} ,...,a_{n}\}$ sao cho $\displaystyle f( s_{1} ,s_{2} ,...,s_{n}) \neq 0$. Do $\displaystyle \mathbb{F}_{p}$ là một trường cho nên ta có $\displaystyle V( s_{1} ,...,s_{n}) \neq 0$ và $\displaystyle V( s_{1} +b_{1} ,...,s_{n} +b_{n}) \neq 0$. $\displaystyle V( s_{1} ,...,s_{n}) \neq 0$ khi và chỉ khi $\displaystyle s_{1} ,...,s_{n}$ đôi một phân biệt hay nói cách khác dãy $\displaystyle s_{i}$ là một hoán vị của $\displaystyle a_{i}$ : $\displaystyle s_{i} =a_{\pi ( i)}$. Tương tự ta cũng có $\displaystyle a_{\pi ( i)} +b_{i}$ đôi một phân biệt do $\displaystyle V( s_{1} +b_{1} ,...,s_{n} +b_{n})$ khác $\displaystyle 0$. Từ đây ta có điều phải chứng minh. 

Tiếp theo ta sẽ chứng minh khẳng định sau và hoàn tất bài toán: Do $\displaystyle A$ và $\displaystyle B$ có vai trò như nhau nên không mất tính tổng quát giả sử $\displaystyle N( a_{1} ,...,a_{n}) \leqslant N( b_{1} ,...,b_{n})$. Lúc này $\displaystyle \min( N( a_{1} ,...,a_{n}) ,N( b_{1} ,...,b_{n})) =N( a_{1} ,...,a_{n})$.

Cuối cùng ta cần chứng minh rằng: Với $\displaystyle 0\leqslant n< p$, tồn tại một hoán vị $\displaystyle \pi \in S_{n}$ sao cho $\displaystyle N( a_{1} +b_{\pi ( 1)} ,...,a_{n} +b_{\pi ( n)}) \leqslant N( a_{1} ,...,a_{n})$

*Chứng minh.* 

Ta sẽ quy nạp theo $\displaystyle n$. Khẳng định là hiển nhiên cho $\displaystyle n=0,n=1$. Xét $\displaystyle 2\leqslant n< p$ và giả sử khẳng định là đúng cho các trường hợp nhỏ hơn. 



Xét trong dãy $\displaystyle a_{1} ,...,a_{n}$ có $\displaystyle k$ phần tử phân biệt. Ta sắp xếp chúng lại theo thứ tự $\displaystyle a_{1} ,a_{2} ,...,a_{k}$. Còn lại $\displaystyle a_{k+1} ,...,a_{n}$, mỗi số trong đây sẽ tạo thành 1 cặp với các số trong $\displaystyle a_{1} ,...,a_{k}$ để tạo thành 1 cặp $\displaystyle i\leqslant k< j$ thỏa mãn $\displaystyle a_{i} =a_{j}$ và có đúng $\displaystyle n-k$ cặp như vậy. Như vậy 
\begin{equation*}
N( a_{1} ,...,a_{n}) =( n-k) +N( a_{k+1} ,...,a_{n})
\end{equation*}
Các phần tử trong $\displaystyle a_{k+1} ,...,a_{n}$ không đảm bảo là phân biệt vì có thể có nhiều hơn 1 phần tử trong dãy trên bằng với các phần tử trong dãy $\displaystyle a_{1} ,...,a_{k}$. 

Theo nhận xét ở trên thì tồn tại một hoán vị $\displaystyle \pi _{1}$ của $\displaystyle 1,2,...,k$ sao cho $\displaystyle a_{1} +b_{\pi _{1}( 1)} ,...,a_{k} +b_{\pi _{1}( k)}$ đôi một phân biệt. Mặt khác theo giả thiết quy nạp thì tồn tại hoán vị $\displaystyle \pi _{2}$ của $\displaystyle k+1,...,n$ sao cho 

$$
\begin{equation*}
N( a_{k+1} +b_{\pi _{2}( k+1)} ,...,a_{n} +b_{\pi _{2}( n)}) \leqslant N( a_{k+1} ,...,a_{n})
\end{equation*}
$$

Ta sẽ kết hợp $\displaystyle \pi _{1}$ và $\displaystyle \pi _{2}$ lại để tạo ra một hoán vị mới là $\displaystyle \pi $. Hai hoán vị $\displaystyle \pi _{1}$ và $\displaystyle \pi _{2}$ không giao nhau vì chúng là hoán vị của hai tập khác nhau. Lúc này, từ định nghĩa của $\displaystyle \pi _{1}$ ta có $\displaystyle a_{1} +b_{\pi ( 1)} ,...,a_{k} +b_{\pi ( k)}$ là phân biệt. Mặt khác với mỗi $\displaystyle k< j\leqslant n$ thì tồn tại tối đa một chỉ số $\displaystyle i\leqslant k$ sao cho $\displaystyle a_{i} +b_{\pi ( i)} =a_{j} +b_{\pi ( j)}$. Dẫn tới bất đẳng thức sau

$$
\begin{gather*}
N( a_{1} +b_{\pi ( 1)} ,...,a_{n} +b_{\pi ( n)}) \leqslant n-k+N( a_{k+1} +b_{\pi ( k+1)} ,...,a_{n} +b_{\pi ( n)})\\
\leqslant n-k+N( a_{k+1} ,...,a_{n}) =N( a_{1} ,...,a_{n})
\end{gather*}
$$

Vậy ta có điều phải chứng minh và bài toán hoàn tất. 

### Bài 3

**Đề bài.** Cho $\displaystyle n$ là một số nguyên dương. Marci viết $\displaystyle n$ số nguyên dương vào vở theo một thứ tự ngẫu nhiên và chỉ có một mình Marci thấy được. Giả sử thứ tự đó là $\displaystyle m( 1) ,m( 2) ,...,m( n)$ hay hoán vị $\displaystyle m$ và mục tiêu của ta là xác định được hoán vị này. Ở mỗi bước, ta sẽ đưa cho Marci một danh sách $\displaystyle n$ số nguyên dương theo thứ tự của ta, lần lượt là $\displaystyle a( 1) ,a( 2) ,...,a( n)$. Marci sau đó vẽ một đồ thị có hướng gồm $\displaystyle n$ đỉnh, đánh số từ $\displaystyle 1$ tới $\displaystyle n$ và Marci sau đó vẽ một cạnh có hướng đi từ $\displaystyle i$ tới $\displaystyle m( a( i))$ với mỗi $\displaystyle 1\leqslant i\leqslant n$. Cuối cùng, đồ thị này sẽ được phân hoạch thành các chu trình rời nhau và Marci sẽ cho ta biết số lượng các chu trình này. 

a/ Chứng minh rằng hoán vị bí mật của Marci có thể được xác định trong tối đa $\displaystyle n\log_{2}( n)$ bước

b/ Liệu có tồn tại một hằng số $\displaystyle c< 1$ sao cho với mỗi số nguyên dương $\displaystyle n$, ta có thể xác định được hoán vị bí mật trong không quá $\displaystyle cn\log_{2}( n)$ bước. 