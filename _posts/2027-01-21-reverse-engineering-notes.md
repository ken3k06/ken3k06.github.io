---
layout: post 
category: misc 
title: Some notes on Reverse Engineering 
---

Mục đích của bài này là để mình tổng hợp lại những kiến thức đã học trong quá trình tập tành chơi Reverse, nên có gì sai sót mong nhận được sự góp ý từ mọi người. 

* This will become a table of contents (this text will be scrapped).
{:toc}

## Tài liệu học 

- Series IDA: <a href="https://kienmanowar.wordpress.com/2019/02/21/reversing-with-ida-from-scratch-p1/"> IDA from scratch </a>
- Basic challenges list: [Github](https://github.com/N4NU/Reversing-Challenges-List/tree/master)
- Kiến thức cơ bản về Hệ điều hành, ASM x86_64, C/C++, ELF, PE, v.v..
- Wargames và CTF: [Dreamhack](https://dreamhack.io/), [Reversing.kr](http://reversing.kr/), [Crackmes](https://crackmes.one/), v.v..

## Setup môi trường 

Công việc đầu tiên mình cần phải làm đó là setup môi trường và tools để phục vụ cho việc giải các bài tập Reverse. 

Để chạy file .exe thì theo mình có 2 lựa chọn: 
- QEMU + KVM
- Wine

Giống như VMWare Workstation thì QEMU cũng là một Hypervisor còn KVM là một module hỗ trợ cho việc ảo hóa có trong nhân Linux. QEMU + KVM sẽ biến Linux kernel thành một hypervisor loại 1 nên sẽ cho hiệu năng tốt hơn hypervisor loại 2. Vậy 2 cái này khác nhau ở đâu? 

<img src="{{ '/assets/images/re-notes/type1-2.png' | relative_url }}" 
  alt="..." 
  width="600">

Nếu mọi người có thử nghịch qua Windows thì sẽ biết rằng Windows có một tính năng đó là Hyper-V được tích hợp sẵn trong hệ điều hành để quản lí các máy ảo. Đây cũng là một hypervisor type 1. 
Điểm khác biệt cơ bản giữa type 1 và type 2 đó chính là type 1 sẽ chạy trực tiếp máy ảo trên phần cứng vật lí và không bị quản lí bởi Host OS còn type 2 thì ngược lại, nó sẽ chạy máy ảo trên một phần mềm hypervisor được cài đặt trên Host OS. Về bộ môn này thì mình xin sẽ đi sâu vào ở các phần sau. 



Tuy nhiên việc setup cũng khá phức tạp nên mình tạm thời chọn cách dễ hơn đó là sử dụng Wine. Nếu mọi người có hứng thú thì có thể tham khảo ở đây: 

- <a href="https://github.com/Fmstrat/winapps/blob/main/docs/KVM.md">https://github.com/Fmstrat/winapps/blob/main/docs/KVM.md</a>
- <a href="https://github.com/hocchudong/KVM-QEMU">https://github.com/hocchudong/KVM-QEMU</a>

Về cơ bản, Wine là một lớp tương thích dùng để chạy ứng dụng Windows trên Linux, macOS & BSD bằng cách dịch thẳng Windows API calls sang POSIX calls một cách trực tiếp thay vì mô phỏng Windows logic như một máy ảo, điều này giúp cải thiện về hiệu năng và bộ nhớ. 


Để cài Wine trên Fedora thì có chỉ cần chạy lệnh sau:
```bash
sudo dnf install wine
``` 

Nếu trong quá trình tải gặp lỗi:
```bash 
Transaction failed: Signature verification failed. OpenPGP check for package "wine-10.20-3.fc42.x86_64" (/var/cache/libdnf5/updates-79babcf8637033ce/packages/wine-10.20-3.fc42.x86_64.rpm) from repo "updates" has failed: Problem occurred when opening the package.
```
Thì có thể thử fix bằng cách xóa cache `/var/cache/libdnf5/` đi rồi chạy lại lệnh cài đặt: 
```bash 
sudo rm -rf /var/cache/libdnf5/*
sudo dnf clean all 
sudo dnf makecache 
sudo dnf update --refresh
```
rồi sau đó chạy lại lệnh `sudo dnf install wine` là được. 

Còn về phần IDA và Ghidra: IDA mọi người có thể tải trực tiếp trên trang chủ của Hex-Rays còn Ghidra có thể tải thông qua snapd

```bash
sudo dnf install snapd 
sudo ln -s /var/lib/snapd/snap /snap 
sudo snap install ghidra
```
## Basic assembly 

## Hệ điều hành Linux 
Linux là một hệ điều hành hiện đại, miễn phí dựa trên UNIX. Nhân Linux bắt đầu được phát triển bởi Linus Torvalds vào năm 1991 với mục đích ban đầu để tương thích với UNIX. 

Cần phân biệt rõ giữa hai khái niệm sau: 
- Linux kernel: Phần mềm gốc được phát triển từ đầu bởi cộng đồng Linux 
- Linux system: Tập hợp các thành phần được phát triển dựa trên Linux kernel, bao gồm các thư viện hệ thống, công cụ dòng lệnh, trình quản lý gói, giao diện người dùng đồ họa (GUI) và các ứng dụng khác.

**Các thành phần chính của hệ thống Linux**: Như phần lớn các hệ thống UNIX, hệ thống Linux bao gồm 3 thành phần chính: nhân, thư viện hệ thống và công cụ hệ thống.


Nhân chịu trách nhiệm duy trì các hoạt động ở mức trừu tượng của hệ điều hành, như bộ nhớ ảo và tiến trình. 
- Các mã của nhân thực thi ở kernel mode với đầy đủ quyền truy xuất đến tài nguyên vật lí của máy tính. 
- Tất cả các mã của nhân và cấu trúc dữ liệu được lưu trên cùng một không gian địa chỉ. 

Các thư viện hệ thống (system librariies) định nghĩa một chuẩn các hàm mà thông qua đó các ứng dụng có thể tương tác với nhân. Các thư viện này cài đặt nhiều chức năng của hệ điều hành mà không cần đầy đủ quyền như các mã của nhân. 

Các công cụ hệ thống (system utilities) là các chương trình thực hiện các chức năng quản lí cụ thể. 



## Reversing.kr


### Easy Crack 
Chạy thử chương trình bằng wine thì thấy đây là một file check password. 


<img src="{{ '/assets/images/re-notes/ez-crack-1.png' | relative_url }}" 
  alt="..." 
  width="600">

Kiểm tra loại file:
```
❯ file Easy_CrackMe.exe
Easy_CrackMe.exe: PE32 executable for MS Windows 4.00 (GUI), Intel i386, 4 sections
```
Đây là file PE32 - Windows 32 bits. Mình mở file bằng IDA và vào hàm `start` để đọc code trước:
```c 
void __noreturn start()
{
  DWORD Version; // eax
  int wShowWindow; // eax
  HMODULE ModuleHandleA; // eax
  int v3; // [esp-4h] [ebp-78h]
  CHAR *lpCmdLine; // [esp+10h] [ebp-64h]
  int v5; // [esp+14h] [ebp-60h]
  struct _STARTUPINFOA StartupInfo; // [esp+18h] [ebp-5Ch] BYREF
  int v7; // [esp+70h] [ebp-4h]

  Version = GetVersion();
  dword_408534 = BYTE1(Version);
  dword_408530 = (unsigned __int8)Version;
  dword_40852C = BYTE1(Version) + ((unsigned __int8)Version << 8);
  dword_408528 = HIWORD(Version);
  if ( !sub_401CFD(0) )
    sub_4012A3((HINSTANCE__)28);
  v7 = 0;
  sub_4019DD();
  dword_408A38 = (int)GetCommandLineA();
  dword_408510 = sub_4018AB();
  sub_40165E();
  sub_4015A5();
  sub_4012C7();
  StartupInfo.dwFlags = 0;
  GetStartupInfoA(&StartupInfo);
  lpCmdLine = (CHAR *)sub_40154D();
  if ( (StartupInfo.dwFlags & 1) != 0 )
    wShowWindow = StartupInfo.wShowWindow;
  else
    wShowWindow = 10;
  v3 = wShowWindow;
  ModuleHandleA = GetModuleHandleA(0);
  v5 = WinMain(ModuleHandleA, 0, lpCmdLine, v3);
  sub_4012F4(v5);
}
```
Ở cuối chương trình ta thấy có hàm WinMain. Đối với các chương trình Windows GUI thì WinMain là tên được quy ước cho các hàm entry point của ứng dụng GUI. 

```
int __clrcall WinMain(
  [in]           HINSTANCE hInstance,
  [in, optional] HINSTANCE hPrevInstance,
  [in]           LPSTR     lpCmdLine,
  [in]           int       nShowCmd
);
```

Nội dung hàm `WinMain` trong IDA như sau: 


<img src="{{ '/assets/images/re-notes/winmain.png' | relative_url }}" 
  alt="..." 
  width="600">

```c
int __stdcall WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nShowCmd)
{
  DialogBoxParamA(hInstance, (LPCSTR)0x65, 0, DialogFunc, 0);
  return 0;
}
```

Ở đây ta thấy hàm `DiaglogBoxParamA` được gọi với tham số thứ 4 là `DialogFunc`. Đây chính là hàm callback xử lí các sự kiện trong dialog box. 

```c
INT_PTR __stdcall DialogFunc(HWND hDlg, UINT a2, WPARAM a3, LPARAM a4)
{
  if ( a2 != 273 )
    return 0;
  if ( (unsigned __int16)a3 == 2 )
  {
    EndDialog(hDlg, 2);
    return 1;
  }
  else if ( (unsigned __int16)a3 == 1001 )
  {
    sub_401080(hDlg);
    return 1;
  }
  else
  {
    return 0;
  }
}
```
Phân tích: Chương trình check `a2` với `273`. Nếu khác thì trả về `0` còn nếu bằng thì tiếp tục. `273` ở đây chính là giá trị của `WM_COMMAND`, kế sau đó là `a3`. Ta có `a3` đại diện cho giá trị `wPARAM`, vì ép kiểu `unsigned __int16` nên ta chỉ quan tâm đến 2 byte thấp của nó, cũng chính là giá trị của `LOWORD(wPARAM)`


Xem thêm tại: <a href="https://learn.microsoft.com/en-us/windows/win32/menurc/wm-command"> https://learn.microsoft.com/en-us/windows/win32/menurc/wm-command </a>

<img src="{{ '/assets/images/re-notes/WM.png' | relative_url }}" 
  alt="..." 
  width="600">

Ở trên thì chương trình sẽ cho ta 2 nhánh. Một nhánh khi `a3 == 2` thì sẽ gọi hàm `EndDialog`, nhánh còn lại khi `a3 = 1001` thì sẽ gọi hàm `sub_401080`. Nếu gọi hàm `EndDiaLog` thì chương trình sẽ kết thúc cho nên ta sẽ phân tích nhánh còn lại. 

Nội dung của hàm `sub_401080` như sau: 
```c 
int __cdecl sub_401080(HWND hDlg)
{
  CHAR String[97]; // [esp+4h] [ebp-64h] BYREF
  __int16 v3; // [esp+65h] [ebp-3h]
  char v4; // [esp+67h] [ebp-1h]

  memset(String, 0, sizeof(String));
  v3 = 0;
  v4 = 0;
  GetDlgItemTextA(hDlg, 1000, String, 100);
  if ( String[1] != 97
    || MEMORY[0x401150](&String[2], MEMORY[0x406078], 2)
    || strcmp(&String[4], MEMORY[0x40606C])
    || String[0] != 69 )
  {
    return MessageBoxA(hDlg, MEMORY[0x406030], Caption, 0x10u);
  }
  MessageBoxA(hDlg, Text, Caption, 0x40u);
  return EndDialog(hDlg, 0);
}
```
Ở đây chương trình set `String` là một mảng ký tự có độ dài 97, sau đó gọi hàm `GetDlgItemTextA` để lấy chuỗi ký tự từ dialog box với ID `1000` , tức là password mà ta nhập vào và lưu vào `String`.

Điều kiện để check password là: 

```c
  if ( String[1] != 97
    || MEMORY[0x401150](&String[2], MEMORY[0x406078], 2)
    || strcmp(&String[4], MEMORY[0x40606C])
    || String[0] != 69 )
```
Đầu tiên mình cần `String[0] = 'E'` và `String[1] = 'a'`. Tiếp theo mình có hàm `MEMORY[0x401150](&String[2], MEMORY[0x406078], 2)`.
Hàm này có pseudocode như sau:
```c 
int __cdecl MEMORY[0x401150](_BYTE *a1, _BYTE *a2, int a3)
{
  int v3; // ecx
  _BYTE *v4; // edi
  bool v5; // zf
  int v6; // ecx
  _BYTE *v7; // edi
  unsigned __int8 v9; // al

  v3 = a3;
  if ( a3 )
  {
    v4 = a1;
    do
    {
      if ( !v3 )
        break;
      v5 = *v4++ == 0;
      --v3;
    }
    while ( !v5 );
    v6 = a3 - v3;
    v7 = a1;
    do
    {
      if ( !v6 )
        break;
      v5 = *a2++ == *v7++;
      --v6;
    }
    while ( v5 );
    v9 = *(a2 - 1);
    v3 = 0;
    if ( v9 > *(v7 - 1) )
      return ~v3;
    if ( v9 != *(v7 - 1) )
    {
      v3 = -2;
      return ~v3;
    }
  }
  return v3;
}
```
2 byte tại địa chỉ `0x406078` là:
```
.data:00406078                 db '5y',0  
```
Về cơ bản thì hàm trên sẽ kiểm tra xem hai chuỗi `a1` và `a2` có giống nhau trong `v6 = a3 - v3` byte hay không. Nếu giống thì trả về `0`, khác thì trả về giá trị khác `0`.

Còn đối với `strcmp(&String[4], MEMORY[0x40606C])` , nó sẽ kiểm tra giá trị của chuỗi String bắt đầu từ vị trí thứ 4 với chuỗi địa chỉ tại `0x40606C`. Bật IDA lên thì mình có được giá trị của chuỗi này sẽ là: 
```
.data:0040606C                 db 'R3versing',0        ; DATA XREF: sub_401080+51↑o
.data:00406076                 align 4
.data:00406078                 db '5y',0               ; DATA XREF: sub_401080+3D↑o
.data:0040607B                 align 10h
.data:00406080 off_406080      dd 401305h     
```
Tổng hợp lại thì chuỗi cần nhập sẽ là `Ea` + `5y` + `R3versing` = `Ea5yR3versing`
<img src="{{ '/assets/images/re-notes/ez-crack-2.png' | relative_url }}" 
  alt="..." 
  width="600">


### Easy ELF 

Đầu tiên mình kiểm tra loại file:
```
❯ file Easy_ELF
Easy_ELF: ELF 32-bit LSB executable, Intel i386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.15, BuildID[sha1]=8edb9e400a3882319cd4582f89dd2373b7e1745c, stripped
```
Đây là file thực thi ELF 32-bit(Intel i386) trên Linux. Chạy thử file:
```
❯ chmod +x Easy_ELF
❯ ./Easy_ELF
Reversing.Kr Easy ELF

HI
Wrong
```
Bài này cũng thuộc dạng check password giống bài trước đó. 

Mở file bằng IDA: 
<img src="{{ '/assets/images/re-notes/ELF.png' | relative_url }}" 
  alt="..." 
  width="600">

Ở đây mình chọn ELF for Intel 386 và phần processor type mình sẽ để nguyên là MetaPC.

Hàm main của chương trình:
```c 
int main()
{
  write(1, "Reversing.Kr Easy ELF\n\n", 0x17u);
  sub_8048434();
  if ( sub_8048451() == 1 )
    sub_80484F7();
  else
    write(1, "Wrong\n", 6u);
  return 0;
}
```
Đầu tiên chương trình sẽ in ra dòng `Reversing.Kr Easy ELF`, sau đó gọi hàm `sub_8048434()` để lấy input từ người dùng.
```c 
int sub_8048434()
{
  return __isoc99_scanf(&unk_8048650, &byte_804A020);
}
```
Nó sẽ kiểm tra điều kiện:
```c
  if ( sub_8048451() == 1 )
    sub_80484F7();
```
Nếu đúng thì sẽ gọi `sub_80484F7()` để in ra `Correct` còn sai thì in ra `Wrong`.
```c
ssize_t sub_80484F7()
{
  return write(1, "Correct!\n", 9u);
}
```
Logic của hàm `sub_8048451()` như sau:
```c
_BOOL4 sub_8048451()
{
  if ( byte_804A021 != 49 )
    return 0;
  byte_804A020 ^= 0x34u;
  byte_804A022 ^= 0x32u;
  byte_804A023 ^= 0x88u;
  if ( byte_804A024 != 88 )
    return 0;
  if ( byte_804A025 )
    return 0;
  if ( byte_804A022 != 124 )
    return 0;
  if ( byte_804A020 == 120 )
    return byte_804A023 == -35;
  return 0;
}
```
Để ý thì: 
```c
  if ( byte_804A025 )
    return 0;
```
Nên ta có thể bỏ qua byte cuối. 
Còn lại thì ta tính toán các điều kiện để cho ra chuỗi cần nhập:
```python 
from z3 import * 
lst = [0] * 6

lst[1] = 49
lst[4] = 88 
lst[2] = 124 ^ 0x32
lst[3] = (-35 ^ 0x88) & 0xff 
lst[0] = 120 ^ 0x34
print(''.join([chr(x) for x in lst]))
# L1NUX 
```
```
❯ ./Easy_ELF
Reversing.Kr Easy ELF

L1NUX 
Correct!
```