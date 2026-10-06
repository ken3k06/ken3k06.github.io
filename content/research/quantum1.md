+++
date = '2026-09-10T15:55:04+07:00'
title = 'An introduction to Quantum Computing - Part 1'
toc = true
math = true 
+++

## Lời mở đầu


Kì này mình có đăng ký học môn Lập trình cho máy tính lượng tử (SE366.R11) ở trên trường, mình thấy môn này khá hay ~~và cũng có dự định làm nghiên cứu về quantum~~ cho nên mình muốn viết series này để note lại một số thứ mình học được về Quantum. Lưu ý rằng bài viết có thể chứa khá nhiều lỗi, một phần vì mình không phải là sinh viên ngành Toán hay Vật lý, cho nên ở cuối bài mình sẽ trích dẫn một số tài liệu tham khảo để mọi người cùng đọc và sẽ rất vui nếu nhận được góp ý từ mọi người. 


Một số tài liệu tham khảo

[1] [Quantum Computing : An Applied Approach, Jack D. Hidary](https://drive.google.com/file/d/1BjOIomqfznzu4ibIQ7khQWjh7O_syx3s/view?usp=sharing)

[2] [Quantum Computation and Quantum Information, Michael A. Nielsen and Isaac L. Chuang](https://drive.google.com/file/d/1s1DR5NEUmF81DDWnS4iZa2ntcW_dw_p8/view?usp=sharing)

[3] Mật mã hậu lượng tử, PGS.TS Nguyễn Hiếu Minh 

[4] [abgrilo.github.io/viasm.html](https://abgrilo.github.io/viasm.html)

## Khái niệm cơ bản 

Hành vi của máy tính cổ điển hiện nay có thể được mô tả bằng các định luật vật lý cổ điển. Tuy nhiên điều này không phải lúc nào cũng đúng vì các vật thể ở quy mô nguyên tử hoạt động khác nhau trong các thí nghiệm so với dự đoán của vật lý cổ điển. Do đó để mô tả chính xác các hệ thống này, các nhà khoa học đã phát triển một lý thuyết vật lý mới gọi là vật lý lượng tử. Máy tính lượng tử cũng được ra đời dựa trên các định luật vật lý này. 

Máy tính lượng tử là một thiết bị sử dụng các định luật vật lý lượng tử để giải các bài toán. Có nhiều cách mà máy được thực hiện, tuy nhiên ta không cần quan tâm điều đó ở đây. Điều quan trọng cần lưu ý đó chính là máy tính lượng tử đã được thực hiện thành công.

Để mô tả cách hoạt động của máy tính lượng tử, ta cần một bộ quy tắc toán học sau đây. 

### Qubit 

Trong máy tính cổ điển, thông tin được lưu trữ dưới dạng bit. Mỗi bit trong máy tính được hiểu là một đối tượng tồn tại ở một trong hai trạng thái là $\displaystyle 0$ và $\displaystyle 1$. Máy tính có thể thao tác trạng thái của bit bằng các phép toán khác nhau và có thể kiểm tra trạng thái mà bit hiện đang tồn tại. 



Bây giờ, ta sẽ biểu diễn mỗi bit bởi một trong hai trạng thái kí hiệu là $\displaystyle \ket{0}$ và $\displaystyle \ket{1}$. 



Kí hiệu $\displaystyle \ket{}$ còn được gọi là Ket. Ta viết mỗi bit dưới dạng

$$
\begin{equation*}
\ket{0} =\begin{pmatrix}
1\\
0
\end{pmatrix} ,\ket{1} =\begin{pmatrix}
0\\
1
\end{pmatrix}
\end{equation*}
$$

Nếu ta muốn biểu diễn nhiều hơn 1 bit thì sao? Trong máy tính cổ điển ta có thể viết dưới dạng sau:
$$
\begin{equation*}
00,01,10,11
\end{equation*}
$$

Để biểu diễn các bit này dưới dạng một vector thì cần một phép toán mới gọi là tích Tensor. Cụ thể, với hai ma trận $\displaystyle A,B$ có dạng 

$$
\begin{equation*}
A=\begin{pmatrix}
a_{11} & \dotsc  & a_{1n}\\
\vdots  & \dotsc  & \vdots \\
a_{m1} & \dotsc  & a_{mn}
\end{pmatrix} ,B=\begin{pmatrix}
b_{11} & \dotsc  & b_{1n'}\\
\vdots  & \dotsc  & \vdots \\
b_{m'1} & \dotsc  & b_{m'n'}
\end{pmatrix}
\end{equation*}
$$

thì tích tensor giữa $\displaystyle A$ và $\displaystyle B$, kí hiệu $\displaystyle A\otimes B$ sẽ bằng: 

$$
\begin{equation*}
A\otimes B=\begin{pmatrix}
a_{11} B & \dotsc  & a_{1n} B\\
\vdots  & \dotsc  & \vdots \\
a_{m1} B & \dotsc  & a_{mn} B
\end{pmatrix}
\end{equation*}
$$

Với bit $\displaystyle 00$, ta sẽ chuyển thành 

$$
\begin{equation*}
\ket{0} \otimes \ket{0} =\begin{pmatrix}
1\\
0
\end{pmatrix} \otimes \begin{pmatrix}
1\\
0
\end{pmatrix} =\begin{pmatrix}
1\\
0\\
0\\
0
\end{pmatrix}
\end{equation*}
$$

Tương tự 

$$
\begin{equation*}
\ket{0} \otimes \ket{1} =\begin{pmatrix}
1\\
0
\end{pmatrix} \otimes \begin{pmatrix}
0\\
1
\end{pmatrix} =\begin{pmatrix}
0\\
1\\
0\\
0
\end{pmatrix}
\end{equation*}
$$

Ta có thể viết vắn tắt dưới dạng 

$$
\begin{equation*}
\ket{0}\ket{0} ,\ket{0}\ket{1} ,\ket{1}\ket{0} ,\ket{1}\ket{1}
\end{equation*}
$$

hoặc 

$$
\begin{equation*}
\ket{00} ,\ket{01} ,\ket{10} ,\ket{11}
\end{equation*}
$$

Tương tự với các giá trị lớn hơn ta sẽ làm như sau: 

$$
\begin{equation*}
\ket{5}_{3} =\ket{1} \otimes \ket{0} \otimes \ket{1} =\begin{pmatrix}
0\\
1
\end{pmatrix} \otimes \begin{pmatrix}
1\\
0
\end{pmatrix} \otimes \begin{pmatrix}
0\\
1
\end{pmatrix} =\begin{pmatrix}
0\\
1\\
0\\
0
\end{pmatrix} \otimes \begin{pmatrix}
0\\
1
\end{pmatrix} =\begin{pmatrix}
0\\
0\\
0\\
0\\
0\\
1\\
0\\
0
\end{pmatrix}
\end{equation*}
$$

Tổng quát, giả sử $\displaystyle x$ được biểu diễn dưới dạng nhị phân $\displaystyle x=\sum _{j=0}^{n-1} x_{j} 2^{j}$ thì bit $\displaystyle \ket{x}_{n}$ sẽ được biểu diễn như sau 

$$
\begin{equation*}
\ket{x}_{n} =\ket{x}_{n-1} \otimes \ket{x}_{n-2} \otimes \dotsc \otimes \ket{x}_{1} \otimes \ket{x}_{0}
\end{equation*}
$$

Hoặc viết ngắn gọn 

$$
\begin{equation*}
\ket{x}_{n} =\ket{x_{n-1} x_{n-2} \dotsc x_{1} x_{0}}
\end{equation*}
$$

Trong máy tính lượng tử, thông tin được lưu trữ và hoạt động dưới dạng các bit lượng tử hay còn gọi là qubit (quantum bit). Một qubit có thể tồn tại ở một trong nhiều trạng thái khác nhau. Một trạng thái như vậy của qubit được biểu diễn dưới dạng một vector đơn vị trong một không gian vector phức hai chiều. Để biểu diễn một vector như vậy thì ta cần chọn một cơ sở. Ở đây ta sẽ chọn cơ sở $\displaystyle \left\{\ket{0} =\begin{pmatrix}
1\\
0
\end{pmatrix} ,\ket{1} =\begin{pmatrix}
0\\
1
\end{pmatrix}\right\}$. Cơ sở này còn được gọi là cơ sở trực chuẩn thuận tiện (convenient orthonormal basis) và ta sẽ gọi nó là cơ sở tính toán (computational basis). Nói cách khác, trạng thái tổng quát của một qubit có thể được biểu diễn dưới dạng 

$$
\begin{equation*}
\ket{\phi } =\alpha \ket{0} +\beta \ket{1} \in \mathbb{C}^{2}
\end{equation*}
$$

trong đó $\displaystyle \alpha $ và $\displaystyle \beta $ được gọi là biên độ (amplitude) của $\displaystyle \ket{0}$ và $\displaystyle \ket{1}$, và $\displaystyle \alpha ,\beta \in \mathbb{C}$. Vì $\displaystyle \ket{\phi }$ là một vector đơn vị nên ta sẽ có $\displaystyle |\alpha |^{2} +|\beta |^{2} =1$. 

Như vậy, ta có thể hiểu rằng, một trạng thái tổng quát của một qubit là sự chồng chập trạng thái của hai qubit cơ bản là qubit $\displaystyle \ket{0}$ và $\displaystyle \ket{1}$. 



Một số kí hiệu khác mà ta cần nắm:

Ket để chỉ các vector cột, kí hiệu là $\displaystyle \ket{\psi } =\begin{pmatrix}
a_{1}\\
a_{2}\\
\dotsc \\
a_{m}
\end{pmatrix} ,\ket{\varphi } =\begin{pmatrix}
b_{1}\\
b_{2}\\
\dotsc \\
b_{m}
\end{pmatrix}$

Ngược lại với Ket ta có Bra để chỉ các vector hàng và hơn nữa nó là liên hợp của Ket 

$$
\begin{equation*}
\bra{\psi } =\begin{pmatrix}
a_{1}^{*} & a_{2}^{*} & \dotsc  & a_{m}^{*}
\end{pmatrix} ,\bra{\varphi } =\begin{pmatrix}
b_{1}^{*} & b_{2}^{*} & \dotsc  & b_{m}^{*}
\end{pmatrix}
\end{equation*}
$$

Braket để chỉ tích nội của hai vector 

$$
\begin{gather*}
\bra{\varphi }\ket{\psi } =\begin{pmatrix}
b_{1}^{*} & b_{2}^{*} & \dotsc  & b_{m}^{*}
\end{pmatrix}\begin{pmatrix}
a_{1}\\
a_{2}\\
\dotsc \\
a_{m}
\end{pmatrix}\\
=\sum _{i\in [m]} b_{i}^{*} a_{i} \in \mathbb{C}
\end{gather*}
$$
Ngược lại ta có Ketbra 

$$
\begin{gather*}
\ket{\varphi }\bra{\psi } =\begin{pmatrix}
b_{1}\\
b_{2}\\
\dotsc \\
b_{m}
\end{pmatrix}\begin{pmatrix}
a_{1}^{*} & a_{2}^{*} & \dotsc  & a_{m}^{*}
\end{pmatrix}\\
=\begin{pmatrix}
b_{1} a_{1}^{*} & b_{1} a_{2}^{*} & \dotsc  & b_{1} a_{m}^{*}\\
b_{2} a_{1}^{*} & b_{2} a_{2}^{*} & \dotsc  & b_{2} a_{m}^{*}\\
\dotsc  & \dotsc  & \dotsc  & \dotsc \\
b_{m} a_{1}^{*} & b_{m} a_{2}^{*} & \dotsc  & b_{m} a_{m}^{*}
\end{pmatrix}
\end{gather*}
$$

Ngoài ra ta còn có một cách biểu diễn khác cho các Qubit đó là sử dụng quả cầu Bloch. Quả cầu Bloch là một quả cầu có bán kính đơn vị. Nó được sử dụng để biểu diễn Qubit một cách trực quan. 


<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791295492/6f392783-0c8c-454a-b60c-64520a849698.png" alt="">
</div>


Lúc này, vị trí của các Qubit được xác định rõ ràng thông qua các tham số $\theta$ và $\varphi$

Quả cầu này còn có ý nghĩa biểu diễn cho các cổng lượng tử có vai trò thực hiện phép quay mà ta sẽ tìm hiểu ở phần sau. 


$$
\displaystyle \ket{\psi } =\alpha \ket{0} +\beta \ket{1} =\cos\left(\frac{\theta }{2}\right)\ket{0} +e^{i\varphi }\sin\left(\frac{\theta }{2}\right)\ket{1}
$$
### Tích nội và không gian Hilbert 


### Ma trận Hermitian và ma trận Unita 

### Tích tensor

Ở trên ta đã mô tả cách sử dụng tích Tensor để biểu diễn nhiều hơn 1 qubit. Tích Tensor còn có một vai trò khác đó chính là kết hợp các không gian Hilbert lại với nhau


## Mạch lượng tử 

Một mạch lượng tử là một mô hình tính toán gồm các qubit và các cổng lượng tử được kết nối với nhau để thực hiện các thao tác tính toán. Ta sẽ dùng các mạch lượng tử này để mô tả các thuật toán lượng tử.

Trước tiên ta cần phải hiểu thế nào là một cổng lượng tử. Một cổng lượng tử có thể được xem là một toán tử hoạt động trên các qubit.


Ta đã quen thuộc với khái niệm về toán tử tuyến tính. Cụ thể, một toán tử tuyến tính giữa hai không gian vector $\displaystyle V$ và $\displaystyle W$ là một ánh xạ $\displaystyle A:V\rightarrow W$ nếu như nó tuyến tính trên các đầu vào. Cụ thể 

$$
\begin{equation*}
A\left(\sum _{i} a_{i}\ket{v_{i}}\right) =\sum _{i} a_{i} A\left(\ket{v_{i}}\right)
\end{equation*}
$$

Các cổng lượng tử có thể được hiểu như là các toán tử và các toán tử này sẽ được biểu diễn dưới dạng ma trận. Bây giờ ta sẽ xem xét một số cổng lượng tử trên một qubit đơn lẻ (single qubit operations)



Để chỉ một cổng lượng tử tác động lên một dây qubit ta có hình vẽ sau 

<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791296945/e073b7fb-b115-497a-ae90-f144aeb80f5e.png" alt="">
</div>

Với $n$ dây thì ta sẽ có: 

<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791297071/d6f0b7db-c8aa-45a4-981e-662e9a185299.png" alt="">
</div>

Kí hiệu sau để chỉ việc đo trạng thái một qubit $q$ và ghi kết quả vào kênh cổ điển $c$:


<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791297139/3f166142-1bf5-4b21-94f5-af1f9b595ceb.png" alt="">
</div>

và tương tự với $n$ qubit:


<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791297174/b16ecd84-0bda-4b8b-a8f6-f22b0e5b14da.png" alt="">
</div>


Khi thực hiện các thao tác trên một qubit thì ta cần đảm bảo độ dài của nó không được thay đổi, tức là giá trị $\displaystyle |\alpha |^{2} +|\beta |^{2} =1$ vẫn được giữ nguyên. Do đó ta cần các ma trận đại diện cho toán tử tác động lên qubit phải là một ma trận đơn nhất. 

3 cổng lượng tử quan trọng có thể kể đến đó là $\displaystyle X,Y,Z$ cụ thể như sau 

$$
\begin{equation*}
X=\begin{pmatrix}
0 & 1\\
1 & 0
\end{pmatrix} ,Y=\begin{pmatrix}
0 & -i\\
i & i
\end{pmatrix} ,Z=\begin{pmatrix}
1 & 0\\
0 & -1
\end{pmatrix}
\end{equation*}
$$

### Cổng pha 

Cổng pha (phase gate) là một cổng lượng tử có tác dụng xoay trạng thái lượng tử của qubit xung quanh trục $\displaystyle Z$ trên mặt cầu Bloch. 
$$
\begin{equation*}
P( \phi ) =\begin{pmatrix}
1 & 0\\
0 & e^{i\phi }
\end{pmatrix} ,\phi \in \mathbb{R}
\end{equation*}
$$

Tương tự ta có cổng $\displaystyle S$ và cổng $\displaystyle T$ như sau: 
$$
\begin{equation*}
S=P\left(\frac{\pi }{2}\right) =\sqrt{Z} =\begin{pmatrix}
1 & 0\\
0 & e^{\frac{i\pi }{2}}
\end{pmatrix} ,S^{\dagger } =\begin{pmatrix}
1 & 0\\
0 & e^{-\frac{i\pi }{2}}
\end{pmatrix}
\end{equation*}
$$

Và ta có 
$$
\begin{equation*}
SS\ket{\psi } =Z\ket{\psi }
\end{equation*}
$$
Đối với cổng $\displaystyle T$ thì nó sẽ là 

$$
\begin{equation*}
T=P\left(\frac{\pi }{4}\right) =\sqrt[4]{Z} =\sqrt{S}
\end{equation*}
$$

Ta có cổng Hadamard $\displaystyle H$ với biểu diễn 

$$
\begin{equation*}
H=\frac{1}{\sqrt{2}}\begin{pmatrix}
1 & 1\\
1 & -1
\end{pmatrix}
\end{equation*}
$$

Cổng Hadamard có hai tính chất đặc biệt. Tính chất đầu tiên của nó chính là đưa một trong hai trạng thái qubit cơ bản về trạng thái chồng chập. Cụ thể 

$$
\begin{gather*}
H\ket{0} =\frac{1}{\sqrt{2}}\left(\ket{0} +\ket{1}\right) =\ket{+}\\
H\ket{1} =\frac{1}{\sqrt{2}}\left(\ket{0} -\ket{1}\right) =\ket{-}
\end{gather*}
$$

Nó còn một tính chất khác đó là $\displaystyle H=\frac{X+Z}{\sqrt{2}}$. Ta có thể kiểm chứng bằng tính toán đơn giản như sau 

$$
\begin{equation*}
X+Z=\begin{pmatrix}
0 & 1\\
1 & 0
\end{pmatrix} +\begin{pmatrix}
1 & 0\\
0 & -1
\end{pmatrix} =\begin{pmatrix}
1 & 1\\
1 & -1
\end{pmatrix}
\end{equation*}
$$

### Cổng quay có tham số 

Parameterized gate hay còn gọi là cổng quay có tham số là một cổng cho phép ta quay một góc $\theta \in [0,2\pi]$ quanh một trong ba trục $\displaystyle X,Y,Z$ trên mặt cầu Bloch. Để biểu diễn các cổng này thì ta cần một tính chất nhỏ như sau

**Định lý.** Cho $\displaystyle x\in \mathbb{R}$ và một ma trận $\displaystyle A$ thỏa mãn $\displaystyle A^{2} =I$. Chứng minh rằng 

$$
\begin{equation*}
e^{ixA} =\cos xI+i\sin xA
\end{equation*}
$$

Ta có thể chứng minh bằng khai triển Taylor như sau: 
$$
\begin{gather*}
e^{z} =\sum _{n=0}^{\infty }\frac{z^{n}}{n!} =1+z+\frac{z^{2}}{2!} +...\\
\Longrightarrow e^{ixA} =I+( ixA) +\frac{( ixA)^{2}}{2!} +...\\
=1+ixA-\frac{x^{2}}{2!} I-i\frac{x^{3}}{3!} A+\frac{x^{4}}{4!} I+...\\
=I\left( 1-\frac{x^{2}}{2!} +\frac{x^{4}}{4!} -...\right) +iA\left( x-\frac{x^{3}}{3!} +\frac{x^{5}}{5!} -...\right)
\end{gather*}
$$
Mà ta có 
$$
\begin{gather*}
\cos( x) =1-\frac{x^{2}}{2!} +\frac{x^{4}}{4!} -...\\
\sin( x) =x-\frac{x^{3}}{3!} +\frac{x^{5}}{5!} -...
\end{gather*}
$$
Cho nên 
$$
\begin{equation*}
e^{ixA} =\cos xI+i\sin xA
\end{equation*}
$$
Bây giờ ta có các cổng $\displaystyle R_{x}( \theta ) ,R_{y}( \theta ) ,R_{z}( \theta )$ có dạng như sau 
$$
\begin{gather*}
R_{x}( \theta ) =e^{\frac{-i\theta X}{2}} =\cos\frac{\theta }{2} I-i\sin\frac{\theta }{2} X=\begin{pmatrix}
\cos\left(\frac{\theta }{2}\right) & -i\sin\left(\frac{\theta }{2}\right)\\
-i\sin (\frac{\theta }{2}) & \cos\left(\frac{\theta }{2}\right)
\end{pmatrix}\\
R_{y}( \theta ) =e^{\frac{-i\theta Y}{2}} =...\\
R_{z}( \theta ) =e^{\frac{-i\theta Z}{2}} =...
\end{gather*}
$$

Ta có tính chất $\displaystyle XYX=-Y$ và từ đây có được $\displaystyle XR_{y}( \theta ) X=R_{y}( -\theta )$



Tổng quát hơn ta có cổng $\displaystyle U$ được gọi là cổng lượng tử phổ dụng (universal gate). Cụ thể 
$$
\begin{equation*}
U( \theta ,\phi ,\lambda ) =\begin{pmatrix}
\cos\frac{\theta }{2} & -e^{i\lambda }\sin\frac{\theta }{2}\\
e^{i\phi }\sin\frac{\theta }{2} & e^{i( \lambda +\phi )}\cos\frac{\theta }{2}
\end{pmatrix}
\end{equation*}
$$

Ta có thể phân rã $\displaystyle U$ ra thành các cổng $\displaystyle R_{x} ,R_{y} ,R_{z}$ nhưng phần đó ta tạm thời chưa nhắc đến ở đây. 

### CNOT 


Tiếp theo ta nói về cổng CNOT. CNOT là viết tắt của Controlled-NOT. Cổng này sẽ nhận vào 2 qubit, lần lượt là control qubit và target qubit và ta có thể biểu diễn tác động của nó dưới dạng $\displaystyle \ket{c}\ket{t}\rightarrow \ket{c}\ket{t\oplus c}$. Như vậy, nếu control qubit là $\displaystyle \ket{1}$ thì ta sẽ đổi trạng thái của target qubit, còn ngược lại thì không. 


ổng CNOT có một chút khác biệt so với các cổng mà ta đã giới thiệu ở trên đó chính là nó tác động lên 2 qubit chứ không còn là 1 qubit nữa. Vậy thì ta phải làm thế nào để biểu diễn ma trận toán tử của nó? Câu trả lời đó chính là ta sẽ sử dụng tích Tensor. 



Quan sát cổng lượng tử CNOT ở hình dưới đây, ta thấy có 2 dây nối, dây ở trên sẽ nối vào qubit điều khiển còn dây ở dưới sẽ nối vào target qubit. Phép đổi trạng thái qubit tương đương với việc áp dụng cổng $\displaystyle X$ vào qubit đó vì ta có tính chất $\displaystyle X\ket{0} =\ket{1}$ và $\displaystyle X\ket{1} =\ket{0}$. 


<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791299443/2630d4af-f33d-4978-af43-64293c8fffca.png" alt="">
</div>


Nếu như control qubit là $\displaystyle \ket{0}$ thì trạng thái được giữ nguyên, tức là ta đang áp dụng toán tử $\displaystyle I$ lên target qubit. Nó tương đương với việc viết $\displaystyle \ket{0}\bra{0} \otimes I$. Và nếu control qubit là $\displaystyle \ket{1}$ thì kết quả sẽ là $\displaystyle \ket{1}\bra{1} \otimes X$. Ở đây $\displaystyle \ket{\psi }\bra{\psi }$ được gọi là toán tử chiếu lên không gian sinh bởi $\displaystyle \ket{\psi }$. Ta có thể hiểu rằng nếu như control qubit nằm trong không gian con sinh bởi $\displaystyle \ket{0}$ thì target qubit sẽ được tác động bởi cộng $\displaystyle I$ và ngược lại. Không gian con ở đây là ta đang xét tổng quát cho $\displaystyle \text{span}\left\{\ket{\psi }\right\}$

Như vậy cổng CNOT có dạng ma trận là 
$$
\begin{gather*}
CX=\ket{0}\bra{0} \otimes I+\ket{1}\bra{1} \otimes X\\
=\begin{pmatrix}
I & 0\\
0 & X
\end{pmatrix} =\begin{pmatrix}
1 & 0 & 0 & 0\\
0 & 1 & 0 & 0\\
0 & 0 & 0 & 1\\
0 & 0 & 1 & 0
\end{pmatrix}
\end{gather*}
$$
Đây cũng là cách ma ta sẽ dùng để biểu diễn một số cổng lượng tử cho $\displaystyle n$ qubit khác nhau. 



Ta sẽ đi từ cổng đơn qubit trước. 




<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791300669/a0f4baa1-1ea9-49ca-80b3-1ee7abb56456.png" alt="">
</div>

Xem hình ở trên ta nắm được một số ý chính như sau: Trong biểu diễn cổng lượng tử, cổng nào tác động trước thì sẽ được đặt ở trước, chẳng hạn như trong hình ta có hai cổng $X,H$. Tuy nhiên khi thực hiện phép nhân ma trận thì ta thực hiện từ phải sang trái cho nên ta phải viết nó dưới dạng $HX\ket{\psi }$.

Tiếp theo với cổng tác động lên $n$ qubit



<div style="text-align: center;">
    <img src="https://res.cloudinary.com/yfrc4n5u/image/upload/v1791301101/6de188ec-dd51-4742-bc46-5875c38ecf5b.png" alt="">
</div>

Giải thích: Ở cổng đầu tiên ta thì ta thấy rằng, dây đầu tiên tác động lên qubit $\displaystyle \ket{0}$ bằng cổng $\displaystyle H$ cho nên trạng thái của nó sẽ là $\displaystyle H_{0}\ket{0}$. Ở dây còn lại thì sẽ là $\displaystyle X_{1}\ket{0}$. Ta muốn kết hợp cả hai trạng thái này thì công cụ cần dùng sẽ là tích Tensor $\displaystyle H_{0}\ket{0} \otimes X_{1}\ket{0}$. Trong trường hợp dây nối với qubit không có cổng nào tác động lên thì ta sẽ sử dụng toán tử $\displaystyle I$. 

