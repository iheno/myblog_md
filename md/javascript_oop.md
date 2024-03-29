---
tags:
  - Front-end
  - Javascript
thumbnail: /img/jsoop.png
---

# Javascript 객체 지향 프로그래밍

`서로 연관된 변수와 함수를 그룹핑하고 이름을 붙인 것`

## 배열과 객체를 만들고, 값을 읽는 법

```JS index.js
const memberArray = ["AAA", "BBB", "CCC"];
console.log("memberArray[2]", memberArray[2]);

//객체
const memberObject = {
  manager: "AAA",
  developer: "BBB",
  designer: "CCC"
};

memberObject.designer = "CCCC"; //객체 이름 수정
console.log("memberObject.designer", memberObject.designer);
console.log("memberObject['designer']", memberObject["designer"]);

delete memberObject.manager;
console.log("delete memberObject.manager", memberObject.manager);

```

-> result

```memberArray[2]
CCC
memberObject.designer
CCCC
memberObject['designer']
CCCC
delete memberObject.manager

- undefined
```

## 반복문을 이용해서 객체의 모든 값에 적근하는 방법

```JS index.js
const memberArray = ["AAA", "BBB", "CCC"];
console.group("array loop");

let i = 0;
while (i < memberArray.length) {
  console.log(i, memberArray[i]);
  i = i + 1;
}

console.groupEnd("array loop");
const memberObject = {
  manager: "AAA",
  developer: "BBB",
  designer: "CCC"
};
console.group("object loop");
  for (let name in memberObject) {
  console.log(name, memberObject[name]);
  }
console.groupEnd("object loop");
```

-> result

```
0
"AAA"
1
"BBB"
2
"CCC"
manager
AAA
developer
BBB
designer
CCC
```

## #객체를 실제로 활용하는 사례

**_수학적 객체_**

```JS index.js
console.log(Math.PI);
console.log(Math.random());
console.log(Math.floor(3.9));
```

## 객체를 만들어서 연관된 변수와 함수를 정리 정돈

```JS index.js
console.log("Math.PI", Math.PI);
console.log("Math,random()", Math.random()); //method
console.log("Math.floor(3.9)", Math.floor(3.9));

const MyMath = {
  PI: Math.PI,
  random: function() {
  return Math.random();
  },
  floor: function(val) {
  return Math.floor(val);
  }
};

console.log("MyMath.PI", MyMath.PI);
console.log("MyMath.random()", MyMath.random());
console.log("MyMath.floor(3.9)", MyMath.floor(3.9));

const MyMath_PI = Math.PI;
  function MyMath_random() {
  return Math.random();
  }
  function MyMath_floor(val) {
  return Math.floor(val);
  }

console.log(MyMath_PI);
```

# ’This’

`메소드 내에서 메소드가 속한 객체를 참조 할 때 사용하는 키워드인 this에 대해서 알아보기`<br/>
**_자기 자신을 가리키는 대명사 ’this’_**

```JS index.js
const Kim = {
  name: "kim",
  first: 10,
  second: 20,
  sum: function() {
  return this.first + this.second;
  }
};

console.log(Kim.sum());
```

-> result

```
30
```

## 객체를 수동으로 만드는 가내수공업에서 벗어나서 객체를 자동으로 찍어내는 공장인 constructor을 만들어보자

**_가내수공업으로 객체를 만들 때의 단점_**

```JS index.js
const kim = {
  name: "kim",
  first: 10,
  second: 20,
  third: 30,
  sum: function() {
  return this.first + this.second + this.third;
  }
};

const lee = {
  name: "lee",
  first: 10,
  second: 10,
  third: 10,
  sum: function() {
  return this.first + this.second + this.third;
  }
};

console.log(kim.sum());
console.log(lee.sum());
```

**_내장된 객체를 통해서 객체 공장의 쓰임을 체험_**

```JS index.js
const kim = {
  name: "kim",
  first: 10,
  second: 20,
  third: 30,
  sum: function() {
  return this.first + this.second + this.third;
  }
};

const lee = {
  name: "lee",
  first: 10,
  second: 10,
  third: 10,
  sum: function() {
  return this.first + this.second + this.third;
  }
};

console.log(kim.sum());
console.log(lee.sum());

const d1 = new Date("2019-12-25");
console.log(d1.getFullYear());
console.log(d1.getMonth() + 1); // 0 ,1, 2, 3...
```

**_Constructor function 만들기(construct function : 생성자함수)_**

```JS index.js
function Person(name, first, second, third) {
  this.name = name;
  this.first = first;
  this.second = second;
  this.third = third;
  this.sum = function() {
  return this.first + this.second + this.third;
  };
}

const kim = new Person("kim", 10, 20, 30);
const lee = new Person("lee", 10, 10, 10);
console.log(kim.sum());
console.log(lee.sum());
```

-> result

```
60
30
```

## Prototype

`JavaScript의 prototype이 필요한 이유와 prototype을 통해서 코드의 재사용성과 성능을 향상시키는 방법`
<br/>
**_prototype을 이용해서 코드의 재사용성을 높이고, 성능을 향상시키는 방법_**

```JS index.js
function Person(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
}

Person.prototype.sum = function() {
  return `prototype : ` + (this.first + this.second);
};
//성능과 메모리 절약뿐 아니라 유지보수가 싶다

const kim = new Person("kim", 10, 20);
  kim.sum = function() {
  return `this : ` + (this.first + this.second);
};
//재정의도 가능하다
const lee = new Person("lee", 10, 10);
console.log(kim.sum());
console.log(lee.sum());

```

## class

`클래스에서 생성자 함수를 구현하는 방법`
<br/>

```JS index.js
class Person {
  constructor(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
  }
}

const kim = new Person("kim", 10, 20);
console.log(kim);
```

## class에서 객체의 method 구현하기

```JS index.js
class Person {
  constructor(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
}
  sum() {
  return `prototype : ` + (this.first + this.second);
  }
}

const kim = new Person("kim", 10, 20);
  kim.sum = function() {
  return `this : ` + (this.first + this.second);
};
const lee = new Person("lee", 10, 10);
console.log(kim.sum());
console.log(lee.sum());
```

## class 상속

`클래스를 상속해서 서브 클래스를 만드는 방법`<br/>

```JS index.js
class Person {
  constructor(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
  }
  sum() {
  return this.first + this.second;
  }
}

class PersonPlus extends Person {
  avg() {
  return (this.first + this.second) / 2;
  }
}

const kim = new PersonPlus("kim", 10, 20);
console.log(kim.sum());
console.log(kim.avg());
```

## super

`부모 클래스에게 일을 시키고 부모가 하지 못하는 일은 나만 하도록 하는 키워드가 super 다.`
</br>
**_super( ) 에서 ( ) 안에는 부모 클래스에서의 생성자를 넣는다._**

```JS index.js
class Person {
  constructor(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
  }
  sum() {
  return this.first + this.second;
  }
}

class PersonPlus extends Person {
  constructor(name, first, second, third) {
  super(name, first, second);
  this.third = third;
  }
    sum() {
    return super.sum() + this.third;
  }
    avg() {
    return (this.first + this.second + this.third) / 3;
  }
}

const kim = new PersonPlus("kim", 10, 20, 30);
console.log(kim.sum()); // 60
console.log(kim.avg()); // 20
```

## 객체간의 상속

`1.proptotype(__proto__)을 이용해서 상속을 구현`

```JS index.js
const superObj = { superVal: "super" };
const subObj = { subVal: "sub" };
subObj.__proto__ = superObj; //subObj 가 superObj의 자식이다.

console.log(subObj.subVal);
console.log(subObj.superVal);

subObj.superVal = "sub";
console.log(superObj.superVal);

// sub super super
```

`2.Object.create를 이용해서 __proto__를 대체하는 방법`

```JS index.js
const superObj = { superVal: "super" };

const subObj = Object.create(superObj);
subObj.subVal = "sub";
debugger;

console.log(subObj.subVal); //sub
console.log(subObj.superVal); //super
subObj.superVal = "sub";
console.log(superObj.superVal); //super
```

`예제)`

```JS index.js
const superObj = { superVal: "super" };

const subObj = Object.create(superObj);
subObj.subVal = "sub";
debugger;

console.log(subObj.subVal); //sub
console.log(subObj.superVal); //super
subObj.superVal = "sub";
console.log(superObj.superVal); //super

const kim = {
  name: "kim",
  first: 10,
  second: 20,
  sum: function() {
  return this.first + this.second;
  }
};

// const lee = {
// name: "lee",
// first: 10,
// second: 10,
// avg: function() {
// return (this.first + this.second) / 2;
// }
// };

// lee.__proto__ = kim;

const lee = Object.create(kim);
  lee.name = "lee";
  lee.first = 10;
  lee.second = 10;
  lee.avg = function() {
  return (this.first + this.second) / 2;
};

console.log(lee.sum());
console.log(lee.avg());
```

## 객체와 함수

`자바스크립트는에서 함수는 혼자 있으면 개인이고, new가 앞에 있으면 객체를 만드는 신이고, call을 뒤에 붙이면 용병이고, bind를 붙이면 분신술을 부리는 놀라운 존재입니다.`<br/>

### 1. call을 통해서 실행할 때마다 this의 값을 변경하는 방법

```JS index.js
const kim = { name: "kim", first: 10, second: 20 };
const lee = { name: "lee", first: 10, second: 10 };

function sum(prefix) {
return prefix + (this.first + this.second);
}

// sum();
console.log(sum.call(kim, "=>")); // =>30
console.log(sum.call(lee, ":")); // :20
```

### 2. bind를 통해서 독립적이면서도 특정 객체의 메소드 역할을 할 수 있는 함수 만들기

```JS index.js
const kim = { name: "kim", first: 10, second: 20 };
const lee = { name: "lee", first: 10, second: 10 };

function sum(item) {
return item + (this.first + this.second);
}

// sum();
console.log(sum.call(kim, "=>"));
console.log(sum.call(lee, ":"));

const kimSum = sum.bind(kim, "->");
console.log(kimSum()); // ->30
```
