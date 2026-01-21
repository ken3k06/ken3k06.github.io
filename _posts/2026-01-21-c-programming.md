---
layout: post
category: misc 
---

Trước khi đọc bài này thì mọi người nên có một số kiến thức cơ bản về một ngôn ngữ lập trình cụ thể, ví dụ C++/Python vì mình sẽ đi nhanh lại các khái niệm cơ bản để tránh lan man quá. 

* This will become a table of contents (this text will be scrapped).
{:toc}

# Mở đầu
Import thư viện bằng `#include`. Trong C có các thư viện có sẵn như [`stdio.h`](https://www.ibm.com/docs/en/zos/3.1.0?topic=files-stdioh-standard-input-output) cung cấp các hàm để hỗ trợ việc nhập xuất. 

Hàm main là nơi chương trình bắt đầu được thực thi. Các câu lệnh được ngăn cách nhau bởi dấu chấm phẩy `;`. Đối với C thì nó sẽ bỏ qua khoảng trắng trong code. Cho nên ta đặt dấu `;` ở đâu cũng được miễn là nó nằm sau mỗi câu lệnh. 

Ví dụ ta có một chương trình C hello world như sau: 


```c
#include <stdio.h>
int main(){
    printf("Hello World\n");
    return 0;
}
```


Để chạy code C thì ta cần sử dụng trình biên dịch. Trình biên dịch (compiler) là phần mềm biên dịch từ mã nguồn thành các chuỗi bit. Với C thì ta sử dụng trình biên dịch GNU. 

Quá trình biên dịch sẽ diễn ra như sau:
    
![image](https://hackmd.io/_uploads/rkFJNdwg-l.png)


Bộ tiền xử lý (pre-processor) sẽ lấy bản sao của tệp mã nguồn (source file *.c) nằm tại thư mục hiện hành và sao chép nội dung của các tệp tiêu đề (header file *.h) nằm tại `/usr/include` vào bản sao ấy.  

Trình biên dịch (compiler) sau đó sẽ biên dịch bản sao này thành một chương trình ở mức hợp ngữ (.asm) theo kiến trúc tập lệnh mà máy tính đang sử dụng. Sau đó, trình biên dịch hợp ngữ (Assembler) sẽ thông dịch chương trình ở mức hợp ngữ này thành  các tệp đối tượng (.o). Cuối cùng, trình liên kết (Linker) sẽ liên  kết các tệp đối tượng và các thư viện (.a, .so, .sa) nằm tại `/usr/lib` hoặc `/lib` để tạo thành một chương trình ở mức nhị phân có thể thực thi được trên máy tính:


# Kiểu dữ liệu 
Trong C có các kiểu dữ liệu cơ bản như sau: 

![image](https://hackmd.io/_uploads/rk_fBdPxbe.png)

Mỗi loại dữ liệu sẽ có một đặc tả riêng để hàm `printf` nhận biết và in ra output. Ví dụ với `n=5` thì đặc tả bởi `%d`. 

```c 
printf("%d", n);
```

Ta cũng có thể gán kiểu dữ liệu cho một biến bằng cú pháp khai báo đơn giản là

```
data_type var_name;
```

Trong C cũng có những quy tắc đặt tên riêng như sau: 

- Không được đặt tên bắt đầu bằng chữ số. 
- Tên biến không được chứa dấu cách hoặc các ký tự đặc biệt
- Tên biến không được trùng với các keyword có sẵn trong C
- Không được đặt 2 biến cùng tên, kể cả chúng khác kiểu dữ liệu	
- Tên biến trong C có phân biệt chữ hoa và chữ thường

# Define và Typedef

## Typedef
Typedef giúp ta tạo một tên mới cho các kiểu dữ liệu trong ngôn ngữ C. 

Cú pháp là 
```c 
typedef data_type new_name; 
```

```c
#include <stdio.h>

typedef long long ll; 
int main(){
    ll x = 5; 
    printf("%lld", x); 
    return 0;
}
```

## Define
Define có 3 chức năng chính
- Định nghĩa tên cho kiểu dữ liệu 
- Định nghĩa tên cho giá trị 
- Định nghĩa tên cho cấu trúc hoặc câu lệnh 



Cách mà Define định nghĩa tên cho kiểu dữ liệu sẽ ngược lại so với typedef 

```c 
#define ten_moi kieu_du_lieu
```
Ví dụ
```c 
#include <stdio.h>

#define ll long long
int main(){
    ll x = 5; 
    printf("%lld", x); 
    return 0;
}
```

+ Định nghĩa tên cho các giá trị:

Ví dụ 

```c
#define PI 3.14 
#define INF 1000000000
#define TRUE 1
#define FALSE 0
```

Và cuối cùng là 
+ Định nghĩa tên cho cấu trúc và câu lệnh 

Ví dụ:
```c 
#include <stdio.h>


#define FOR(i,a,b) for(int i = a ; i <b ; i++)
#define greet printf("Hello world\n")


int main(){
    greet; 
    FOR(i,5,7){
        printf("%d", i ); 
    }
    return 0;
}
```


Khác nhau cơ bản giữa 2 lệnh này? 

Đầu tiên ta có thể thay rõ sự khác biệt trong cú pháp giữa 2 lệnh này. 
Tiếp theo ta cần biết rằng typedef sẽ được xử lý bởi trình biên dịch (compiler) còn define sẽ được xử lý bởi preprocessor. 

# Điều khiển luồng 

## if - else 

Cú pháp 
```c
if (điều kiện){
    // câu lệnh được thực thi nếu điều kiện đúng
}
```

Dùng chung với else để rẽ nhánh điều kiện:

```c
if (điều kiện){
    // đúng thì chạy 
}
else {
    // sai sẽ chạy
}
```

Và có thể lồng lại để chạy nhiều nhánh điều kiện
```c 
if (điều kiện){
    // đk 1 
}
else if (...){
    // đk 2 
}
else {
    // đk 3
}
```

## switch case

Tương tự như if-else, với đầu vào $n$ thì sẽ rẽ nhánh dựa trên các trường hợp có thể có của nó 

```c
int n = 2; 
switch(n){
    case 1: {
        // nếu n==1 thì thực thi lệnh trong khối lệnh này 
    }
    case 2: {
        // tương tự
    }
    default: {
        // trường hợp mặc định, nếu như n không là một trong các giá trị trên 
    }
}
```


Lưu ý là phải kết thúc mỗi khối lệnh bằng lệnh `break;` nếu không thì sẽ xảy ra một hiện tượng gọi là fall-through. Tức là sau khi chương trình thực thi lệnh của case đúng thì nó sẽ tiếp tục thực thi lệnh của các case sau và cho ta kết quả không mong muốn. 
```c
#include <stdio.h>
int main(){
    int n = 2; 
    switch(n){
        case 1: {
            printf("hello");
            break; 
        }
        case 2:{
            printf("good bye");
            break;
        }
        default:{
            printf("check thoi");
        }
    }

    return 0;
}
```

## goto 

Trong chương trình đôi khi bạn muốn bỏ qua 1 số câu lệnh hoặc quay lại một số câu lệnh khi đó bạn có thể gán nhãn cho vị trí các câu lệnh và sử dụng câu lệnh goto để chương trình tiến hành thực hiện các câu lệnh bắt đầu từ vị trí nhãn. 

```c
#include <stdio.h>
int main(){
    Lap: 
    int n;
    printf("Nhap n: ");
    scanf("%d",&n);
    if (n%2 ==0){
        printf("ok");
    }
    else{
        printf("not ok");
        goto Lap; 
    }
    return 0;
}
```
## For
For trong C thì cũng khá giống trong C++

```c 
for(Câu_lệnh_khởi_tạo ; Điều_kiện_lặp; Câu_lệnh_cập_nhật){
    //code
}
```
Lưu ý là điều kiện lặp và câu lệnh cập nhật có thể kiểm tra cũng như cập nhật nhiều biến. Câu lệnh khởi tạo cũng vậy, có thể khởi tạo nhiều biến cùng lúc, miễn là ngăn cách nhau bởi dấu `,`
```c 
#include <stdio.h>

int main() {
    int i, j;

    for(i = 0, j = 10; i < 5 && j > 5; i++, j--) {
        printf("i=%d, j=%d\n", i, j);
    }

    return 0;
}
```

## while-do và do-while

Khác biệt cơ bản của 2 lệnh này đó là:

Đối với while - do thì sẽ kiểm tra điều kiện trước rồi mới thực hiện khối lệnh
```c 
while (điều kiện){
    // do 
}
```

Còn do-while thì thực hiện khối lệnh trước rồi mới kiểm tra điều kiện 
```c 
do{
    // khối lệnh
}while(điều kiện)
```
Có thể dùng do-while để đóng gói lệnh khá hay vì với `while(0)` thì khối lệnh sẽ thực thi một lần duy nhất rồi dừng lại. 


# Khai báo nguyên mẫu hàm 
Khai báo nguyên mẫu hàm nhằm cung cấp các thông tin của hàm cho trình biên dịch bao gồm 

- Kiểu trả về của hàm
- Tên hàm
- Số lượng tham số của hàm
- Dánh sách kiểu dữ liệu của các tham số 

```c 
#include <stdio.h>
int tong(int, int ,int);

int tong(int a, int b, int c){
    int sum = a+b+c; 
    return sum; 
}
int main() {
    int i=1, j=2,k=3;
    printf("%d\n",tong(i,j,k)); 
    return 0;
}
```

Ngoài ra chương trình cũng sẽ gặp lỗi nếu như biên dịch hàm không đúng thứ tự. 
```c
#include <stdio.h>

void B(){
    printf("B");
    A();
}

void A(){
    printf("A");
}

int main(){
    B();
    return 0;
}
```


Sẽ gặp lỗi như sau:
```
warning: implicit declaration of function ‘A’ [-Wimplicit-function-declaration]

warning: conflicting types for ‘A’; have ‘void()’

note: previous implicit declaration of ‘A’ with type ‘void()’
```


Lỗi đầu tiên đó là ta khai báo hàm `B` trước khi khai báo hàm `A`. Như vậy thì compiler sẽ giả định kiểu trả về của hàm `A` là `int`, dẫn đến lỗi ở dòng tiếp theo là `conflicting types for A` : giữa 2 kiểu void và int 

Nếu sửa lại `int A()` ở sau thì chỉ còn lại lỗi `implicit declaration of function A`

![image](https://hackmd.io/_uploads/B1ch7v_gZe.png)


# Mảng 1 chiều

Trong C để khai báo mảng thì dùng cú pháp 
```
data_type list_name[number_of_elements]; 
```
Ví dụ mảng gồm 100 số nguyên:
```c 
int a[100];
```

Tiếp theo ta nói về các thao tác trên mảng. 

## Duyệt mảng

Duyệt bằng chỉ số

```c
#include <stdio.h>

int main(){
    int a[10] = {3, 2, 1, 4, 5, 8, 9, 7, 6, 10};
    int n = 10; 
    for(int i = 0 ; i<n;i++){
        printf("%d  ",a[i]); 
    }
    return 0;
}
```

## Nhập mảng 

```c 
#include <stdio.h>

int main(){
    int n; 
    scanf("%d",&n); 
    int a[n]; 
    for (int i = 0 ; i <n ;i++){
        printf("nhập phần tử %d\n  ", i+1); 
        scanf("%d", &a[i]); 
    }
    for (int i = 0 ; i < n ; i++){
        printf("%d\n", a[i]);
    }

    return 0;
}
```

Dùng tham chiếu `&` để thay đổi trực tiếp. 


## Xóa và chèn 



# Con trỏ và địa chỉ

Con trỏ hay biến con trỏ cũng là một biến thông thường nhưng giá trị mà nó lưu lại là địa chỉ của một biến khác 

Ví dụ biến kiểu int N trong chương trình sẽ có địa chỉ nhất định trong bộ nhớ, để lưu giá trị địa chỉ này ta cần biến con trỏ kiểu int 

Khi khai báo biến con trỏ ta thêm dấu * vào trước tên biến

Cú pháp khai báo: 

```nasm
data_type *pointer_name
```

```c
#include <stdio.h>
int main(){
	int *ptr; 
	long long *ptr2; 
	// ... 
	return 0;
	
}
```

Mỗi biến trong chương trình đều được cấp phát vùng nhớ để lưu trữ giá trị của nó, ví dụ biến int sẽ được cấp phát 4 byte liên tiếp để lưu trữ và lấy địa chỉ của byte đầu tiên làm địa chỉ cho biến? đây là biểu diễn theo kiểu little endian trong các kiến trúc như IA32 , Windows hay IOS đều xài kiểu biểu diễn dữ liệu này. 

Để in ra địa chỉ của biến ta dùng toán tử &N, 

Biến con trỏ int thì sẽ lưu được địa chỉ của biến int. 

Để gán địa chỉ của biến int N cho p thì ta sẽ làm như sau:

```c
int N = 1000;
int *ptr; 
ptr = &N; 
```

## Tham chiếu và giải tham chiếu 

Khi con trỏ ptr tham chiếu (reference) tới biến `N` thì thông qua con trỏ ptr ta có thể truy xuất cũng như thay đổi giá trị của biến `N` mà không cần dùng `N`.
Để truy xuất tới giá trị của biến mà con trỏ đang trỏ tới ta dùng toán tử giải tham chiếu `*` (dereference)
```c 
#include <stdio.h>
int main(){
    int N = 1000;
    int *ptr = &N;
    *ptr = 280;
    printf("%p\n", N); 
    return 0;
}
```
Ta cũng có thể khai báo nhiều con trỏ để trỏ tới cùng 1 biến 
```c 
int N = 1000;
int *ptr1 = &N;
int *ptr2 = &N;
...
```

## Hàm và con trỏ 

Có hai cách để truyền giá trị vào trong hàm. Một là truyền tham trị pass-by-reference. Trong C thì không có kiểu truyền tham chiếu như trong C++. Truyền tham trị là giá trị của đối số sẽ được gán cho tham số khi lời gọi hàm được thực hiện. Chẳng hạn 
```c
#include <stdio.h>
int foo(int n){
    int sum = n+100;
    return sum;
}
int main(){
    int N = 1000;
    int res = foo(N);
    printf("%p\n", res); 
    printf("%p\n",N); 
    return 0;
}
```
Khi truyền tham trị như vậy thì giá trị của `N` sẽ không thay đổi sau khi ta thực hiện lệnh gọi hàm.

Để thay đổi giá trị của `N` sau khi gọi hàm thì ta sẽ dùng biến con trỏ. 
```c
#include <stdio.h>


void foo(int *x){
    *x = 999; 
}
int main(){
    int N = 1000;
    foo(&N); 
    printf("%p\n",N); 
    return 0;
}
```

Hàm void khai báo với tham số đầu vào là một biến con trỏ , ta truyền vào đó địa chỉ của N thì giá trị của N sẽ được thay đổi trực tiếp sau khi ra khỏi hàm.

## Con trỏ cấp 2
Con trỏ cấp 2 hiểu đơn giản là một con trỏ trỏ tới con trỏ. Vì con trỏ cũng là một loại biến trong C, cho nên để lưu trữ nó thì cũng cần cấp phát địa chỉ và vùng nhớ. 
Có con trỏ cấp 2 thì tương tự cũng sẽ có con trỏ cấp 3, số lượng toán tử * đứng trước biến sẽ là cấp độ của con trỏ. 
Ví dụ 

```c
#include <stdio.h>
int main(){
    int N = 1000;
    int *ptr1 = &N;
    int **ptr2 = &ptr1; 
    printf("%p\n", ptr1);
    printf("%p\n", ptr2);
}
```


## Con trỏ và mảng 

Địa chỉ của phần tử đầu tiên trong mảng, `&a[0]` cũng chính là giá trị của `a`. 

```c 
#include <stdio.h>

int main(){
    int n; 
    scanf("%d",&n); 
    int a[n]; 
    for (int i = 0 ; i <n ;i++){
        printf("nhập phần tử %d\n  ", i+1); 
        scanf("%d", &a[i]); 
    }
    for (int i = 0 ; i < n ; i++){
        printf("%d\n", a[i]);
    }
    printf("%d",a); 
    printf("%d", &a[0]); 
    return 0;
}
```

Cả hai sẽ có cùng giá trị địa chỉ, chỉ khác biệt nhau ở kiểu dữ liệu, một bên là mảng một bên là số nguyên. 

Trong mảng một chiều `a[]` thì con trỏ trỏ tới phần tử `a[i]` sẽ là `a+i`. Ta có thể viết `a[i]` hoặc `a+i` đều được. 

Có thể dùng con trỏ để truy xuất phần tử: 

```c 
#include <stdio.h>
#include <stdlib.h>

int main(){
    int n = 5;
    int a[5] = {3, 8, 4, 2, 9};
    int *ptr = &a[0];
    for(int i = 0; i < n; i++){
        printf("%d ", *(ptr + i));
    }
    printf("\n");
    ++ptr; // => a[1]
    printf("%d\n", *ptr); 
    ptr+= 2; // a[3]
    printf("%d\n", *ptr);
    --ptr; // a[2]
    printf("%d\n", *ptr);
    return 0;
}
```

## Cấp phát động 

Cấp phát động là một kĩ thuật giúp ta có thể xin cấp phát một vùng nhớ phù hợp với nhu cầu của bài toán trong lúc thực thi thay vì phải khai báo cố định. 

Cấp phát động thường được dùng để cấp phát mảng động và ta sẽ học cách xây dựng cụ thể trong phần sau đây cùng với kiến thức về struct. 

### malloc() - memory allocation
Hàm này được sử dụng để xin cấp phát khối bộ nhớ theo kích thước byte mong muốn. 
Cú pháp
```c 
ptr = (cast_type*)malloc(byte_size)
```
- Trong đó ptr là con trỏ lưu trữ ô nhớ đầu tiên của vùng nhớ được cấp phát. 
- (cast_type*) là kiểu con trỏ mà ta muốn ép sang 
- Còn byte_size là kích thước theo byte mà ta muốn cấp


Chẳng hạn ta muốn cấp phát vùng nhớ cho một dãy các số nguyên 

```c 
#include <stdio.h>
#include <stdlib.h> 


int main(){
    int n; 
    int *ptr = (int*)malloc(100*sizeof(int));
    for (int i = 0 ; i < 100; i++){
        *(ptr + i) = i; 
    }
    for (int i = 0 ; i<100; i++){
        printf("%d ", ptr[i] );
    }
    return 0;
}
```
Note thêm: 


### calloc() - contiguous allocation

Tương tự như calloc(), được sử dụng để cấp phát vùng nhớ động nhưng các giá trị của các vùng nhớ được cấp phát sẽ có giá trị mặc định là 0 thay vì các giá trị rác như hàm malloc() 

```c
#include <stdio.h>
#include <stdlib.h> 


int main(){
    int n; 
    int *ptr = (int*)calloc(5,sizeof(int));
    for (int i = 0 ; i<5; i++){
        printf("%d ", ptr[i] );
    }
    return 0;
}
```
Ghi chú: Trong một số trường hợp nếu cấp phát lỗi thì ta cần check thêm đằng trước điều kiện `ptr == NULL`.
### free() 

Hàm `calloc()` và `malloc()` chỉ cấp phát vùng nhớ mà không tự giải phóng vùng nhớ. Do vậy ta cần gọi thêm hàm `free()` để làm việc này. 
Cú pháp đơn giản là `free(ptr)` (giải phóng ở cuối chương trình nếu không sẽ gặp lỗi)

### realloc() - re-allocation 


Hàm realloc() viết tắt của re-allocation tức là cấp phát lại, trong trường hợp sử dụng malloc() và calloc() nhưng cần bổ sung thêm bạn sử dụng realloc(). 
Cú pháp: 
```c 
ptr = (cast_type*)realloc(ptr, new_size)
```
Ví dụ:
```c 
#include <stdio.h>
#include <stdlib.h> 
int main(){
    int n; 
    int *ptr = (int*)calloc(5,sizeof(int));
    ptr = realloc(ptr, 10 * sizeof *ptr); 
    for (int i =0 ; i < 10; i++){
        printf("%d ", ptr[i]);
    }
    return 0;
}
```
## Con trỏ hàm

Ta có một khái niệm gọi là con trỏ hàm.
Con trỏ là một biến chứa địa chỉ của đối tượng được trỏ tới. Vậy thì con trỏ hàm là con trỏ chứa địa chỉ của một hàm. 
Ví dụ:
```c
int add(int a, int b){
    return a+b; 
}
```
Ta sẽ gọi 1 con trỏ trỏ tới hàm đó và pass tham số vào 
```c
#include <stdio.h>
#include <stdint.h>
int add(int a, int b){
    return a+b;
}
int main()
{
    int (*fp)(int,int); 
    fp = add;
    int res = fp(4,5); 
    printf("%d\n", res); 
    return 0;
}
```
Có thể truyền địa chỉ bằng `fp = add` hoặc `fp = &add` đều được. 

# Struct trong C 

Struct sẽ được gọi khi ta cần quản lý các đối tượng có nhiều trường thông tin, ví dụ như SinhVien thì cần có MSSV, lớp, chuyên ngành, v.v...
Khai báo như sau: 
```c 
struct ten_struct{
    data_type1 data_1; 
    data_type2 data_2;
    ...
        
};
```

Để truy cập vào trường dữ liệu của struct thì ta dùng toán tử `.`, chẳng hạn `ten_struct.data_1`


Struct cũng có thể khai báo lồng nhau 
```c 
#include <stdio.h>
#include <string.h>

struct TacGia{
    char hoten[100];
    char quoctich[100];
};

typedef struct TacGia TacGia;

struct Sach{
    TacGia tg;
    char tensach[100];
    int giaban;
};

typedef struct Sach Sach;

int main(){
    Sach s;
    strcpy(s.tensach, "Hanh trinh vo dich WC 2022");
    s.giaban = 500000;
    strcpy(s.tg.hoten, "Lionel Messi");
    strcpy(s.tg.quoctich, "Argentina");
    printf("Thong tin sach : \n");
    printf("Tieu de : %s\n", s.tensach);
    printf("Ten tac gia : %s\n", s.tg.hoten);
    printf("Quoc tich tac gia : %s\n", s.tg.quoctich);
    printf("Gia ban : %dVND\n", s.giaban);
    return 0;
}
```

và dùng làm tham số cho hàm
```c
#include <stdio.h>
#include <string.h>

struct CauThu{
    char hoten[50];
    char clb[50];
    char quoctich[50];
    int banthang, kientao;
};

typedef struct CauThu CauThu;

CauThu nhap(){
    CauThu x;
    printf("Nhap ho ten : "); gets(x.hoten);
    printf("Nhap clb : "); gets(x.clb);
    printf("Quoc tich : "); gets(x.quoctich);
    printf("So ban thang, kien tao : ");
    scanf("%d%d", &x.banthang, &x.kientao);
    return x;
}

void xuat(CauThu x){
    printf("Thong tin cau thu : \n");
    printf("Ho ten : %s\n", x.hoten);
    printf("CLB : %s\n", x.clb);
    printf("Quoc tich : %s\n", x.quoctich);
    printf("Ban thang : %d, kien tao : %d\n", x.banthang, x.kientao);
}

int main(){
    CauThu s = nhap();
    xuat(s);
    return 0;
}
```

## Con trỏ kiểu cấu trúc
Con trỏ kiểu cấu trúc có thể được sử dụng để trỏ tới biến cấu trúc, để truy cập các trường dữ liệu của biến cấu trúc thông qua con trỏ ta có thể kết hợp thêm toán tử giải tham chiếu. 

Ngoài cách dùng toán tử giải tham chiếu ra ta có thể sử dụng toán tử `->`
```c
#include <stdio.h>
#include <string.h>

struct SinhVien {
    char name[50];
    int age;
    float gpa;
};

int main() {
    struct SinhVien sv;          // biến cấu trúc bình thường
    struct SinhVien *p;          // con trỏ kiểu struct SinhVien

    // Gán địa chỉ của sv cho con trỏ p
    p = &sv;

    // Gán giá trị cho các trường thông qua con trỏ p
    // Cách 1: dùng toán tử * và .
    (*p).age = 20;
    (*p).gpa = 3.5f;
    strcpy((*p).name, "Nguyen Van A");

    // Cách 2: dùng toán tử ->
    p->age = 21;  
    p->gpa = 3.7f;


    printf("Ten: %s\n", sv.name);
    printf("Tuoi: %d\n", sv.age);
    printf("GPA: %.2f\n", sv.gpa);

    return 0;
}
```




# Chuỗi kí tự 

## Cơ bản
Trong C để lưu trữ chuỗi kí tự ta sử dụng mảng char. 
Xâu kí tự là một dãy các kí tự được kết thúc bởi kí tự null (`\0`)
Có 2 cách khai báo là đặt toàn bộ trong dấu nháy kép hoặc liệt kê từng kí tự của chuỗi. 
Ví dụ chương trình sau:
```c 
#include <stdio.h>
int main(){
    char c[] = "hello";
    printf("%s\n",c);
    char d[] = {'a','b','e','\0'};
    printf("%s\n",d);
    return 0;
}
```
Chuyện gì sẽ xảy ra nếu không thêm `\0` ở cuối dãy kí tự `d[]`?
Chương trình: 
```c
#include <stdio.h>
#include <string.h> 

int main(){
    char c[] = "hello";
    printf("%s\n",c);
    char d[] = {'a','b','e'};
    printf("%s\n",d);
    return 0;
}
```
Nó sẽ output ra như sau: 
![image](https://hackmd.io/_uploads/Sk87pzJfbe.png)


Vì sao nhỉ? 

Mình thử debug bằng pwngdb thì quan sát thấy được như sau: 

Đầu tiên đặt break point tại hàm `main()` rồi cho chương trình chạy tiếp

Thử in ra địa chỉ của mảng `c` và `d` thì mình thấy như này:
```c 
pwndbg> p &c
$1 = (char (*)[6]) 0x7fffffffd5c2
pwndbg> p &d
$2 = (char (*)[3]) 0x7fffffffd5bf
pwndbg> p &d[0]
$3 = 0x7fffffffd5bf ""
pwndbg> p &d[1]
$4 = 0x7fffffffd5c0 "\260\326\377\377\377\177"
pwndbg> p &d[2]
$5 = 0x7fffffffd5c1 "\326\377\377\377\177"
pwndbg> p &d[3]
$6 = 0x7fffffffd5c2 "\377\377\377\177"
pwndbg> p &d[4]
$7 = 0x7fffffffd5c3 "\377\377\177"
```
Vậy tức là stack sẽ trông như thế này:
```
0x7fffffffd5bf   d[0] = 'a'
0x7fffffffd5c0   d[1] = 'b'
0x7fffffffd5c1   d[2] = 'e'
0x7fffffffd5c2   c[0] = 'h'
0x7fffffffd5c3   c[1] = 'e'
0x7fffffffd5c4   c[2] = 'l'
0x7fffffffd5c5   c[3] = 'l'
0x7fffffffd5c6   c[4] = 'o'
0x7fffffffd5c7   c[5] = '\0'
```

Nếu mảng kí tự không có `\0` thì nó sẽ trigger Undefined behavior của C và đọc nốt phần còn lại của stack đó là các char của `c[]`

Mình sẽ chưa đi sâu vào phần này và cách xài pwngdb. Sẽ quay lại sau.

Đọc thêm tại: <a href="https://stackoverflow.com/questions/4711449/what-does-the-symbol-0-mean-in-a-string-literal">https://stackoverflow.com/questions/4711449/what-does-the-symbol-0-mean-in-a-string-literal</a>





- Để xuất chuỗi kí tự ra màn hình thì ta sẽ dùng đặc tả là `%s` như trên. 

- Còn để biết số lượng kí tự trong xâu ta sử dụng hàm `strlen()` trong thư viện `<string.h>`. Chú ý thêm rằng kí tự null ở cuối xâu không được tính là một kí tự trong xâu khi sử dụng hàm `strlen()`


- Nhập chuỗi với `scanf`. Nhưng sẽ có 2 trường hợp, 1 là nhập chuỗi không có dấu cách và có dấu cách. Với trường hợp nhập chuỗi không có dấu cách ta sử dụng hàm `scanf` với đặc tả `%s`. Nếu ta cố gắng nhập chuỗi có dấu cách thì hàm `scanf` chỉ nhập được từ đầu tiên cho tới khi gặp dấu cách. 

```c 
#include <stdio.h>
#include <string.h> 

int main(){
    char c[100]; 
    printf("Nhap xau ki tu\n");
    scanf("%s", c); 
    printf("%s\n", c); 
    printf("%d\n", strlen(c));
    return 0;
}
```
![image](https://hackmd.io/_uploads/BJLhSmyfbe.png)

Để nhập chuỗi có dấu cách ta sẽ sử dụng `gets()` hoặc `fgets()`. 
Nó sẽ nhận hết nội dung trên 1 dòng cho tới khi gặp dấu xuống dòng (enter) thì mới dừng nhập. 
```c
#include <stdio.h>
#include <string.h> 

int main(){
    char c[100]; 
    printf("Nhap xau ki tu\n");
    gets(c); 
    printf("%s\n", c); 
    printf("%d\n", strlen(c));
    return 0;
}
```
![image](https://hackmd.io/_uploads/Byr78QyMZx.png)

Khi xài hàm `gets()` thì mình nhận được một thông báo khá sus. 
```
 warning: the `gets' function is dangerous and should not be used.
```
Đọc bài viết này: <a href="https://stackoverflow.com/questions/1694036/why-is-the-gets-function-so-dangerous-that-it-should-not-be-used">https://stackoverflow.com/questions/1694036/why-is-the-gets-function-so-dangerous-that-it-should-not-be-used</a>


Còn với hàm `fgets()` thì cú pháp của nó sẽ bao gồm 3 args 
```c
char* fgets(char *string, int length, FILE *stream);
```
Trong đó 
- `char *string` sẽ là con trỏ trỏ tới char array mà ta muốn lưu kí tự nhập vào
- `int length` là độ dài tối đa của kí tự mà ta muốn đọc, bao gồm cả NULL char. `fgets` lúc này sẽ đọc tối đa (length-1) kí tự và chừa vị trí cuối cho NULL char
- FILE *stream: pointer tới file object để input stream đọc. Cái này có thể là pointer thu được từ các hàm như fopen hoặc ta có thể điền stdin cho standard input. 

```c
#include <stdio.h>
#include <string.h> 

int main(){
    char c[100]; 
    printf("Nhap xau ki tu\n");
    fgets(c, 100, stdin); 
    printf("%s\n", c); 
    printf("%d\n", strlen(c));
    return 0;
}
```

![image](https://hackmd.io/_uploads/rJJwvQJMZg.png)

Xử lí trôi lệnh. 
Có thể xử lí bằng `getchar()` để đọc 1 kí tự từ bàn phím. Hàm này sẽ đọc phím enter dư thừa. 


hoặc `scanf("\n")`.

Câu lệnh này sẽ bỏ qua mọi ký tự là dấu cách và enter cho tới khi bạn nhập kí tự khác dấu cách và enter, vì thế nếu bạn nhập số bằng scanf sau đó có dư thừa các dấu cách hoặc rất nhiều kí tự enter sau hàm scanf thì câu lệnh này sẽ giúp bạn loại bỏ toàn bộ


Tiếp theo ta có hàm `sú`. Cú pháp của hàm này sẽ là 


```c
strlen(char *c) 
```


`char *c` là con trỏ kiểu char trỏ tới kí tự đầu tiên mà mình muốn đếm.

Kết quả trả về của `strlen` là độ dài của chuỗi kí tự, không tính null byte `\0` ở cuối. 


## Hàm kiểm tra loại kí tự

Trong C cũng cung cấp cho ta một số hàm để kiểm tra loại kí tự. Các hàm này nằm trong thư viện `ctype.h`


![image](https://hackmd.io/_uploads/HJf1p5SzWl.png)


## Các hàm so sánh xâu
Để so sánh 2 xâu trong C thì bạn không thể sử dụng các toán tử so sánh mà phải dùng hàm, quy tắc so sánh 2 xâu là xét theo thứ tự từ điển.

Thứ tự từ điển được quyết định bởi mã ASCII, mã ASCII nhỏ hơn sẽ có thứ tự từ điển nhỏ hơn, ví dụ kí tự 'A' thì có thứ tự từ điển nhỏ hơn kí tự 'B'

Đầu tiên là hàm `int strcmp(char *s, char *t)`.
Nó sẽ trả về một giá trị < 0 nếu như `s<t`, bằng 0 nếu `s==t` và `>0` nếu `s>t`. 
Ví dụ 
```c
#include <stdio.h>
#include <string.h> 
#include <ctype.h> 


int main(){
    char c[] = "Hello"; 
    char d[] = "Hello123"; 
    printf("%d\n", strcmp(c,d)); 

    char e[] = "Hello"; 
    printf("%d\n", strcmp(c,e)); 

    char f[] = "HelloA";
    printf("%d\n", strcmp(f,d));
// -49
// 0
// 16
    return 0; 
}
```

Tiếp theo là hàm `int strncmp(char *s, char *t, size_t n)` để so sánh `n` kí tự đầu tiên của hai xâu. 

Lưu ý trong trường hợp 2 xâu có 1 xâu không đủ n kí tự thì xâu dài hơn sẽ có thứ tự từ điển lớn hơn.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char s[] = "hello";
    char t[] = "helium";

    int r1 = strncmp(s, t, 2);
    int r2 = strncmp(s, t, 3);
    int r3 = strncmp(s, t, 4);

    printf("So sánh 2 ký tự đầu: %d\n", r1); 
    printf("So sánh 3 ký tự đầu: %d\n", r2); 
    printf("So sánh 4 ký tự đầu: %d\n", r3);

    return 0;
}
```

# Static và ý nghĩa của nó
