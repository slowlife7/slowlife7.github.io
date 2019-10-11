---
layout: post
title: HTML CSS 활용 Mobile 게시판 화면
description: Mobile 게시판 화면을 만들어 보자.
categories: html css
---


# Mobile 게시판 화면

![layout1]({{site.baseurl}}/images/layout_mobile_1.jpg)  

![layout2]({{site.baseurl}}/images/layout_mobile_2.jpg)  

# sample source
---------------------------------------  
html, css로 구현되어 있다.

예제 소스는 아래와 같다.

~~~html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <style>
            * { margin:0; padding: 0; }
            li { list-style: none; }
            a { text-decoration: none; }

            header { position: relative; text-align: center; background-color: rgb(204, 165, 165); color:#ffffff; }
            header > .header_left { position:absolute; top: 10px; left:10px; width: 80px; text-align: center;}
            header > .header_left a { color: #ffffff; }
            header > .header_right { position:absolute; top: 10px; right:10px; width: 80px; text-align: center; }

            #toggle { display: none; }
            #toggle:checked ~ .wrap_gnb  { display: block; }

            .wrap_gnb { display: none; }
            .wrap_gnb > .gnb ul { overflow: hidden; background-color: rgb(204, 165, 165); }
            .wrap_gnb > .gnb ul li { float:left; padding: 4px 15px; font-size:1.1em; }
            .wrap_gnb > .gnb ul li a { color: #ffffff; }

            content { width: 100%; }
            content > .wrap_content { margin:20px; }
            content > .wrap_content ul li { width: 100%; height: 50px; line-height: 50px; border-bottom: 1px solid #cccccc; }
            content > .pagination_content  { width: 300px; overflow: hidden; margin: 0 auto; }
            content > .pagination_content ul li { float:left; text-align: center;  }
            content > .pagination_content ul li a { display: block; font-size:1.2em; padding: 5px 12px; color:dimgray; }
            content > .pagination_content ul li a:hover { color:honeydew; }
        </style>
    </head>
    <body>
        <input id="toggle" type="checkbox"/>
        <header>
            <div class="header_left">
                <a href="#"><img src="" alt="Menu"></a>
            </div>
            <div class="header_main">
                <h1>OKKY</h1>
            </div>
            <div class="header_right">
                <label for="toggle" onclick=""><img src="" alt="Login"></label>
            </div>
        </header>
        <div class="wrap_gnb">
            <div class="gnb">
                <ul>
                    <li><a href>GNB1</a></li>
                    <li><a href>GNB2</a></li>
                    <li><a href>GNB3</a></li>
                    <li><a href>GNB4</a></li>
                    <li><a href>GNB5</a></li>
                </ul>
            </div>
        </div>

        <content>
            <div class="wrap_content">
                <ul>
                    <li>TEST1</li>
                    <li>TEST2</li>
                    <li>TEST3</li>
                    <li>TEST4</li>
                    <li>TEST5</li>
                    <li>TEST6</li>
                    <li>TEST7</li>
                </ul>
            </div>

            <div class="pagination_content">
                <ul>
                    <li><a href="#"><<</a></li>
                    <li><a href="#">1</a></li>
                    <li><a href="#">2</a></li>
                    <li><a href="#">3</a></li>
                    <li><a href="#">4</a></li>
                    <li><a href="#">5</a></li>
                    <li><a href="#">>></a></li>
                </ul>
            </div>
        </content>

        <footer>

        </footer>
    </body>
</html>

~~~