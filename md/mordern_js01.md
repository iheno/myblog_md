---
title: mordern_js01
date: 2019-11-20 13:56:20
tags:
  - Front-end
  - Javascript
thumbnail: /img/modernjs.png
---

## 모던 자바스크립트 - 01

## Scope

`const를 기본으로 사용한다. 그런데 변경이 될 수 있는 변수는 let 을 사용한다. var는 사용하지 않는다.`

**const를 사용하더라도 배열과 오브젝트의 값을 변경하는 것은 가능하다.**

```JS index.js
function home() {
  const list = ["apple", "orgnge", "apple"];
  list.push("banana");
  console.log(list);
}

home();
```

-> ["apple", "orgnge", "apple", "banana”]

**_immutable array를 어떻게 만를지?_**

```JS index.js
function home() {
const list = ["apple", "orgnge", "apple"];
lists = [].concat(list, "banana");
console.log(list, lists);
}

home();
```

## String

```JS index.js
const str = "hello world ! ^^ ~~";
const matchstr = "hello";
console.log(str.startsWith(matchstr));
//true
console.log(str.endsWith(matchstr));
//false
console.log(str.includes("world"));
//true
```

## Array

### use forEach

```JS index.js
const data = [1, 2, undefined, NaN, null, ""];
  data.forEach(value => {
  console.log("value is", value);
  }
);
```

###for in \*Don't use [Array]

```JS index.js
const data = [1, 2, undefined, NaN, null, ""];
  for (const idx in data) {
  console.log(data[idx]);
}
//1 , 2, undefined, NaN, null, ""
```

### for of

```JS index.js
const data = [1, 2, undefined, NaN, null, ""];
  for (const value of data) {
  console.log(value);
}
//1, 2, undefined, NaN, null, ""

const str = "hello world";
  for (const value of str) {
  console.log(value);
}
// h e l l o w o r l d
```

### spread operator - array (펼침연산자)

```JS index.js
const pre = ["apple", "orange", 100];
const newData = [...pre];
console.log(pre, newData);
```

-> ["apple", "orange", 100]["apple", "orange", 100]

**…pre -> pre를 펼쳐준다.**

1. add

```JS index.js
const pre = [100, 200, "hello", null];
const newData = [0, 1, 2, 3, 4, ...pre, 5];
console.log(newData);
// 0 ,1, 2, 3, 4, 100, 200, "hello", null ,5
```

2. sum

```JS index.js
// function sum(a, b, c) {
// return a + b + c;
// }

const sum = (a, b, c) => {
return a + b + c;
};

const pre = [100, 200, 300];
console.log(sum.apply(null, pre)); //이전 방법
console.log(sum(...pre)); //요즘 방법

// 600 600
```

3. from method (from메서드로 진짜 배열 만들기)

```JS index.js
// function addMark() {
// const newArray = Array.from(arguments);
// const newData = newArray.map(function(value) {
// return value + "!";
// });
// console.log(newData);
// }

// addMark(1, 2, 3, 4, 5, 6, 7, 8, 9);

function addMark() {
const newArray = Array.from(arguments);
const newData = newArray.map(value => value + "!");
console.log(newData);
}

addMark(1, 2, 3, 4, 5, 6, 7, 8, 9);
```

**_filter, includes, from을 사용해서 문자열 ‘e’가 포함된 노드로 구성된 배열을 만들어서 반환하기_**

```JS index.js
function print() {
let list = document.querySelectorAll("li");
// console.log(toString.call(list)); // 자바스크립트에서 타입체크할때 많이 쓰는 방법
// console.log(typeof list);
let listArray = Array.from(list); //li node로 구성된 배열
// console.log(toString.call(listArray));
let eArray = listArray.filter(v => v.innerText.includes("e"));
console.log(eArray.length);
}
print();
```

**간단히 객체 생성하기**

```JS index.js
const name = "heno";
const age = 33;

const obj = {
name: name,
age: age
};

console.log(obj);
```

## Destructuring

### Destructuring Array

```JS index.js
const data = ["a", "b", "c", "d", "e"];
// const aae = data[0];
// const bbb = data[2];

const [aaa, , bbb] = data; // 가운데 스페이스로 건너뛰기
console.log(aaa, bbb);
```

-> a c

### Destructuring Object

```JS index.js
const obj = {
name: "aaa",
address: "Tokyo",
age: 30
};

// const { name, age } = obj;
// console.log(name, age);

const { name: myName, age: myAge } = obj; // 다른 이름으로 할당
console.log(myName, myAge);
```

### Destructuring활용 JSON파싱

```JS index.js
{
title: "News",
newlist: ["aaaaaaaaaaaa", "bbbbbbbbbbbb", "cccccccccccc", "dddddddddddd"]
},
{
title: "Blogs",
newlist: [
"sasasasasassa",
"rarararararar",
"cdcdcdcddcdcd",
"qwqwqwqwqwqwq"
]
}
];

// 두 번째 항목만 따로 뽑겠다.

// const [, Blogs] = what;
// const { title } = Blogs;
// console.log(title);

const [, { title }] = what;
console.log(title);
```

### Destructuring Event

```JS index.js
// document
// .querySelector(".aaa")
// .addEventListener("click", function({ type, target }) {
// console.log(type, target.innerText);
// });

document
.querySelector(".aaa")
.addEventListener("click", ({ type, target }) =>
console.log(type, target.innerText)
);
```

## Set

```JS index.js
const mySet = new Set();
// console.log(toString.call(mySet));

mySet.add("aaa");
mySet.add("bbb");
mySet.add("aaa");

// console.log(mySet.has("aaa")); //check values
// 증복된 값을 제외하고 반환
mySet.forEach(v => console.log(v));
```

-> aaa bbb

```JS index.js
const mySet = new Set();
// console.log(toString.call(mySet));

mySet.add("aaa");
mySet.add("bbb");
mySet.add("aaa");

mySet.delete("aaa");

mySet.forEach(v => console.log(v));

```

-> aaa
