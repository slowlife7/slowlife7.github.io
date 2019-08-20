---
layout: post
title: 기본적인 Git 사용법 (1)
description: Git 사용법을 알아보자.
tags: [Git, Learn] # add tag
---

# Git ?
---------------------------------------
SVN 같은 중앙 서버로 관리하는 버전 시스템과 다르게 Local Repository, Remote Repository 별도로  
버전관리가 가능하다.

# Git 파일 관리
---------------------------------------
Git은 파일을 스냅샷 형태로 저장하며, 아래와 같이 3 가지 단계가 존재한다.

![Git Status]({{site.baseurl}}/assets/img/gitstatus.jpg)


- **Working Directory**  
CheckOut 한 특정 버전의 프로젝트 디렉토리. 

- **Staging Area**  
Git 디렉토리에 존재하며 곧 커밋 할 파일에 대한 메타 정보 저장.  

- **Git Repository**  
커밋된 데이터가 저장되는 Git 데이터베이스  
Working Directory의 모든 파일은 Tracked 와 UnTracked로 표현 될 수 있으며  
Tracked는 Git으로 관리되고 있는 파일을 의미한다.  

# Git의 파일 상태  
---------------------------------------

- **Modified**  
Working Directory의 파일이 변경된 상태.  

- **Staged**  
Modified 상태거나 Untracked 파일을 Add 하여 Staging Area로 올린 상태.  

- **Commited**  
Staging Area에서 Git Repository로 Commit 완료 상태.  


