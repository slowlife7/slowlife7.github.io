---
layout: post
title: Let's Ecrypt 로 IPTIME DDNS HTTPS 적용하기
description: IPTIME DDNS에 HTTPS을 적용하자.
categories: git
---

# DDNS HTTPS 적용하기  
---------------------------------------  
IPTIME에서 제공하는 무료 도메인 서비스인 DDNS를 사용하다
github.io 블로그와 DDNS를 iframe으로 연결하기 위해서 HTTPS를
적용했습니다.

### Let's Encrypt 설치  
  
$ git clone https://github.com/letsencrypt/letsencrypt  

### letsencrypt 폴더 이동  
   
$ cd letsencrypt  

### 의존성 다운로드 및 설치  
  
$ ./letsecrypt-auto --help  

### letsecrypt 인증서 발급  
  
아래의 명령어를 입력하면 이메일, 사용하고 있는 도메인, 발급확인 단계로 
진행됩니다.  

$ ./letsencrypt-auto certonly --manual  

**인증서 발급 확인**  
  
아래와 같은 메시지가 출력되며, 아래의 url로 웹서버에 접속하여 인증단계를 마무리 합니다.
인증을 마무리 하기위해서 nginx를 설치합니다.

Create a file containing just this data:

OmmFpxoFsS3Pnw3iZbkVCj70xXyMh-NPw0zmux4HygM.3GLkXiUxIidyO0NaiIVh157SJMZqKC7sg-TXr1Fbl5g

And make it available on your web server at this URL:

http://rasgo.iptime.org/.well-known/acme-challenge/OmmFpxoFsS3Pnw3iZbkVCj70xXyMh-NPw0zmux4HygM  


### NGINX 설치
  
**Repository 등록**   
root 권한으로 아래의 스크립트 실행합니다.

$ cat << EOF > /etc/yum.repos.d/nginx.repo

[nginx]
name=Nginx Repository \$basearch - Archive
baseurl=http://nginx.org/packages/centos/\$releasever/\$basearch/
enabled=1
gpgcheck=1
gpgkey=https://nginx.org/keys/nginx_signing.key
EOF

**반영 여부 확인**  
  
$ yum info nginx  

**설치**  
  
$ yum install nginx  

**부팅시 자동 실행 설정**  
  
$ systemctl enable nginx
$ systemctl restart nginx

**환경 파일 설정**  
  
NGINX 환경 파일에 인증서 발급 확인 단계의 URI 경로에 매칭되는 PATH 설정합니다.  
  
$ vi /etc/nginx/conf.d/default.conf  
  
location /.well-known {                  //route point 지정
    root  /tmp/letsencrypt/public_html;  // 경로 지정 
}  

**NGINX 재시작**  
   
$ systemctl restart nginx  
  
### SSL 인증서 발급 진행
  

인증서 발급 확인 단계에서 Enter 입력합니다.

정상적으로 인증서 발급시 아래와 같은 메시지 출력됩니다.

IMPORTANT NOTES:
- Congratulations! Your certificate and chain have been saved at:
/etc/letsencrypt/live/rasgo.iptime.org/fullchain.pem
Your key file has been saved at:
/etc/letsencrypt/live/rasgo.iptime.org/privkey.pem
Your cert will expire on 2019-11-19. To obtain a new or tweaked
version of this certificate in the future, simply run
letsencrypt-auto again. To non-interactively renew *all* of your
certificates, run "letsencrypt-auto renew"
- If you like Certbot, please consider supporting our work by:

Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
Donating to EFF:                    https://eff.org/donate-le











