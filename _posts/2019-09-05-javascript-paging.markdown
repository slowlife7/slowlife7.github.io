---
layout: post
title: JAVASCRIPT PAGING 하기
description: JAVASCRIPT로 Paging 해보자.
categories: javascript
---

# 페이징?
---------------------------------------  
게시판에서 많이 볼 수 있으며, 아래와 같이 페이지를 나누는 것이라고 볼 수 있다.

![paging]({{site.baseurl}}/images/paging.jpg)  

# sample source
---------------------------------------  
javascript, html, css로 구현되어 있다.

예제 소스는 아래와 같다.

~~~html

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Paging</title>

<style>
.pagination {
  display: inline-block;
}

.pagination a {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
}

</style>
</head>

<body>
    <div class="pagination">

    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {

			/*
				page_no : 현재 페이지
				pagination_count : 한번에 보여질 페이징 갯수 
				
				5개 인 경우
				EX) << 1 2 3 4 5 >>
				
				total_page : 전체 페이징 갯수
			*/
            function get_pagination(page_no, pagination_count, total_page) {
			
                let page_group = Math.ceil(page_no / pagination_count);
                let last = page_group * pagination_count;

                if(last > total_page)
                    last = total_page;
                
                const first = last - pagination_count + 1;
                return {
                    prev : (first - 1 ) < 0 ? 0 : first - 1,
                    first : first,
                    last : last,
                    next : (last < total_page) ? last+1 : 0
                }
            }
			
			function remove_all_child(node) {
				 while(node.hasChildNodes()) {
                    node.removeChild(node.firstChild);
                 }
			}

            function draw_pagination(page_no, pagination_count, total_page) {

                const page_list = get_pagination(page_no, pagination_count, total_page);
                const pagination = document.querySelector('.pagination');

                if(page_list.prev) {
                    let a = document.createElement('a');
                    a.setAttribute("href", "#");
                    a.setAttribute("id","prev");
                    a.text = '<<';

                    a.addEventListener('click', function() {
                        remove_all_child(pagination);
                        draw_pagination(page_list.prev, pagination_count, total_page);
                    });

                    pagination.appendChild(a);
                }
                
                for(let i = page_list.first; i <= page_list.last; i++) {
                    let a = document.createElement('a');
                    a.setAttribute("href", "#");
                    a.setAttribute("id",i);
                    a.text = i;

                    a.addEventListener('click', function() {
                        console.log(a.text);
                    });

                    pagination.appendChild(a);
                }

                if(page_list.next) {
                    let a = document.createElement('a');
                    a.setAttribute("href", "#");
                    a.setAttribute("id","next");
                    a.text = '>>';

                    a.addEventListener('click', function() {

                       remove_all_child(pagination);
                       draw_pagination(page_list.next, pagination_count, total_page);

                    });
                    pagination.appendChild(a);
                }
            }

            draw_pagination(1,10,28);
        });
    </script>
</body>
</html>

~~~