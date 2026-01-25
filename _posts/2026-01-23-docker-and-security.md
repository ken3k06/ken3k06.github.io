---
layout: post 
category: misc
title: Docker and Security
---

* This will become a table of contents (this text will be scrapped).
{:toc}

## Tài liệu 
- <a href="https://docs.docker.com/reference/"> Docker Documentation</a> 
- <a href="https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html"> OWASP Docker Security Cheat Sheet</a>

## Các khái niệm cơ bản 

### Docker là gì? 
Docker là một nền tảng cho phép developers và sysadmin để develop, deploy và run application với container. Nó cho phép tạo các môi trường độc lập và tách biệt để khởi chạy và phát triển ứng dụng và môi trường này được gọi là container. Khi cần deploy lên server thì chỉ cần run container của Docker lên server là xong. 

Để cài đặt docker-engine trên fedora thì mình làm như sau (hiện tại thì docker-engine hỗ trợ 3 phiên bản fedora mới nhất là 41,42,43) : 

Đầu tiên cần xóa các gói cũ tồn tại trước đó trên hệ thống:
```bash 
sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

Tiếp theo cần set-up Docker repository và tải thông qua package manager rpm:
```bash
sudo dnf config-manager addrepo --from-repofile https://download.docker.com/linux/fedora/docker-ce.repo
```
Để cài đặt phiên bản mới nhất thì chạy lệnh sau đây: 
```bash 
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Check GPG fingerprint có đúng là `060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35` hay không. Sau đó chạy docker engine bằng `systemctl`

```
sudo systemctl enable --now docker 
```
Kiểm tra trạng thái docker service bằng 
```
sudo systemctl status docker 
❯ sudo systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: disabled)
    Drop-In: /usr/lib/systemd/system/service.d
             └─10-timeout-abort.conf
     Active: active (running) since Wed 2026-01-21 20:00:16 +07; 37min ago
```
Để kiểm tra docker đã được cài đặt thành công chưa thì chạy lệnh `docker run hello-world` 

Về kiến trúc, docker sử dụng mô hình client-server và bao gồm các thành phần Docker's Client, Docker Host, Network và Storage components và Docker Registry/Hub 

<img src="{{ '/assets/images/docker/architect.png' | relative_url }}" 
  alt="..." 
  width="600">

1. Docker client: là nơi người dùng tương tác với docker thông qua CLI. Khi bất kì lệnh docker nào chạy, client sẽ gửi chúng đến dockerd daemon để thực hiện các lệnh đó. Docker API được sử dụng bởi các lệnh Docker. Docker client có thể giao tiếp với nhiều hơn một daemon. 

    Dockerd ở đây là một tiến trình chạy nền(daemon) của docker, thường nằm ở `/usr/bin/dockerd`. Dockerd sẽ chịu trách nhiệm quản lí các object của docker như image, container, network và volume. 

2. Docker host: docker host cung cấp một môi trường hoàn chỉnh để thực thi và chạy các ứng dụng. Nó bao gồm docker daemon, images, containers, networks và storage. Như đã đề cập trước đó, dockerd chịu trách nhiệm cho tất cả các hành động liên quan đến container và nhận các lệnh thông qua CLI hoặc API REST. 

3. Docker's Registry: Docker registry là một kho lưu trữ để lưu trữ và phân phối các docker image. 


Ví dụ khi ta chạy lệnh `docker run nginx` và hiện tại trên máy chưa có nginx image thì docker client sẽ gửi yêu cầu tới docker daemon để từ đó docker daemon gửi tiếp yêu cầu tới docker registry để tải nginx về máy. Mặc định thì các cơ quan đăng ký công khai bao gồm Docker Hub và Docker Cloud. Ngoài ra, người dùng cũng có thể thiết lập private registry của riêng mình. 

```
❯ sudo docker run nginx
[sudo] password for dvck13: 
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
700146c8ad64: Pull complete 
57f0dd1befe2: Pull complete 
d989100b8a84: Pull complete 
500799c30424: Pull complete 
eaf8753feae0: Pull complete 
119d43eec815: Pull complete 
10b68cfefee1: Pull complete 
e2dd2dbe6277: Download complete 
785250c9bf9e: Download complete 
Digest: sha256:c881927c4077710ac4b1da63b83aa163937fb47457950c267d92f7e4dedf4aec
Status: Downloaded newer image for nginx:latest
```

Docker sẽ tự pull về nếu không có image hoặc ta có thể tự pull bằng `docker pull <image-name>`


Kiểm tra các images trên máy:
```
❯ sudo docker images
                                                                                                                                         i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   05813aedc15f       21.8kB         9.52kB    U   
nginx:latest         c881927c4077        239MB         65.7MB    U   
```

Vì ở trên ta chỉ chạy `sudo docker run nginx` cho nên khi check `docker ps`, ta thấy nginx đang chạy ở PORT 80 trong container nhưng không map ra ngoài host. 

```
❯ sudo docker ps
[sudo] password for dvck13: 
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
cd8f51e8d35a   nginx     "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes   80/tcp    festive_keldysh
```
Để test xem nginx đã chạy thành công chưa thì mình cần stop images này rồi chạy lại một lần nữa với các flag đầy đủ hơn:
```
sudo docker stop [docker-name]
sudo docker run -d --name web -p 8080:80 nginx
```
Ở đây ta xài thêm flag `-d` để chạy ngầm container, nếu không thêm flag này thì terminal sẽ bị kẹt và ta không làm việc tiếp được. Nếu xài `Ctrl+C` thì container sẽ bị stop ngay. Tiếp theo là flag `-p` để map port. Ở đây ta map port 80 trong container ra port 8080 trên host (nginx mặc định chạy trên port 80). 



Cuối cùng, test bằng curl xem có chạy được chưa: 
```
❯ curl -I http://127.0.0.1:8080
HTTP/1.1 200 OK
Server: nginx/1.29.4
Date: Wed, 21 Jan 2026 14:07:44 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Tue, 09 Dec 2025 18:28:10 GMT
Connection: keep-alive
ETag: "69386a3a-267"
Accept-Ranges: bytes
```

Để xóa images thì xài lệnh 
```
docker rmi <Image ID>/<Image name>
```
Còn với các container trong `docker ps -a` thì xóa bằng `docker rm <Container ID>/<Container name>`

### Docker image vs Container 
Docker image là một file bất biến, chỉ đọc, bao gồm tất cả các mã nguồn, thư viện, công cụ và các thiết lập phụ thuộc cần thiết để chạy một ứng dụng. Docker image đôi khi còn được gọi là snapshots. Images chỉ là các mẫu và việc duy nhất ta có thể làm với images là sử dụng chúng để làm cơ sở xây dựng một container.

Khi ta chạy một môi trường containerized, về cơ bản ta đang tạo một instance đọc-ghi của một docker image bên trong container. Lúc này nó sẽ thêm một container layer cho phép sửa đổi toàn bộ bản sao của image. 


<img src="{{ '/assets/images/docker/layer.png' | relative_url }}" 
  alt="..." 
  width="600">

Ngoài ra ta có thể lưu trữ các images bên trong các registry công khai hoặc riêng tư để dễ dàng phân phối và triển khai chúng trên các môi trường khác nhau.

Ví dụ: khi chạy `sudo docker run nginx` và `sudo docker run -d --name web -p 8080:80 nginx` thì ta đã tạo ra các container từ cùng một docker image là nginx. Tuy nhiên, mỗi container sẽ có các trạng thái riêng biệt với nhau.  



### Dockerfile 

Để build một docker image thì ta cần một Dockerfile. 


## Docker compose 
