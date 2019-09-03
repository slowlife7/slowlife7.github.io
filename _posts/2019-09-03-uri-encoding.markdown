---
layout: post
title: URL 인코딩 
description: URL 인코딩 
categories: Http nodejs uri
---

# URL 인코딩
---------------------------------------  
브라우저에서 웹서버로 전달되는 URI는 유효한 ASCII 형식으로 전송됩니다.  

- ASCII 코드 대응 값이 없는 경우 UTF-8 로 변환된 HEX 값 앞에 %를 추가한다.

![ascii]({{site.baseurl}}/images/ascii_code.gif)  

EX)
~~~  

https://test.com?query=한글 -> https://test.com?query=%ED%95%9C%EA%B8%80

https://test.com?query=test -> https://test.com?query=test

~~~  

# nodejs sample source
---------------------------------------  
~~~javascript

const https = require('https');
const url = require('url');
const fs = require('fs');

const ssl_options = {
        key : fs.readFileSync('ssl/privkey.pem'),
        cert: fs.readFileSync('ssl/cert.pem')
};

https.createServer(ssl_options, (req, res) => {

        const path = url.parse(req.url);
        console.log(path.query);
        res.writeHead(200, {'Content-Type':'text/html'});
        res.end();
}).listen(7000);

~~~

# javascript 인코딩, 디코딩 함수
---------------------------------------  
- URI 전체 인코딩 encodeURI  
- URI 파라미터 인코딩 encodeURIComponent  

# 참고 사이트

[덕's IT Story](https://itstory.tk/entry/인코딩이란-ASCII-URL-HTML-Base64-MS-Script-인코딩)

[FreshCrush, Developer](https://trustit.tistory.com/159)

[KAZIKAI's 개발자 블로그](http://blog.kazikai.net/?p=194)
