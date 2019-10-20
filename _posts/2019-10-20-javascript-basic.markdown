---
layout: post
title: javascript hoisting, lexical environment, execute context, this binding
description: javascript 기본기 다지기
categories: javascript
---

### 함수 선언식 및 함수 표현식  
javascript에서 함수를 정의하는 함수 선언과 동시에 할당하는 '함수 선언식', 
선언과 할당이 나뉘어 있는 '함수 표현식' 있다.  

함수 선언식은 호이스팅에 영향을 받지만, 함수 표현식은 그렇지 않다. 
함수 정의 전에 함수가 호출될수 있어 내부 로직이 복잡해 질수 있다. 따라서 '함수 표현식'
사용을 권장하고 있다.

**예제**  
~~~javascript  
world(); //error
hello(); //hello

function hello() {
    console.log('hello');
}

var world = function() {
    console.log('world');
}
~~~  

### Hoisting  
Hoisting의 사전적 정의는 '끌어올리다' 라는 의미이다.  
javascript에서 Hoisting은 변수가 정의된 범위에 따라 선언과 할당으로 분리되어 정의된
영역에서 최상위로 끌어올려지는 것을 말한다.
즉 함수안에서는 함수의 최상위로, 전역 공간에 정의되었다면 전역 컨텍스트의 최상위로 올려진다.

**예제**  
~~~javascript  
world(); //error
hello(); //hello
console.log(test); //undefined
var test = 10;
console.log(test); //10

~~~  

