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
