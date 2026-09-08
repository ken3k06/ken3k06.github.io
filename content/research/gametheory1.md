+++
date = '2026-09-08T15:55:04+07:00'
title = 'Some notes on game theory - Part 1'
toc = true
math = true 
+++

<style>
table {
    border-collapse: collapse;
}

th, td {
    border: 1px solid #888;
    padding: 8px;
}
</style>

Tham khảo và viết lại từ cuốn Lý thuyết trò chơi của thầy Tạ Quang Sơn

## Ra quyết định
Lý thuyết trò chơi liên quan rất nhiều tới việc ra quyết định. Vì vậy ta hãy cùng xem qua một số ví dụ sau đây để hiểu rõ về việc ra quyết định.

                                                                                                                                                                                                                                                                                                                                                                                                                              
Ví dụ 1: Có một khách du lịch muốn đi thăm một vùng quê, nơi  này gồm nhiều ngôi làng của thổ dân sinh sống. Chiếc xe khách chở anh ta sẽ lần lượt đi qua các ngôi làng và anh ta mong muốn dừng chân tại một ngôi làng đẹp nhất. Tại mỗi ngôi làng, chiếc xe dừng lại ở đầu làng và trả khách và lại tiếp tục hành trình. 

Vậy nếu bạn là người khách du lịch này thì bạn sẽ đưa ra quyết định như thế nào? Biết rằng, việc giao tiếp với thổ dân là không khả thi, và ra hiệu bằng hành động thì không đủ để diễn tả điều mình cần nói. 

Chiếc xe sẽ tiếp tục di chuyển cho tới khi dừng lại ở ngôi làng cuối cùng và tới lúc đó ta buộc phải đưa ra lựa chọn xuống xe. Không có gì đảm bảo ngôi làng cuối cùng là ngôi làng đẹp nhất cả, cho nên ta có thể chuyển sang lựa chọn việc xuống xe tại một ngôi làng bất kì trên đường. Tuy nhiên ta lại bị giới hạn thông tin nên không thể thực hiện so sánh giữa các ngôi làng được. 

Hơn nữa, kể cả khi ta giới hạn thông tin lại ở việc chỉ đánh giá cổng làng, thì ta cũng không thể thực hiện so sánh vì xe sẽ cứ chạy như vậy. 

Cuối cùng ta buộc phải đưa ra quyết định xuống xe dựa vào may rủi. 


Ở ví dụ này, quyết định của người khách là quyết định độc lập, tức là nó chỉ ảnh hưởng đến đúng một người duy nhất là anh ta. Quyết định này cũng hoàn toàn phụ thuộc vào cá nhân anh và không có một bên khác đối kháng lại với quyết định mà anh ấy đưa ra. 


Bây giờ ta sẽ xem xét một ví dụ khác mà tại đó quyết định đưa ra có sự cạnh tranh

Ví dụ 2: Có hai anh A và B cùng ra quyết định đầu tư, mỗi người đều có 10 tỉ trong tay. Cả hai có hai lựa chọn đầu tư. Lựa chọn đầu tiên là mua trái phiếu chính phủ với lợi nhuận hàng năm là $10\%$ hoặc là đầu tư vào bất động sản. Đầu tư vào bất động sản sẽ có rủi ro, đòi hỏi phải có 20 tỷ thì mới có triển vọng thành công với lợi nhuận $20\%$ năm. Còn nếu đầu tư dưới 20 tỷ thì chắc chắn sẽ thất bại. 

Vấn đề ở đây là hai anh A và B hoàn toàn không quen biết nhau nên không thể đưa ra quyết định bàn bạc hợp tác. 

Như vậy sẽ có những trường hợp như dưới đây: 

- Nếu anh A quyết định mua trái phiếu còn B quyết định đầu tư bất động sản thì A sẽ được 11 tỉ trong khi B sẽ không được gì. 
- Nếu cả A và B cùng đầu tư trái phiếu thì mỗi người sẽ nhận được 11 tỉ
- Nếu cả hai cùng đầu tư bất động sản thì mỗi người được 12 tỉ. 

Các số liệu đầu tư này có thể được mô tả bởi một song ma trận như sau:





| | B-TP | B-BDS |
| :--- | :---: | :---: |
| **A-TP** | (11, 11) | (11, 10) |
| **A-BDS** | (10, 11) | (12,12) |

Trong đó TP = Trái phiếu còn BDS = Bất động sản

Nhận xét: 
- Bất cứ quyết định nào của ngừoi này cũng có thể ảnh hưởng đến người kia
- Mặc dù người này biết tất cả các dự định của người kia nhưng không biết được sự lựa chọn của người kia.
- Các quyết định được đưa ra có thể dẫn tới tình trạng đối kháng.


Tóm lại, lý thuyết trò chơi có thể được hiểu là sự nghiên cứu các mô hình toán học dạng đối kháng và hợp tác giữa những người ra quyết định thông minh và có trách nhiệm. Lí thuyết trò chơi cung cấp cho ta các công cụ toán học để phân tích tình huống giữa hai hay nhiều người chơi khhi đưa ra các quyết định, mà quyết định của người chơi này có thể ảnh hưởng đến lợi ích của người chơi khác. 

Để nghiên cứu về lý thuyết trò chơi, ta cần phải có một quy tắc nhận biết về mặt toán học dành cho các trò chơi, để phân biệt nó với ý nghĩa của các trò chơi thông thường. 

Các quy tắc đó bao gồm: 

1. Luật chơi phải rõ ràng và được thực hiện nghiêm túc khi chơi
2. Có kết quả thưởng phạt (thu hoạch) đầy đủ đối với người chơi.
3. Có chứa yếu tố bất ngờ đối với kết quả (lưu ý đối với một số dạng trò chơi như trò chơi tổ hợp thì kết quả thường không mang tính ngẫu nhiên này, chẳng hạn như trò chơi Nim, hoặc cờ vua)
4. Các quyết định trong khi chơi là rõ ràng
5. Không có yếu tố gian lận
6. Có ít nhất hai người tham gia trò chơi

## Các khái niệm

Trò chơi (**game**) là thuật ngữ dùng để mô tả sự kiện có **tính đối kháng hoặc cạnh tranh** giữa những người tham gia sự kiện và mỗi người đều có quyết định đúng đắn. Một trò chơi phải hội tụ đủ các quy tắc được nêu ở trên



Một chiến lược cân bằng hay chiến lược tối ưu (**equilibrium strategy**) là một chiến lược mà mỗi người chơi đều nhận được thu hoạch tốt nhất đối với họ, tức là người chơi hài lòng nhất đối với thu hoạch mà mình nhận được so với tất cả các lựa chọn khác

Thu hoạch hay điểm thưởng phạt (**payoff**) ở đây dùng để đo lường mức độ hoàn hảo của người chơi trong việc tính thu hoạch trong khi chơi. Ứng với một bộ chiến lược được thực hiện của người chơi, mỗi người chơi sẽ nhận được điểm thưởng phạt cho riêng mình. 

Chiến lược (**strategy**) ở đây là một tập hợp các quyết định (**decision**) lựa chọn giữa tất cả các người chơi (**player**). Mỗi người chơi sẽ tiến hành chơi trò chơi (**play**) và đưa ra các quyết định có lợi hoặc không có lợi cho mình. 

## Các loại trò chơi


### Trò chơi hợp tác và trò chơi không hợp tác 

Trò chơi hợp tác (cooperative game) là trò chơi mà người chơi được phép chia sẻ thông tin, chia sẻ mọi giao kèo để thực hiện trò chơi như đã xác định bởi các chiến lược được chọn. Trò chơi không hợp tác (noncooperative games) là ngược lại. 


Ta đều ít nhiều từng nghe qua cái tên song đề tù nhân. Vậy rốt cuộc song đề tù nhân là gì?

Song đề tù nhân là một dạng của trò chơi không hợp tác được phát biểu như sau:

Có hai người bị tình nghi liên quan đến một vụ án nghiêm trọng và bị cảnh sát bắt giam vào hai buồng giam riêng biệt để lấy lời khai. Hình phạt đối với các nghi phạm phụ thuộc vào việc họ có nhận tội hay không. Mỗi nghi phạm chỉ có hai lựa chọn hoặc là nhận tội hoặc là không. Lúc này sẽ có ba trường hợp

- Nếu cả hai cùng nhận tội thì mỗi người sẽ chỉ phải ngồi tù 1 năm
- Nếu cả hai cùng chối thì sẽ cùng phải ngồi tù 2 năm
- Nếu một người chối, người còn lại nhận tội thì người nhận tội được trả tự do và người không kia sẽ phải ngồi tù 3 năm.

Vì điều kiện giam giữ nên cả hai không thể liên lạc với nhau để thảo luận phương án chung. 

Ma trận thu hoạch có dạng

| | B-KNT | B-NT |
| :--- | :---: | :---: |
| **A-KNT** | (1, 1) | (3, 0) |
| **A-NT** | (0, 3) | (2,2) |

Trong đó KNT = Không nhận tội và NT = Nhận tội


**Nhận xét:** Cả hai người tù đều muốn giành thuận lợi cho mình, bất chấp tình trạng của người kia. Kể cả khi cả hai đã thảo luận với nhau thì không có gì đảm bảo họ sẽ tin tưởng nhau. Ai cũng muốn nhận tội để được tự do. Nhưng nếu theo quán tính như vậy thì sẽ dễ rơi vào trường hợp cả hai cùng nhận tội và nhận án phạt 2 năm. Nếu một người thành thật khai báo và nhận tội thì không có gì đảm bảo người kia sẽ như vậy và có thể khiến bản thân nhận án phạt 3 năm. Cả hai đều không nhận tội có lẽ là phương án tốt nhất, tuy nhiên trên thực tế thì điều này trái với phản ứng thông thường khi bị phạt. 


![](https://res.cloudinary.com/yfrc4n5u/image/upload/v1788857899/73743c03-a8f4-482d-a7cd-2141664128b9.png)


Các phiên bản khác của trò chơi "Song đề tù nhân" sau này mà ta sẽ nghiên cứu thường được thực hiện với ma trận thu hoạch có dạng tổng quát:

| | $B-H_1$ | $B-H_2$ |
| :--- | :---: | :---: |
| $A-H1$ | $(b,b)$ | $(d,a)$ |
| $A-H2$ | $(a,d)$ | $(c,c)$ |

trong đó $a < b < c < d$

### Trò chơi có tổng thu hoạch bằng hằng số

Trò chơi mà tại đó tổng điểm thu hoạch của hai người chơi luôn là một hằng số được gọi là trò chơi có tổng bằng hằng số (LOL), thuật ngữ tiếng anh là Constant-sum games. Tương tự ta sẽ có Zero-sum games là trò chơi có tổng bằng không. 

Ví dụ: Có hai người chơi A và B chơi trò đặt đồng xu. Luật chơi như sau: MỖi người lấy trong túi ra một đồng xu có hai mặt sấp và ngửa đã được quy ước từ trước và chọn mặt để đặt lên bàn cùng lúc. Nếu cả hai đồng xu cùng sấp hay cùng ngửa thì A thắng, A lấy đồng xu của B, lúc này A sẽ +1 còn B sẽ là -1. Còn nếu có một mặt sấp một mặt ngửa thì B thắng và B sẽ lấy một đồng xu của A, ma trận thu hoạch sẽ có dạng

| | $B-S$ | $B-N$ |
| :--- | :---: | :---: |
| $A-S$ | $(+1,-1)$ | $(-1,+1)$ |
| $A-N$ | $(-1,+1)$ | $(+1,-1)$ |

Đây là trò chơi có tổng bằng không.





### Trò chơi có thông tin hoàn hảo và không hoàn hảo

Trò chơi có thông tin hoàn hảo (perfect information game) là một tò chơi mà mỗi người chơi đều biết các nước đi của các người chơi khác đã thực hiện. Trò chơi tuần tự là trò chơi có tính chất thông tin hoàn hảo. Đa số các trò chơi được nghiên cứu đều là trò chơi có thông tin không hoàn hảo. 

Ta cần phân biệt rõ trò chơi có thông tin hoàn hảo với trò chơi có thông tin đầy đủ (complete information game) .

Trò chơi có thông tin đầy đủ là dạng trò chơi mà mọi người chơi đều biết đầy đủ tập hợp các nước đi của đối phương với các thu hoạch, tuy nhiên chỉ không biết đối phương chọn nước nào. Một ví dụ cho trò chơi có thông tin đầy đủ là song đề tù nhân kể trên. Ta biết được các nước đối phương có thể chọn cùng với thu hoạch tuy nhiên ta không thể biết đối phương chọn nước nào cho tới cuối trò chơi.

Còn về trò chơi có thông tin hoàn hảo chẳng hạn như cờ vua hoặc cờ caro. Một bên sẽ đưa ra quyết định trước và bên còn lại sẽ cân nhắc để đưa ra lựa chọn của mình. 



### Trò chơi đồng thời và trò chơi tuần tự 

Căn cứ vào thời điểm ra quyết định, ta có hai loại trò chơi là loại đồng thời và loại tuần tự.

Trò chơi đồng thời (simultaneous game): Cả hai người chơi sẽ thực hiện các nước đi một cách đồng thời hoặc khi thực hiện nước đi, các người chơi không biết về hành động của đối thủ. Trò chơi loại này còn gọi là trò chơi có chiến lược chuẩn (strategic form game, normal form game) 

Ngược lại với trò chơi đồng thời ta sẽ có trò chơi tuần tự (sequential game): Trong trò chơi tuần tự, sau nước đi của người này mới đến nước đi của người khác. Chẳng hạn như cờ vua là một dạng trò chơi tuần tự. Người đi sau lúc này có thể biết trước một số thông tin của người đi trước. Trò chơi loại này còn gọi là trò chơi có chiến lược chuẩn mở rộng (extensive form game).

### Trò chơi thuần túy và trò chơi hỗn hợp

Một trò chơi được gọi là trò chơi có chiến lược thuần tùy (pure strategy) nếu các nước đi được quyết định hoàn toàn do ý thức của người chơi và quyết định đó thuộc tập hợp các quyết định đã có. Nếu việc lựa chọn các nước đó có sự can thiệp của yếu tố ngẫu nhiên thì ta gọi đó là trò chơi có chiến lược hỗn hợp (mixed strategy).

Lấy ví dụ trò chơi tung đồng xu ở trên, chỉ khác ở đây hai người chơi sẽ lấy đồng xu ra và tung lên để rơi xuống đất. Lúc này bản thu hoạch sẽ được giữ nguyên tuy nhiên các nước đi lúc này sẽ phụ thuộc vào yếu tố ngẫu nhiên. 

### Trò chơi một ván và trò chơi lặp lại

Trò chơi một ván (one-shot game) là loại trò chơi mà trong đó mỗi người chơi chỉ có một lần ra quyết định. Trò chơi có nhiều hơn một ván được gọi là trò chơi lặp lại. Ta gọi là trò chơi lặp lại bậc $n$ nếu số lần lặp lại $n>1$. 

Ví dụ: đá phạt là trò chơi một ván, thủ môn và người đá phạt đền chỉ thực hiện cản phá và sút một lần duy nhất. Còn đá luân lưu là trò chơi lặp lại. 


### Trò chơi tĩnh và trò chơi động

Trong các trò chơi nêu trên, có những trò chơi mà quyết định được đưa ra đồng thời. Các trò chơi như thế được gọi là trò chơi tĩnh (static game).

Trò chơi đồng thời và trò chơi tĩnh khác nhau ở đâu? 

Thực ra hai thuật ngữ này đều được dùng để chỉ chung một mô hình trò chơi. Còn vì sao có hai cái tên khác nhau thì do tác giả thích vậy.


Đối với trò chơi động (dynamic games), ta đang nói đến các trò chơi mà tại đó quyết định được đưa ra ở các thời điểm khác nhau. Thông thường, một  người chơi đưa ra quyết định, rồi người khác mới cân nhắc để đưa ra quyết định đối ứng. 

## Mô tả trò chơi

Ở phần cuối của bài viết này, ta sẽ phân tích một số cách để mô tả trò chơi. 

Đối với trò chơi hai người thông thường ta sẽ sử dụng song ma trận để chỉ thu hoạch của các bên. Nếu như thu hoạch của người chơi này bằng đúng thiệt hại của người chơi kia thì ta có thể sử dụng đơn ma trận. Ngoài ra nếu là trò chơi động, trò chơi tuần tự thì ta sẽ mô tả dưới dạng sơ đồ cây. 

### Ma trận

Có hai dạng là song ma trận và đơn ma trận


Giả sử có hai người cùng tham gia trò chơi. Người thứ I với tập hợp các quyết định $\displaystyle A$ có $\displaystyle m$ phần tử, người thứ II với tập hợp các quyết định B có $\displaystyle n$ phần tử. Không gian chiến lược tương ứng là 

\begin{equation*}
A\times B=\{( a_{i} ,b_{j}) \ |\ a_{i} \in A,b_{j} \in B,i=\overline{1,m} ,j=\overline{1,n}\}
\end{equation*}


Hàm thu hoạch của từng người chơi là $\displaystyle U_{i} :A\times B\rightarrow \mathbb{R} ,i=1,2$. Khi đó ma trận thu hoạch có dạng 

$$
\begin{equation*}
\begin{array}{ c|c c c }
 & b_{1} & \dotsc  & b_{n}\\
\hline
a_{1} & ( U_{1}( a_{1} ,b_{1}) ,U_{2}( a_{2} ,b_{2})) & \dotsc  & ( U_{1}( a_{1} ,b_{n}) ,U_{2}( a_{1} ,b_{n}))\\
\vdots  & \vdots  &  & \vdots \\
a_{m} & ( U_{1}( a_{m} ,b_{1}) ,U_{1}( a_{m} ,b_{2})) & \dotsc  & ( U_{1}( a_{m} ,b_{n}) ,U_{2}( a_{m} ,b_{n}))
\end{array}
\end{equation*}
$$

Đây là song ma trận.

Trong trường hợp $\displaystyle U_{2}( a_{i} ,b_{j}) =-U_{1}( a_{i} ,b_{j})$ với mọi $\displaystyle i=1,...,m$ và $\displaystyle j=1,...,n$ thì chỉ cần dùng đơn ma trận tính cho người thứ $\displaystyle I$ với thu hoạch $\displaystyle U_{1}$





$$
\begin{equation*}
\begin{array}{ c|c c c }
 & b_{1} & \dotsc  & b_{n}\\
\hline
a_{1} & U_{1}( a_{1} ,b_{1}) & \dotsc  & U_{1}( a_{1} ,b_{n})\\
\vdots  & \vdots  &  & \vdots \\
a_{m} & U_{1}( a_{m} ,b_{1}) & \dotsc  & U_{1}( a_{m} ,b_{n})
\end{array}
\end{equation*}
$$


### Cây trò chơi

Cây trò chơi được dùng để miêu tả trò chơi tuần tự, khi người chơi sau có thể cân nhắc đưa ra quyết định dựa vào quyết định của người đi trước. 

![](https://res.cloudinary.com/yfrc4n5u/image/upload/v1788858426/6b016d11-da6b-473e-b584-a3e9caba26b4.png)

Bài viết xin được kết thúc tại đây

Lý thuyết trò chơi còn có một số ứng dụng trong mật mã học, chẳng hạn như trong multi-party computation (rational cryptography/protocol) . Trong tương lai, tác giả sẽ cập nhật một số bài viết về chủ đề này. 