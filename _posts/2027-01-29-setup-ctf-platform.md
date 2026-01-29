---
layout: post 
category: misc 
title: Setup CTF platform 
---

## rCTF 


Ở đây mình sẽ xài rCTF. Doc xem tại đây <a href="https://github.com/otter-sec/rctf"> https://github.com/otter-sec/rctf</a>


Đầu tiên ta tải về bằng lệnh sau dưới quyền root:

```bash
❯ sudo su
root@192:/home/dvck13/Desktop/CTF# curl -L https://get.rctf.osec.io | sh
```

Sau đó platform sẽ mặc định chạy trên port 8080. 

Config cho platform sẽ được đặt tại `/opt/rctf/` ở thư mục root. 

Restart lại bằng docker compose như sau: 
```bash
docker compose up -d --force-recreate --build
```

Mặc định thì các container sẽ được tự động chạy mỗi khi restart máy, để tắt cài đặt này thì có thể chạy lệnh sau: 
```bash 
sudo docker update --restart=no rctf-rctf-1\nsudo docker update --restart=no rctf-postgres-1\nsudo docker update --restart=no rctf-redis-1\n
```

Kiểm tra lại: 
```bash 
docker ps -a 
sudo docker stop rctf-rctf-1 rctf-postgres-1 rctf-redis-1\n
```

