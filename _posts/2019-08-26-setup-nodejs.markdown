---
layout: post
title: Centos Nodejs 설치 하기
description: Centos Nodejs 설치 하기
categories: nodejs
---

### 아래의 주소에서 Linux Binaries (x64) 다운로드  
---------------------------------------  
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz  

### 환경 변수 및 디렉토리 생성 
  
VERSION=v10.16.3
DISTRO=linux-x64  
  
  
sudo mkdir -p /usr/local/lib/nodejs  
sudo tar -xJvf node-$VERSION-$DISTRO.tar.xz -C /usr/local/lib/nodejs  

### bash_profile 설정    
   
$ vi ~/.bash_profile  
   
VERSION=v10.15.0  
DISTRO=linux-x64  
export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH  

### profile 반영  
  
source ~/.bash_profile    