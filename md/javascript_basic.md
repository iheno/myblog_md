---
tags:
  - Front-end
  - Javascript
thumbnail: /img/jsbasic.jpg
---

# Javascript 기초잡기

`자바스크립트는 사용자와 상호작용을 하는 언어이다.`

자바스크립트 이벤트 헨들러들 :
onclick, onchange and so on.

## 자료형 (data type)

<ol>
  <li>Boolean</li>
  <li>number</li>
  <li>string</li>
  <li>null</li>
  <li>undefined</li>
  <li>symbol</li>
  <li>Object</li>
</ol>

## 변수와 대입연산자

`x = 1 (오른쪽 1을 왼쪽 x 에 대입한다 라는 뜻)`

## variable vs constant

`변수 바뀔수 있는 함수: 변수(variable) 바뀌지 않는 함수 : 상수 (constant)`

## 비교연산자 (Comparison operators & Boolean)

**=== 같다**

```JS index.js
1 === 1; //true
1 === 2; //false
```

**!== 같지않다**

```JS index.js
1 !== 1; //false
1 !== 2; //true
```

## 조건문 (Conditional statements)

```JS index.js
If ( ) {
 XXXXXXXXXXX
} else {
  XXXXXXXXXXXX
}
```

`If 문에는 true / false의 Boolean값이 온다 즉 Boolean값에 따라서 실행되는 순서가 바뀐다.`

```HTML index.html
<body>
  <input
    id="night_day"
    type="button"
    value="night"
    onclick="
    if(document.querySelector('#night_day').value === 'night'){
    document.querySelector('body').style.backgroundColor='black';
    document.querySelector('body').style.color='white';
    document.querySelector('#night_day').value = 'day'
    }
      else {
      document.querySelector('body').style.backgroundColor='white';
      document.querySelector('body').style.color='black';
      document.querySelector('#night_day').value = 'night'
    }
  "
 />
</body>
```

## 리팩토링 (Refactoring)

공장으로 다시 보내서 개선한다?

`자기 자신을 가리키는 ’this’를 사용`

```HTML index.html
<body>
<input
  type="button"
  value="night"
  onclick="
    if(this.value === 'night'){
    document.querySelector('body').style.backgroundColor='black';
    document.querySelector('body').style.color='white';
    this.value = 'day';
    }
      else {
      document.querySelector('body').style.backgroundColor='white';
      document.querySelector('body').style.color='black';
      this.value = 'night';
    }
  "
/>
</body>
```

**프로그래밍을 잘하는 팁 : 중복된 코드를 전부다 제거한다.**

`변수를 활용하여 document.querySelector('body’)를 target에 대입한다.`

```HTML index.html
<body>
<input
  type="button"
  value="night"
  onclick="
  const target = document.querySelector('body');
    if(this.value === 'night'){
    target.style.backgroundColor='black';
    target.style.color='white';
    this.value = 'day';
    }
      else {
      target.style.backgroundColor='white';
      target.style.color='black';
      this.value = 'night';
      }
    "
  />
</body>
```

## 배열 (Array)

집에 시간이 지날수록 살람이 늘어나게 되고 책장이나 수납상자를 사거나 방을 여러개 늘릴 수 도 있다.
프로그래밍도 마찬가지로 데이터가 많아짐에 따라 복잡해진다.

**배열 만들기 :**
`배열은 대괄호 안에 [ ] 표현 배열을 변수에 넣기 : const XXX = [1, 2, 3];`

**_배열 꺼내오기:_**

```JS index.js
const XXX = ["a", "b", "c"];

console.log(XXX[0]);
```

**_배열에 들어있는값이 몇개 인가 체크하기:_**

```JS index.js
const XXX = ["a", "b", "c"];

console.log(XXX.length);
```

**_배열에 더하기:_**

```JS index.js
const XXX = ["a", "b", "c"];

XXX.push("d");

console.log(XXX);

const pre = ["aa", "bb", "cc"];
const newData = [...pre, "dd", "ee"];
console.log(newData);
```

## 반복문 (Loop)

프로그래밍을 하다보면 반복적으로 복사&붙여넣기 할 경우가 많이 생긴다. 그것을 해결하기 위한것이 반복문이다.
예) ul li 코드

while(){} : while이라는 반복문의 키워드를 이용하기

If ( )와 마찬가지로 while ( ) 문도 true/false 같은 Boolean 이 들어간다.

`항상 반복문에서는 이 반복문이 언제 종료될 것인지 지정하는 것이 필요하다. 그렇지 않으면 무한 루프되는 지옥을 맛볼것이다.`

예졔1

```JS index.js
*
**
***
****
*****
```

```JS index.js
// print stars example 01
for(let i=0;i<5;i++){
let result = "";
for(let m=0;m<=i;m++){
result+="*";
}
document.write(result,"
");
}// print stars example 01
for(let i=0;i<5;i++){
let result = "";
for(let m=0;m<=i;m++){
result+="*";
}
document.write(result,"
");
}
```

예졔2

```JS index.js
*****
****
***
**
*
```

```JS index.js
for (let i=5; i>0; i--){
let result = "";
for (let m=0; m<i; m++){
result += "*";
}
document.write(result,"<br/>")
}
```

예졔3

```JS index.js
3*1=3
3*2=6
3*3=9
3*4=12
3*5=15
3*6=18
3*7=21
3*8=24
3*9=27
```

```JS index.js
let tables=3;
for (let i=1; i<=9; i++){
document.write(`${tables}*${i}=${tables*i}`+"<br/>")
}

```

예졔4

```JS index.js
배열의 총합구하기
```

```JS index.js
const data = [10,20,30,40,50];
let result = 0;
for (let i=0; i<data.length; i++){
result += data[i];
}
document.write(`The Array Sum are ${result}.`);
```

예졔5

```JS index.js
배열과 반복문 합성하기
```

```JS index.js
const coworkers = ["asadada", "vsvsvsvs", "cwdwdwdw", "adqwdaqwe"];

let i = 0;
while (i < coworkers.length) {
document.write(`<li>${coworkers[i]}</li>`);
i = i + 1;
}
```

예제:버튼 클릭으로 a 태그 색상변화와 백그라운드 색상 변화를 동시에 주기

```HTML index.html
<ul>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
</ul>
<input
  type="button"
  value="night"
  onclick="
  const target = document.querySelector('body');
    if(this.value === 'night'){
      target.style.backgroundColor='black';
      target.style.color='white';
      this.value = 'day';
      const blist = document.querySelectorAll('a');
      var i = 0;
      while (i < blist.length){
        blist[i].style.color = 'red';
        i = i + 1;
        }
      }
      else {
        target.style.backgroundColor='white';
        target.style.color='black';
        this.value = 'night';

        const blist = document.querySelectorAll('a');
        var i = 0;
        while (i < blist.length){
        blist[i].style.color = 'blue';
        i = i + 1;
        }
      }
    "
  />
```

## 함수(function)

예제: 함수를 이용하여 더욱 유지보수 편하게 하기

```HTML index.html
<script>
  function nightDayHandler(self) {
    const target = document.querySelector("body");
      if (self.value === "night") {
        target.style.backgroundColor = "black";
        target.style.color = "white";
        self.value = "day";

        const blist = document.querySelectorAll("a");
        var i = 0;
        while (i < blist.length) {
          blist[i].style.color = "red";
          i = i + 1;
          }
        } else {
          target.style.backgroundColor = "white";
          target.style.color = "black";
          self.value = "night";

          const blist = document.querySelectorAll("a");
          var i = 0;
          while (i < blist.length) {
          blist[i].style.color = "blue";
          i = i + 1;
          }
        }
      }
</script>
<body>
<ul>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
</ul>
<input type="button" value="night" onclick="nightDayHandler(this);" />

<script src="src/index.js"></script>
</body>
```

## 함수의 이론

`함수의 기본적인 문법:`

```HTML index.html
<ul>
  <script>
  function two() {
    document.write(`<li>2-1</li>`);
    document.write(`<li>2-2</li>`);
  }
  document.write(`<li>1</li>`);
  two();
  </script>
</ul>
```

```JS index.js
function NAME( ) {

}

NAME( ) ;

```

`함수로 만들어 더욱 심플하게`

```HTML index.html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <meta charset="UTF-8" />
  </head>
<script>
  function linksSetColor(color) {
    const blist = document.querySelectorAll("a");
    var i = 0;
    while (i < blist.length) {
    blist[i].style.color = color;
    i = i + 1;
   }
  }

  function bgSetColor(color) {
    document.querySelector("body").style.color = color;
  }

  function bgSetBackgroundColor(color) {
    document.querySelector("body").style.backgroundColor = color;
  }

  function nightDayHandler(self) {
    const target = document.querySelector("body");
    if (self.value === "night") {
    bgSetBackgroundColor("black");
    bgSetColor("white");
    self.value = "day";

    linksSetColor("red");
    } else {
      bgSetBackgroundColor("white");
      bgSetColor("black");
      self.value = "night";

      linksSetColor("blue");
    }
  }
</script>
<body>
<ul>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
</ul>
<input type="button" value="night" onclick="nightDayHandler(this);" />

<script src="src/index.js"></script>
</body>
</html>
```

## 입력 (Parameter: 매개변수 & Argument: 인자 )

```JS index.js
function sum(left, right){
document.write();
}
```

`여기서 left, right는 Parameter 즉 매개변수이다.`

```JS index.js
function sum(left, right) {
document.write(`${left + right}<br/>`);
}
sum(2, 3);
sum(3, 4);
```

`Sum(2, 3) 에서 2 와 3 은 Argument 즉 인자이다.`

## 출력 (Return)

```JS index.js
function sum2(left, right) {
return left + right;
}
document.write(sum2(2, 3) + "<br/>");
```

## 객체 (Object)

`배열 [ ] 은 순서로 데이터를 저장하는것이다. 반대로 순서없이 데이터를 저장 하는것은 바로 객체이다.`
**“객체는 바로, 이름이 있는 정리정돈 상자 "**
**객체에 속해 있는 함수는 함수라고 하지 않고 메소드(method)라고 부른다.**

**_함수명이 중복되는 것을 막는 방법은 ?
이름이 충돌되지 않도록 객체를 만든다. (폴더라는 관점)_**

# 배열은 대괄호 [ ]

# 객체는 중괄호 { }

## 객체의 생성

```HTML index.html
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
  </head>

  <h1>object</h1>
  <script>
    const coworkers = {
      programmer:"aaaaa",
      designer: "bbbbb"
    };
    document.write(`${coworkers.programmer} ${coworkers.designer}`);
  </script>
</body>
</html>
```

## 객체의 추가

이미 만들어진 객체에 객체를 추가하고 싶을때는?

```HTML index.html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <meta charset="UTF-8" />
  </head>
  <h1>object</h1>
<script>
  const coworkers = {
    programmer:"aaaaa",
    designer: "bbbbb"
  };
  document.write(`${coworkers.programmer} ${coworkers.designer}`);
  coworkers.writer = "ccccc";
  document.write(` ${coworkers.writer}`);
  coworkers["data maker"] = "dddddd"; // 띄어 쓰기가 있는 이름에는 배열을 이용해 문자열을 만든다.
  document.write(` ${coworkers["data maker"]}`);
</script>
</body>
</html>
```

## 객체를 가져오기 (반복문)

`For in`
<Br/>
ABC라는 변수가 가리키는 객체에 있는 key 값들을 가져오는 반복문

**ABC에 있는 키를 하나하나 꺼내 중괄호에 있는 코드를 실행해 주는 명령이 for다.:**

```JS index.js
for (const key in ABC){
}
```

`즉, key라는 것은 우리가 가져오고 싶은 정보에 도달할 수 있는 열쇠

반대로 배열에서는 순서대로 정렬되어 있기 때문에 key라고 표현을 하지않고
index라는 표현을 쓴다.`

## 객체의 데이터 순회하는 방법

```HTML index.html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <meta charset="UTF-8" />
  </head>
  <h1>object</h1>
<script>
  const coworkers = {
    programmer:"aaaaa",
    designer: "bbbbb"
  };
  document.write(`${coworkers.programmer} ${coworkers.designer}`);
  coworkers.writer = "ccccc";
  document.write(` ${coworkers.writer}`);
  coworkers["data maker"] = "dddddd"; // 띄어 쓰기가 있는 이름에는 배열을 이용해 문자열을 만든다.
  document.write(` ${coworkers["data maker"]}`);
</script>

<script>
  for (const key in coworkers){
    document.write('<br/>' + key + ':' + coworkers[key] +'<br/>');
  }
</script>
</body>
</html>
```

## 객체프로퍼티와 메소드

`객체에는 변수, 상수 뿐만아니라 함수도 담을 수 있다.`

```JS index.js
coworkers.showAll = function(){

}

```

위에와 같은 표현 방식

```JS index.js
function showAll() {
}
```

## 객체에 소속된 함수 만들기

```HTML index.html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <meta charset="UTF-8" />
  </head>
  <h1>object</h1>
<script>
  const coworkers = {
    programmer:"aaaaa",
    designer: "bbbbb"
  };
  document.write(`${coworkers.programmer} ${coworkers.designer}`);
  coworkers.writer = "ccccc";
  document.write(` ${coworkers.writer}`);
  coworkers["data maker"] = "dddddd"; // 띄어 쓰기가 있는 이름에는 배열을 이용해 문자열을 만든다.
  document.write(` ${coworkers["data maker"]}`);
</script>

<script>
  for (const key in coworkers){
    document.write('<br/>' + key + ':' + coworkers[key] +'<br/>');
  }
</script>

<h2>property and method</h2>
<script>
  coworkers.showAll = function(){
    for (const key in this){
    document.write('<br/>' + key + ':' + this[key] +'<br/>');
    }
  }
  coworkers.showAll();
</script>
</body>
</html>
```

`coworkers.showAll(); // showAll 은 메소드`<br/>
`이 와 같이 객체에 소속된 함수를 메소드라고 한다. 또한 객체에 소속된 변수(programmer, designer…등)를 프로퍼티라고 부른다.`

_객체는 객체의 프로퍼티와 프로퍼티를 구분 할때 콤마를 찍는다._

## 객체의 활용

```HTML index.html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <meta charset="UTF-8" />
  </head>
<script>
  const Links = {
    setColor: function(color) {
  const blist = document.querySelectorAll("a");
  var i = 0;
    while (i < blist.length) {
      blist[i].style.color = color;
      i = i + 1;
      }
    }
  };

  const Bg = {
    setColor: function(color) {
    document.querySelector("body").style.color = color;
    },
    setBackgroundColor: function(color) {
    document.querySelector("body").style.backgroundColor = color;
    }
  };

  function nightDayHandler(self) {
    const target = document.querySelector("body");
    if (self.value === "night") {
      Bg.setBackgroundColor("black");
      Bg.setColor("white");
      self.value = "day";

    Links.setColor("red");
    } else {
      Bg.setBackgroundColor("white");
      Bg.setColor("black");
      self.value = "night";

      Links.setColor("blue");
    }
  }
</script>
<body>
<ul>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
  <li><a href="#">aaaa</a></li>
</ul>
<input type="button" value="night" onclick="nightDayHandler(this);" />

<script src="src/index.js"></script>
</body>
</html>
```

**추가 공부할 검색어 (문제에 닥쳤을때)**

<ol>
  <li>Document (객체)</li>
  <li>Dom (다큐먼트객체는 돔의 일부)</li>
  <li>window (웹브라우저 자체를 제어하려면 윈도우 객체를 조사한다)</li>
  <li>ajax (웹페이지를 리로드하지 않고 정보를 변경하고 싶다면)</li>
  <li>cookie (웹페이지가 리로드 되어도 현재 상태를 유지하고 싶다면)</li>
  <li>Offline web application (인터넷이 끊겨도 동작하게 하려면)</li>
  <li>webRTC (화상통신 웹 앱을 만들고 싶다면)</li>
  <li>speech (사용자의 음성을 인식하고 음성으로 정보를 전달하고 싶다면)</li>
  <li>webGL (3차원 그래픽으로 게임과 같은 것을 만들고 싶다면)</li>
  <li>webVR (가상 현실에 관심이 많다면)</li>
</ol>
