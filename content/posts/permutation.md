+++
date = '2026-07-20'
title = 'Một số bài toán về hoán vị'
toc = true
math = true 
tags = ["math"]
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


