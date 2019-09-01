---
layout: post
title: Nodejs 활용한 Video Streaming 하기
description: Http Live Streaming 
categories: Http nodejs streaming
---

# http range header
---------------------------------------  
Http header 필드인 range를 이용하여 chunk-data를 수신 할 수 있다.

header 형태는 아래와 같다.
~~~
GET HTTP/1.1 /
range : bytes=0-
~~~

0은 chunk data의 시작 position '-' 은 구분자
그리고 뒤에 나오는 숫자는 끝나는 position 값을 의미 한다.

예를 들면 bytes=0-100 이라면 0부터 100까지 길이의 데이터를 요청한 것이다.

range 필드를 가진 request에 대한 response 헤더는 아래의 필드를 포함 한다.

~~~

Accept-Ranges: bytes,
Content-Length: 100,
Content-Type: video/mp4

~~~  

range 필드를 포함한 request에 대한 응답은 응답 코드를 206(partial)로 전송하며,  

아래의 헤더 필드가 추가 된다.  

~~~
Content-Range: bytes 0-100/100
~~~  

의미는 0 ~ 100 까지의 바이트를 전송했으며 chunk data의 총 길이는 100 이다.  

없는 경우 응답 코드를 200(OK)으로 설정하며, 전체 데이터를 전송한다.

# 위 설명에 대한 예제(nodejs) 
---------------------------------------  

nodejs 및 간단한 html 파일로 위의 설명에 대한 예제를 작성했다.  

코드는 아래와 같다.  

- nodejs  

~~~javascript  
const https = require('https');
const fs = require('fs');
const url = require('url');
const querystring = require('querystring');

const options = {
        key : fs.readFileSync('/etc/letsencrypt/live/rasgo.iptime.org/privkey.pem'),
        cert: fs.readFileSync('/etc/letsencrypt/live/rasgo.iptime.org/cert.pem')

};

const getStream = function(req, res) {
        const file_name = querystring.unescape(req.url);
        if(!file_name) {
                res.writeHead(404, {'Content-Type':'text/html'});
                res.end();
                return;
        }

        fs.stat(file_name, (err,stats) => {
                if(err) {
                        if(err.code === 'ENOENT') {
                                res.writeHead(404, {'Content-Type':'text/html'});
                                res.end();
                                return;
                        }
                        throw err;
                }

                let start;
                let end;
                let total = 0;
                let contentRange = false;
                let contentLength = 0;

                let range = req.headers.range;
                if(range) {
                        let positions = range.replace(/bytes=/, "").split('-');
                        start = parseInt(positions[0], 10);
                        total = stats.size;
                        end = positions[1] ? parseInt(positions[1], 10) : total - 1;
                        const chunksize = (end - start) + 1;
                        console.log('chunksize:'+chunksize);
                        contentRange = true;
                        contentLength = chunksize;
                } else {
                        start = 0;
                        end = stats.size;
                        contentLength = stats.size;
                }

                 if(start <= end) {
                        let response_code = 200;
                        let header = {
                                "Accept-Ranges":"bytes",
                                "Content-Length":contentLength,
                                "Content-Type":"video/mp4"
                        };
                        if(contentRange) {
                                response_code = 206;
                                header["Content-Range"] = "bytes "+start+"-"+end+"/"+total;
                        }
                        res.writeHead(response_code, header);

                        let st = fs.createReadStream(file_name, { start : start, end: end})
                                .on('end', function() {
                                        console.log('stream Done');

                                })
                                .on('error', function(err) {
                                        res.end(err);

                                })

                                .pipe(res, {end : true});
                } else {
                        res.status(403).send();
                        return;
                }
        });
};

https.createServer(options, (req, res) => {

        console.log(querystring.unescape(req.url));
        const url = querystring.unescape(req.url);

        if(url === '/') {
                fs.readFile('streaming.html', (err, data) => {
                        res.writeHead(200, {'Content-Type':'text/html'});
                        res.end(data);
                });
        }
        else if( url === '/favicon.ico') {
                res.statusCode = 200;
                res.setHeader("Content-Type", "text/plain");
                res.end();

        }
        else {
                console.log('start..............');
                getStream(req, res);

        }
}).listen(7000);
~~~

- html  

~~~html
<!DOCTYPE html>
 <html>
 <head>
     <meta charset="UTF-8">
     <title>HTML5 video태그 예제</title>
 </head>
 <body>
     <video width="640" height="344" controls autoplay="autoplay">
       <source src="/home/bear/video/라디오스타.E605.190220.720p-NEXT.mp4" type="video/mp4">
       Your browser does not support the video tag.
     </video>
 </body>
 </html>
~~~