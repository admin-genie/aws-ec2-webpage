# AWS EC2 Metadata Webpage
📌실습 링크 
[![Naver Blog Badge](https://img.shields.io/badge/Naver%20Blog-03C75A?style=flat&logo=Naver&logoColor=white)](https://blog.naver.com/genie290/223348121840)
---
## 1. 설치 패키지
#### Apache2 , PHP 5.4
#### CentOS/AWS Linux 기준
```
sudo yum -y install httpd php mysql php-mysql git
sudo systemctl start httpd
sudo systemctl enable httpd
curl "https://d1vvhvl2y92vvt.cloudfront.net/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
sudo cd /var/www/html/ && sudo git clone https://github.com/kimdragon50/ec2meta-webpage.git
```

#### AWS EC2 Instance User Data Shell Script 설치 기준
```
#!/bin/sh
sudo yum -y update
sudo yum -y install httpd php mysql php-mysql git
sudo systemctl start httpd
sudo systemctl enable httpd
curl "https://d1vvhvl2y92vvt.cloudfront.net/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
sudo cd /var/www/html/ && sudo git clone https://github.com/kimdragon50/ec2meta-webpage.git
```
_Amazonlinux 사용할 경우에는 awscli 설치 과정이 필요하지 않음_

## 2. 구성 테스트
#### 설치 이후 
#### Apache Daemon 정상 작동 유무 점검
```
ec2-user@ip-10-1-1-148 ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
   Active: active (running) since 일 2020-01-05 08:35:59 UTC; 5h 50min ago
     Docs: man:httpd.service(8)
 Main PID: 4978 (httpd)
   Status: "Total requests: 226; Idle/Busy workers 100/0;Requests/sec: 0.0108; Bytes served/sec:  27 B/sec"
    Tasks: 59
   Memory: 21.3M
   CGroup: /system.slice/httpd.service
           ├─4978 /usr/sbin/httpd -DFOREGROUND
           ├─5021 /usr/sbin/httpd -DFOREGROUND
           ├─5048 /usr/sbin/httpd -DFOREGROUND
           ├─5050 /usr/sbin/httpd -DFOREGROUND
           ├─5053 /usr/sbin/httpd -DFOREGROUND
           ├─5062 /usr/sbin/httpd -DFOREGROUND
           ├─5084 /usr/sbin/httpd -DFOREGROUND
           └─5673 /usr/sbin/httpd -DFOREGROUND

 1월 05 08:35:59 ip-10-1-1-148.ap-northeast-2.compute.internal systemd[1]: Starting The Apache HTTP Server...
 1월 05 08:35:59 ip-10-1-1-148.ap-northeast-2.compute.internal systemd[1]: Started The Apache HTTP Server.
 ```
 #### aws cli 기반 ec2meta-data 정보 확인
 ```
 [ec2-user@ip-10-1-1-148 ~]$ ec2-metadata --all
ami-id: ami-0d59ddf55cdda6e21
ami-launch-index: 0
ami-manifest-path: (unknown)
ancestor-ami-ids: not available
block-device-mapping:
	 ami: /dev/xvda
	 root: /dev/xvda
instance-id: i-0a3a923c6abbc6368
instance-type: t2.medium
local-hostname: ip-10-1-1-148.ap-northeast-2.compute.internal
local-ipv4: 10.1.1.148
kernel-id: not available
placement: ap-northeast-2a
product-codes: not available
public-hostname: ec2-13-125-155-84.ap-northeast-2.compute.amazonaws.com
public-ipv4: 13.125.155.84
public-keys:
keyname:whchoi_office_mac
index:0
format:openssh-key
key:(begins from next line)
ramdisk-id: not available
reservation-id: r-05fa2da8daaac6eb4
security-groups: SSH_WEB_FTP_ICMP
user-data: not available
```
#### AWS EC2 Metadata Webpage 출력 화면
- http://MY_IP/ec2meta-webpage/index.pnp
![AWS EC2 Meta Data 2024](https://user-images.githubusercontent.com/11262759/71781799-1c463b80-3016-11ea-88a4-543dae8858ae.png)
