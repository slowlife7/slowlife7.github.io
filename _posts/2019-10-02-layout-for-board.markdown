---
layout: post
title: HTML CSS 로 게시판 Layout 만들기
description: HTML CSS를 사용해서 게시판 형태를 만들어 보자.
categories: html css
---

# 게시판
---------------------------------------  
HTML 과 CSS를 이용하여 게시판 형태를 만들어 보았다.

# sample source
---------------------------------------  
html, css로 구현되어 있다.

예제 소스는 아래와 같다.

~~~html
<!DOCTYPE HTML>
<html>
  <head>
    <meta charset="utf-8"/>
    <style>
     
      h1{
        text-align: center;
      }

      a {
        text-decoration: none;
      }

      #wrap {
        width: 100%;
        height: 700px;
        margin: 0 auto;
        line-height: 700px;
        overflow: hidden;
      }

      header {
        width: 100%;
        height: 100px;
        line-height: 100px;
        margin: 0 auto;
        border: 1px solid #cccccc;
      }

      footer {
        width: 99%;
        height: 70px;
        line-height: 70px;
      }

      section .section_content .section_search {
        width:700px;
        height: 50px;
        line-height: 50px;
        margin: 0 auto;
      }
  
      section .section_content .section_board{
        width: 700px;
        height: 500px;
        line-height: 500px;
        margin: 0 auto;
        border: 1px solid #cccccc;
        background-color: #f8f8f8;
       
      }

      section .section_content .section_board li {
        list-style-type: none;
      }

      section .section_content .section_board div {
        height: 30px;
        line-height: 30px;
        float : left;
        border: 1px solid #cccccc;
        background-color: #ffffff;
        margin-top: 1px;
      }

      section .section_content .section_board .title_board {
        width: 370px;
        border-right: 0;
        border-left : 5px solid lightblue;
      }

      section .section_content .section_board .summary_board {
        width: 150px;
        border-left: 0; border-right: 0;
      }

      section .section_content .section_board .author_board {
        width: 100px;
        border-left: 0;
      }

      .pagination {
        width: 700px;
        height: 60px;
        line-height: 60px;
        margin: 0 auto;
        margin-top: 20px;
       
      }

      .pagination ul {
        width: 400px;
        height : 40px;
        line-height: 40px;
        margin: 0 auto;
        
      }

      .pagination li a {
        text-decoration: none;
        color:#000000;
        padding: 18px;
        
      }

      .pagination li {
        float:left;
        width: 40px;
        list-style: none;
        line-height: 20px;
        height: 20px;
      
        text-align: center;
      }


    </style>
  </head>
  <body>
    <div id="wrap">
      <header>
        <h1>Board</h1>
      </header>

      <nav>

      </nav>

      <section>
        <div class="section_content">
          <div class="section_search">
            <input type="text"/>
            <button>search</button>
          </div>
          <div class="section_board">
          <ul>
            <li>
                <div class="title_board"><a href="#">TITLE</a></div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>

            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>
            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>
            <li>
                <div class="title_board">TITLE</div>
                <div class="summary_board">SUMMARY</div>
                <div class="author_board">AUTHOR</div>
            </li>
          </ul>
        </div>
        </div>
      </section>

      <footer>
        <div class="pagination">
          <ul>

              <li>
                  <a href="#"><<</a>
                </li>

            <li>
              <a href="#">1</a>
            </li>

            <li>
              <a href="#">2</a>
            </li>

            <li>
                <a href="#">3</a>
            </li>

            <li>
                <a href="#">4</a>
            </li>

            <li>
                <a href="#">5</a>
            </li>

            <li>
                <a href="#">>></a>
            </li>
          </ul>
        </div>
      </footer>
    </div>
  </body>
</html>

~~~