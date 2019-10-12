---
layout: post
title: HTTP COOKIE ?
description: COOKIE 란 무엇인가?
categories: http
---

# HTTP 헤더 필드 중 쿠키에 대해 알아보자
---------------------------------------  
HTTP STATELESS 한 특징으로 Client와 연결을 유지하지 않는다.

따라서 연결에 대한 정보를 기억 할 수 없다.

요청에 대한 Response에 Cookie가 설정되어 있다면 클라이언트에서 쿠키를 가지고

해당 연결에 대한 정보를 유지한다. ( 보안상 취약하다. )    
  
# HTTP HEADER 필드
---------------------------------------
### Response  
Set-Cookie: &lt;cookie-name	&gt;=&lt;cookie-value&gt;  

Expires : 명시한 날짜에 만료된다.  

Max-Age: 명시한 기간 이후에 만료된다.  

Secure : HTTPS 프로토콜 상에서 암호화된(encrypted ) 요청일 경우에만 전송됩니다.  

HttpOnly: HttpOnly쿠키는 JavaScript의 Document.cookie API에 접근할 수 없습니다.  

Domain: 도메인이 명시되면, 서브도메인들은 항상 포함됩니다.  

Path: Cookie 헤더를 전송하기 위하여 요청되는 URL 내에 반드시 존재해야 하는 URL 경로입니다.  

### Request  
Cookie: &lt;cookie-name&gt;=&lt;cookie-value&gt;&#59; &lt;cookie-name&gt; =&lt;cookie-value&gt;  
  
# EXAMPLE 
---------------------------------------  
### 로그인 요청  
![cookie_1]({{site.baseurl}}/images/cookie1.JPG)  
![request_1]({{site.baseurl}}/images/request1.JPG) 

### 응답
![response_]({{site.baseurl}}/images/response.JPG)  
  
### 처음과 동일한 URL로 요청  
![requeust_url]({{site.baseurl}}/images/request2.JPG)  
![cookie_2]({{site.baseurl}}/images/cookie2.JPG)  
  
# sample html  (index.html)
---------------------------------------  
~~~html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>쿠키 & 세션 이해하기</title>
</head>
<body>
    <form action="/login">
        <input id="name" name="name" placeholder="이름을 입력하세요" />
        <button id="login">로그인</button>
    </form>   
</body>
</html>
~~~  

# sample nodejs  (app.js)
---------------------------------------  
~~~javascript
const express = require('express');
const fs = require('fs');
const app = express();

app.use('/login', (req, res, next) => {
    const name = req.query.name;
    const expires = new Date();
    expires.setMinutes(expires.getMinutes() + 5);
  
    res
      .status(201)
      .cookie("name", name, { expires: expires })
      .redirect(302, "/");
});

app.use('/', (req, res, next) => {

    if( req.headers.cookie ) {
      const name = req.headers.cookie.split('=')[1];
      res
      .status(200)
      .set({
        "Content-Type": "text/html charset=utf-8"
      })
      .end(`${name}님 안녕하세요`);
    } else {
        fs.readFile('index.html', (err, data) => {
            if (err) {
                next(err);
                return;
              }
            res.end(data);
        });
    }
});

app.use((err, req, res, next) => {
    console.log('Can not found any router');
	res.status(500).end();
})

app.listen(3000, function() {
	console.log('app listening on port 3000!');
});

~~~