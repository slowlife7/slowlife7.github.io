---
layout: post
title: for loop 에서 var와 let의 차이
description: var와 let의 스코프 차이
categories: javascript
---

### for loop 에서 let 과 var 차이  

# var 사용
~~~javascript
    for(var i = 0; i < 5; i++) {
	    setTimeout(function() { console.log(i); }, i * 1000);
    }
    //결과 
    //4
    //4
    //4
    //4
    //4
~~~

# let 사용
~~~ javascript
    for(let i = 0; i < 5; i++) {
	    setTimeout(function() { console.log(i); }, i * 1000);
    }
    //결과 
    //0
    //1
    //2
    //3
    //4
~~~

### 출력 결과의 차이?  
결과적으로 var 는 function scopde, let 은 block scope를 사용하기 때문이다.  

var은 loop가 실행될때 function scope로 같은 변수 i 를 참조하고 있다.
loop가 끝나고 setTimeout이 호출될때 i 는 이미 4 값을 가지고 있다.  

let은 loop가 실행될때 block scope로 setTimeout 실행시 새로운 값으로 binding 된다.

### var 로 let과 동일하게 출력하기  

var의 function scope를 이용하여 아래와 같이 변경하면 하나의 값을 참조하는 것이
아니라 복사된 값을 참조하게 된다.

~~~javascript
for(var i = 0; i < 5; i++) {
	(function(arg) {
		setTimeout(function() { console.log(arg); }, arg * 1000);
	})(i);
}
~~~

