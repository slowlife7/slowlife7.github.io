---
layout: post
title: Http Basic Authentication 
description: Http 기본 인증하기
categories: Http nodejs
---

# Basic Authentication?  
---------------------------------------  
Http Header를 이용하여 기본적인 인증을 할 수 있는 방법.  

Client로부터 Get 요청을 수신시 인증이 필요한 경우 서버에서 헤더에 'WWW-Authenticate', 상태 코드 '401' 추가하여 송신한다.  

# WWW-Authenticate 헤더    
~~~
HTTP/1.1 401 Unathorization
WWW-Authenticate: Basic realm="test1"
~~~  

WWW-Authenticate 를 수신한 Client는 사용자에게 ID 및 PWD 를 입력 받아 'id:pwd' 형태로 BASE64 인코딩한다.  

서버에 송신후 서버에서는 BASE64로 디코딩하여 ID, PWD를 확인한다.  

# Http Autorization 헤더   
~~~
authorization: Basic 'id:pwd'
~~~


위의 설명에 대한 그림은 아래와 같다.   

![Basic Auth]({{site.baseurl}}/images/http_authenticate_diagram.jpg)  


# 인증 테스트  
---------------------------------------  

nodejs 로 작성된 sample이며, https://127.0.0.1:7000 로 접속시 아래와 같은 화면이 보여진다.  

인증 성공시 Hello World 가 출력되며, 실패시 UnAthorization가 출력 된다.  

![Basic diagram]({{site.baseurl}}/images/authentication.jpg)  

# nodejs sample  
---------------------------------------  

~~~javascript  

const http = require('http');
const fs = require('fs');
const url = require('url');
const querystring = require('querystring');


http.createServer((req, res) => {

        const url = querystring.unescape(req.url);
        const method = req.method;

        if(method === 'GET' && url === '/' ) {
                const authorization = req.headers["authorization"];
                if(authorization) {
                        let remove_trim_auth = authorization.split(" ")[1].trimRight();
                        let decoded_base64_auth = Buffer.from(remove_trim_auth, "base64").toString("utf8");

                        const splited_auth = decoded_base64_auth.split(":");
                        if(splited_auth[0] === 'test1' && splited_auth[1] === '1234') {
                                console.log('success');
                                res.writeHead(200, {"Content-Type":"text/plain"});
                                res.end('Hello World');
                        } else {
                                res.writeHead(401, {"Content-Type":"text/plain"});
                                res.end('UnAthorization');
                        }

                } else {
                        const headers = {
                                "Content-Type": "text/plain",
                                "WWW-Authenticate": "Basic realm=\"test1\""
                        };
                        res.writeHead(401, headers);
                        res.end();
                }

        } else {
                res.writeHead(404, {"Content-Type":"text/plain"});
                res.end('Not Found Page');
        }
}).listen(7000);  

~~~  