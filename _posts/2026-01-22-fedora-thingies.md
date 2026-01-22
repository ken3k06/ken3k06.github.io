---
layout: post 
category: misc 
---

## Note số 1

Lúc đầu khi tải Fedora mình chỉ cấp cho nó 100GB ổ cứng. Việc cấp phát này bao gồm hai bước chính. Bước đầu tiên là tạo ra một phân vùng trống (unallocated memory) từ ổ đĩa D trên Windows. Bước thứ hai là trong quá trình cài đặt Fedora, mình chọn phân vùng trống này để Fedora tự xử lí nốt. 

Vấn đề đặt ra là sau khi boot xong thì liệu có cách nào để extend dung lượng ổ cứng của Fedora ra hay không? 

Cách đơn giản nhất ~~và khổ dâm nhất~~ đó là cài lại Fedora, tất nhiên trước khi cài thì phải backup lại dữ liệu rồi =)) nhưng cái khó không phải ở chỗ backup dữ liệu mà khó ở chỗ cài lại mấy cái tools. Và không ai điên mà đi chọn cách này cả (maybe)

Sau đó thì mình đọc được bài này <a href="https://discussion.fedoraproject.org/t/how-expand-fedora-partition/105550/9?fbclid=IwZXh0bgNhZW0CMTAAYnJpZBExNUVuYjJKS2JTUE4wY3pJbXNydGMGYXBwX2lkEDIyMjAzOTE3ODgyMDA4OTIAAR7_xfTCkxUI6DqzMhrn-cJpt-I0788YtM_sLfBlaSgWymtSbjHQARDCWtcScw_aem_RTlPeE6D0uwu6Q5bnCD_mA">How Expand Fedora Partition</a>

Trong bài này họ có gợi ý sử dụng một phần mềm thứ ba để quản lí các phân vùng đó là GParted. Tải tại đây: [Install](https://gparted.org/download.php)

Mình sử dụng Rufus và một cái USB để boot GParted. Bước tiếp theo là vào BIOS để đẩy cái USB lên đầu rồi tiến hành boot. 

Nó sẽ trông như này: 



<img src="{{ '/assets/images/fedora/gparted.png' | relative_url }}" 
  alt="..." 
  width="600">
Sau đó chọn ngôn ngữ và mode 


<img src="{{ '/assets/images/fedora/image.png' | relative_url }}" 
  alt="..." 
  width="600">

Sau khi xong xuôi thì mình vào được màn hình làm việc chính của GParted. Lúc này có hai việc mình cần làm: Ở trên ảnh thì mọi người có thể thấy có 3 phần vùng chính cần chú ý. Một là `unallocated`, đây là phân vùng trống mình Shrink từ ổ đĩa `D:` trên Windows. Tiếp theo là `/dev/nvme0n1p6` và `/dev/nvme0n1p7`. Một cái để chứa `/boot` và một cái để chứa `/` (root). 

<img src="{{ '/assets/images/fedora/gpart.png' | relative_url }}" 
  alt="..." 
  width="600">

Đầu tiên là di chuyển phân vùng `/dev/nvme0n1p6` về phía bên trái của `unallocated` rồi sau đó click vào `/dev/nvme0n1p7` chọn Resize/Move rồi kéo thả nó về bên trái hết cỡ để lấy hết phần `unallocated` này. 

Mình nghĩ tới đây là êm rồi nhưng không, nó báo lỗi như này:


<img src="{{ '/assets/images/fedora/error.png' | relative_url }}" 
  alt="..." 
  width="600">

Mình cũng không biết nó là lỗi gì nữa :v hỏi chatGPT thì nó cũng không biết. Mình thử resize rồi extend thêm vài lần nữa nhưng cũng không được. Đang lúc bế tắc thì mình đọc được bài này: <a href="https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/storage_administration_guide/resizing-btrfs"> https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/storage_administration_guide/resizing-btrfs</a>


Theo mình hiểu thì Fedora không cho phép resize btrfs file system. Nhưng mình có thể add thêm device vào để mở rộng dung lượng lưu trữ. 

Trước tiên mình cần chuyển phân vùng `unallocated` này thành một ổ đĩa mới hoàn toàn và không chỉnh định dạng cho nó (để nguyên dưới dạng RAW Data thay vì FAT32 hay NTFS). 

<img src="{{ '/assets/images/fedora/Edisk.png' | relative_url }}" 
  alt="..." 
  width="600">

Sau đó mình vào lại Fedora để kiểm tra bằng lệnh `lsblk` 

```
lsblk -f 
├─nvme0n1p6 ext4     1.0          a083214f-eaed-416c-9804-72da2e3e5e14  431.5M    49% /boot
├─nvme0n1p7                                                                           
└─nvme0n1p8 btrfs          fedora e5ac1948-971d-41cc-a67b-269f98439f24   72.6G    26% /home
```
CÓ một ổ đĩa mới là `nvme0n1p7` chưa được định dạng. Mình tiến hành add nó vào bằng các lệnh sau:
```
sudo wipefs -a /dev/nvme0n1p7
sudo btrfs device add /dev/nvme0n1p7 /
sudo btrfs filesystem balance start /
sudo btrfs filesystem balance status / 
sudo btrfs filesystem show /
```

Kết quả cuối cùng sẽ là:
```
Label: 'fedora'  uuid: e5ac1948-971d-41cc-a67b-269f98439f24
        Total devices 2 FS bytes used 25.07GiB
        devid    1 size 99.00GiB used 27.06GiB path /dev/nvme0n1p8
        devid    2 size 10.00GiB used 0.00B path /dev/nvme0n1p7
```

Ở đây `/` là mount point, hay cũng chính là `/home`. 

Demo là như vậy, còn bây giờ mình muốn dọn device này thì có thể chạy lệnh 
```
sudo btrfs device remove /dev/nvme0n1p7 /
```

Một số bài viết hay nên đọc: 
- <a href="https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/storage_administration_guide/index"> Storage Administration Guide </a>

- <a href="https://discussion.fedoraproject.org/t/how-to-take-care-of-your-btrfs-filesystem-health-on-atomic-desktops/146309"> How to take care of your BTRFS filesystem health </a>