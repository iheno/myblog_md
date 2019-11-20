---
title: ES6 문법 훑어보기
date: 2019-11-20 13:56:20
tags:
  - Front-end
  - Javascript
thumbnail: /img/es6.png
---

## ES6의 정석

## 1 Variables

### 1.1 const and let

**const : 변하지 않는 값**

```JS index.js
const name = “heno”;
```

**let : 이전의 var와 같은 것 (값을 변경해야 한다면 let을 사용)**

```JS index.js
let heno = “las”;
heno = “lalala”;
```

// 가능하면 default로 모두 const를 사용하길 권장 절대 var는 사용하지 말기

### 1.2 Temporal dead zone

```JS index.js
var myName = “heno”

console.log(myName);
```

-> heno

if I changed this :

```JS index.js
console.log(myName);

var myName = “heno”
```

-> undefined (이론상으로 존재하지 않는 걸 console.log로 출력하려 한 것)

if I changed let :

```JS index.js
console.log(myName);

let myName = “heno”
```

-> myName is not defined (error)
// 이것이 let의 temporal dead zone이다.

### 1.3 Block Scope

let과 const의 또 다른 장점은 block scope가 있다는 점이다.

scope는 기본적으로 버블이다. 이 버블이 variable들이 접근
가능한지 아닌지를 감지해준다.

```JS index.js
if (true) {
  const hello = "hi";
}

console.log(hello);

// hello is not defined
```

const 와 let 은 모두다 block scope로 되어있다.
이 말의 뜻은 그 block 안에서만 존재한다.
블록은 { } 이것으로 만들어져 있다.
즉 대괄호 밖의 hello 는 존재하지 않는다.

**그러나 var를 쓰면**

```JS index.js
if (true) {
  var hello = "hi";
}
console.log(hello);

// hi
```

var에는 block scope같은게 없다.
if 나 while, for 구문안에서 var로 변수를 만들 수 있다.
var 는 function scope를 가지고 있다. (var가 function안에서 접근할 수 있다는 뜻)

### 1.4 The future of ‘var'

var를 계속 사용하는 이유가 기존의 많은 웹사이트가 var로 구성되어있기 때문에, 좋아서가 아니라 바꿀 수 가 없기 때문에 아직도 var를 쓴다.
하지만 앞으로는 절대 var를 사용하지 않는 것을 권장.
\*let 은 앞으로 변경될 것이고, const는 default로 변경되지 않을것이다.

## 2 Functions

### 2.1 Arrow Functions

**Arrow function은 자바스크립트에서 함수의 모습을 개선한 것이다.**

-기존 function의 구조

```JS index.js
function name() {
}

const hello = function(arg){
}
```

-개선된 function의 구조

**예) 바꾸기 전**
map은 각각의 아이템마다 함수를 호출하는 일을 한다.

```JS index.js
const names = ["a-", "b-", "c-"];

function addHeart(item) {
  return item + "heart";
}
const heart = names.map(addHeart);

console.log(heart);
```

**예) 바뀐 후**
but 요즘에는 다른 함수를 만들어 넣지 않는다.

```JS index.js
const names = ["a-", "b-", "c-"];

const heart = names.map(function(item) {
  return item + "heart";
});

console.log(heart);
```

**arrow function 사용**

1. 첫번째 function을 없애고

```JS index.js
const heart = names.map((item) {
  return item + "heart";
});
```

2. 제거한 function을 =>로 대체

```JS index.js
const heart = names.map((item) => {
  return item + "heart";
});
```

3. 최종 () 제거

```JS index.js
const heart = names.map(item => {
  return item + "heart";
});
```

4. Implicit return (같은 줄에 뭘 적든 간에 리턴이 된다는 뜻)
   \*{} 를 추가 하는 순간 Implicit return은 사라진다

```JS index.js
const heart = names.map(item => item + "heart");
```

기본형:
**XXX = () => {};**

### 2.2 ’This’ in Arrow Functions

1. 대부분의 경우에 Arrow function은 자바크립트에서 사용가능하지만 this키워드를 사용할 경우는 예외다.
2. Arrow functions은 this를 이벤트로 부터 가지고 있지 않다.(window object로 가지고 있다.)

**this 는 현재 실행 문맥이다**

3. 실행문맥이란 말은 호출자가 누구냐는 것과 같습니다.

### 2.3 Arrow Functions in the Real World

**find**
Before arrow :

```JS index.js
const email = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

const foundMail = email.find(function(item) {
  return item.includes("@gmail.com");
});

console.log(foundMail);
```

After arrow :

```JS index.js
const email = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

const foundMail = email.find(item => item.includes("@gmail.com"));

console.log(foundMail);
```

**filter**
Filter 메소드는 제공된 함수의 조건을 만족한 모든 엘리먼트로 새로운 Array를 만든다. 그렇기 때문에 첫번째 엘리먼트 뿐만이 아니라
모든 엘리먼트를 반환한다.

예) 지메일이 아닌 모든 메일을 반환하라:

```JS index.js
const emails = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

const noGmail = emails.filter(email => !email.includes("@gmail"));

console.log(noGmail);
```

**forEach**
각 array의 엘리먼트 마다 제공된 함수를 실행한다.
예) 유저의 이름만 얻자 (array함수에선 현재 값을 나타내므로 current value를 사용한다)

**_멋진 메소드 split 사용 : split는 뭔가를 나누는 것이다._**

배열의 첫번째 것만 가져와서 메일의 유저이름만 가져오게 하기 :

```JS index.js
const emails = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

emails.forEach(email => {
  console.log(email.split("@")[0]);
});
```

**map**

```JS index.js
const emails = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

const cleaned = emails.map(email => email.split("@")[0]);

console.log(cleaned);
```

**_보너스 : 값만 리턴하는것이 아니라 오브젝트를 리턴시킬 경우 (이름 뿐만 아니라 순서까지 리턴 시킬 경우)_**

**{} 안에 있으므로 리턴이 되지 않는다.**

```JS index.js
const emails = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

const cleaned = emails.map((email, index) => {
  username: email.split("@")[0], index;
});

console.log(cleaned);
```

**object를 return 할 수 있는 방법: 대괄호 밖에 괄호를 넣어준다.**\

```JS index.js
const emails = [
  "quruquru80@naver.com",
  "henojiwu@gmail.com",
  "rodelheno@gmail.com",
  "21-coka@daum.net"
];

const cleaned = emails.map((email, index) => ({
  username: email.split("@")[0],
  position: index
}));

console.table(cleaned);
```

### 2.4 Default Values

기본적인 function:

```JS index.js
function sayHi(aName) {
  return "hello" + aName;
}

console.log(sayHi());
```

Use Default Values:

```JS index.js
function sayHi(aName = "Rodel") {
  return "hello" + aName;
}

console.log(sayHi());
```

Arrow function 으로 Default Values:

```JS index.js
const sayHi = (aName = "rodel") => "hello" + aName;

console.log(sayHi());
```

## 3 Strings

### 3.1 Sexy Strings

**Template literas**
문자열 안에 + 가 많아지고 , “로 열었다가 “닫았다가 하는 복잡한 예 :

```JS index.js
const sayHi = (aName = "rodel") => "hello " + aName + " lovely to have you";

console.log(sayHi());
```

**개선안**
**_Use `` and string_**

```JS index.js
const sayHi = (aName = "rodel") => `hello ${aName} lovely to have you`;

console.log(sayHi());
```

**_Template literas 에서는 sexy quotes -> `` 를 쓰도록!_**

**String 안에서 function을 실행시켜보기**

```JS index.js
const add = (a, b) => a + b;

console.log(`hello how atre you ${add(6, 6)}`);
```

### 3.2 HTML Fragments

**자바스크립트안에서 HTML사용하기**

```JS index.js
const wrapper = document.querySelector(".wrapper");

const addWelcome = () => {
  const something = document.createElement("div");
  const whatever = document.createElement("h1");
  whatever.innerText = "hello";
  something.append(whatever);
  wrapper.append(something);
};

setTimeout(addWelcome, 5000);
```

**Template literal string으로 만들기 (HTML이 좀더 복잡해 졌을 경우)**

```JS index.js
const wrapper = document.querySelector(".wrapper");

const addWelcome = () => {
  const something = `
  <div class="hello">
    <h1 class="title">Hello</h1>
  </div>
`;

  wrapper.innerHTML = something;
};

setTimeout(addWelcome, 5000);
```

### 3.3 HTML Fragments part Two

**배열로 친구들 목록 만들기**

기본 예:

```JS index.js
const wrapper = document.querySelector(".wrapper");

const friends = ["me", "you", "he", "she", "they"];

const ul = document.createElement("ul");

friends.forEach(friend => ul.append(`<li>${friend}</li>`));

wrapper.append(ul);
```

Template literal 사용 예 (Map은 무엇을 리턴하던지 그 값을 배열로 만든다)

\*결과 값에 [,] 가 나오는데 map을 썼기 때문에 배열로 정리되서 그런거다. [,]를 지우기 위해서 join함수를 쓴다.

```JS index.js
const wrapper = document.querySelector(".wrapper");

const friends = ["me", "you", "he", "she", "they"];

const list = `
  <h1>Prople I love</h1>
  <ul>
    ${friends.map(friend => `<li>${friend}</li>`).join("")}
  </ul>
`;

wrapper.innerHTML = list;
```

### 3.4 Cloning Styled Components

**_Styled component 는 리액트를 위한 라이브러리다_**

**_Error_**

```JS index.js
const styled = aElement => {
  const el = document.createElement(aElement); // 호출
    return el; // 리턴
 };

  const title = styled("h1")`
    border-radius: 10px;
    color: blue;
  `;
console.log(title);
```

**_fuction 안에 fuction을 리턴하기_**

```JS index.js
const styled = A => {
const el = document.createElement(A); // 호출
  return args => {
  // console.log(args[0]);
   const styles = args[0];
    el.style = styles;
    return el;
  };
};

const title = styled("h1")`
  border-radius: 10px;
  background-color: red;
  color: white;
`;

const subtitle = styled("span")`
  color: black;
`;

title.innerText = "We just clone styled componet";
subtitle.innerText = "Yep! i got it!"

document.body.append(title, subtitle);
```

### 3.5 More String Improvements!

**3 가지 쿨한 string 메소드**

1. include

```JS index.js
const isEmail = email => email.includes("@gmail");

console.log(isEmail("heno@gmail.com"));
```

2. repeat (string.repeat 는 어떤 문자도 반복할 수 있디)

```JS index.js
const CC_NUM = "4890";

const displayName = `${"*".repeat(10)}${CC_NUM}`;

console.log(displayName);
```

3. startsWith (유효성 체크에 사용할 수 있다)

```JS index.js
const name = "Mr. Heno";

console.log(name.startsWith("Mr."));
console.log(name.endsWith("Heno"));
```

## 4 Array

### 4.1 Array.from() and Array.of()

**Array.of**
어떤걸 배열로 만들때 사용

**_평범한 배열:_**

```JS index.js
const friends = ["heno", "atsuko", "jiu", "anton"];
```

**_Array.of:_**

```JS index.js
const friends = Array.of("heno", "atsuko", "jiu", "anton");
console.log(friends);
```

**Array.from**
Html 에 버튼을 여러개 만들고 각각의 버튼에 이벤트리스너를 붙이기 \*가끔 html에서 array를 얻지 못하고, array-like object를 얻는다.
그러면 에러가 난다.
그럴때 쓰는것이 Array.from() 이다. -> array and array-like object의 차이

```JS index.js
const buttons = document.getElementsByClassName("btn");

Array.from(buttons).forEach(button => {
  button.addEventListener("click", () => console.log("I clicked"));
});
```

Also,

```JS index.js
const buttons = document.getElementsByClassName("btn");

const arg = Array.from(buttons);
  arg.forEach(button => {
  button.addEventListener("click", () => console.log("I clicked"));
});
```

### 4.2 Array.find() / Array.findIndex() / Array.fill()

**find()**
ind() 에는 조건이 필요하다:

```JS index.js
const friends = [
  "henojiwu@gmail.com",
  "quruquru80@gmail.com",
  "wwesttune818@hotmail.com",
  "21c-coka@daum.net"
];

const target = friends.find(freind => freind.includes("@daum"));

console.log(target);
```

**findIndex()**

```JS index.js
const friends = [
  "henojiwu@gmail.com",
  "quruquru80@gmail.com",
  "wwesttune818@hotmail.com",
  "21c-coka@daaum.net"
];

// @daaum을 체크한다
const check = () => friends.findIndex(freind => freind.includes("@daaum"));

// 그러면 타겟을 얻게 된다.이 타겟은 @daaum인 사람의 index다
let target = check();

// 만약에 찾았다면 콘솔로그
console.log(target);

// 그리고 usernameㅡㄹ 가져올건데, 문자열을 @로 쪼개고 첫번째 파트만 가져온다
const username = friends[target].split("@")[0];

//그리고 email을 수정하고
const email = "daum.net";

// 그리고 합쳐준다.
friends[target] = `${username}@${email}`;

//고친후 확인
target = check();

//반환
console.log(target);
```

**_-> 좀더 간결한 코드:_**

```JS index.js
const friends = [
  "henojiwu@gmail.com",
  "quruquru80@gmail.com",
  "wwesttune818@hotmail.com",
  "21c-coka@daaum.net"
];

const check = () => friends.findIndex(freind => freind.includes("@daaum"));
let target = check();
if (target !== -1) {
  console.log(target);
  const username = friends[target].split("@")[0];
  const email = "daum.net";
  friends[target] = `${username}@${email}`;
  target = check();
}

console.log(target);
console.log(friends);
```

결과: 만약 -1이니면 3을 출력, 그리고 -1을 반환
21c-coka@daaum -> 21c-cola@daum으로 수정

**fill()**
fill은 array를 채우는 것이다 시작 index부터 마지막 index까지 static value로…

```JS index.js
const friends = [
  "henojiwu@gmail.com",
  "quruquru80@gmail.com",
  "wwesttune818@hotmail.com",
  "21c-coka@daaum.net"
];

friends.fill("*".repeat(8), 0, 3); // 첫번째 부터 3번째까지

console.log(friends);
```

## 5 Destructuring

destructuring 은 object나 array, 그 외 요소들 안의 변수를 바깥으로 끄집어 내서 사용할 수 있도록 하는것

### 5.1 Object Destructuring

**기본 사용방법**

```JS index.js
const setting = {
  notifications: {
  follow: true,
  alert: true,
  unfollow: false
  },
  color: {
  theme: "dark"
  }
};

// 만약 유저의 notifications에 alerts가 true로 되어있을 때, follow도 true로 된 상황이면 이메일을 전송

// // 구 버전
// if(setting.notifications.follow){
// // send email
// }

// use destructuring
const {
  notifications: { follow },
  color
  } = setting;

console.log(follow, color);
```

**If 대신 사용 할 수 있는 one-line-statement**
(Setting 안의 notifications로가서 follow가 있는지 찾아보고 없다면 follow = false를 선언,그리고 notifications자체가 없다면 notification는 빈 object가 된다 )

```JS index.js
// use destructuring
const { notifications: { follow = false } = {} } = setting;
```

### 5.2 Array Destructuring

가져온 데이터를 조작할 필요없을 때 사용하면 좋다 (예: 수정 할수 없는 외부 API)

**요일 array : Not Sexy**

```JS index.js
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

// 이 중에서 앞의 세개만 가져오려면?
const mon = days[0];
const tue = days[1];
const wed = days[2];

console.log(mon, tue, wed);
```

**개선된**

```JS index.js
const days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

// 이 중에서 앞의 세개만 가져오려면?
const [mon, tue, wed] = days;

console.log(mon, tue, wed);
```

**또 다른 버젼**

```JS index.js
const days = () => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

// 이 중에서 앞의 세개만 가져오려면?
const [mon, tue, wed] = days();

console.log(mon, tue, wed);
```

### 5.3 Renaming

Object Destructuring은 그대로 유지하고 변수명을 변경하는 방법

**Before:**

```JS index.js
const setting = {
  color: {
  theme: "dark"
  }
};

const {
  color: { theme = "light" }
} = setting;

console.log(theme);
```

**After: (바꾸려는 변수명 앞에 -> : 추가후 새 변수명을 입력만 하면된다.)**

```JS index.js
const setting = {
  color: {
  theme: "dark"
  }
};

const {
  color: { theme: myTheme = "light" }
} = setting;

console.log(myTheme);
```

**"만약 여기서 let 변수로 myTheme룰 만들면 어떨까"**
-> let 변수 추가후, const 변수를 지운후 () 로 감싸준다.(let 변수에 myTheme를 업데이트 하기)

```JS index.js
const setting = {
  color: {
  theme: "dark"
  }
};

let myTheme = "blue";
  console.log(myTheme);

({
  color: { theme: myTheme = "light" }
} = setting);

console.log(myTheme);
```

### 5.4 Function Destructuring

**긴 augment**

```JS index.js
function saveSetting(followAlert, unfollowAlert, mrkAlert ,themeColor){
}
```

**단축형 augment**

```JS index.js
function saveSetting(settings) {
  console.log(settings);
}

saveSetting({
  follow: true,
  alert: true,
  mkt: true,
  color: "green"
});
```

**진보형: 변수들의 가독성을 확보하고, 각 변수의 기본값을 설정해 주고 싶을 땐**
-> object destructuring을 사용한다!

```JS index.js
function saveSettings({ notifications, color: { theme } }) {
  console.log(theme);
}

saveSettings({
  notifications: {
  follow: true,
  alert: true,
  mkt: false
  },
  color: {
  theme: "blue"
  }
});
```

### 5.5 Value Shorthands(변수명 단축)

변수 이름을 똑같이 하고 싶다면 shorthand property (단축속성명)을 사용할 수 있다.

```JS index.js
const follow = checkFollow();
const alert = checkAlert();

const settings = {
notifications: {
// follow: follow, // 여기 반복되는 부분을 안써도 되게 하기
// alert: alert
follow,
alert
}
};
```

### 5.6 Swapping and Skipping

**Swapping**

```JS index.js
//Swapping
let mon = "Sat";
let sat = "Mon";

[sat, mon] = [mon, sat];

console.log(sat, mon);
```

**Skipping**

```JS index.js
//Skipping (빈 칸을 [콤마] 로 채우기)
const days = ["Mon", "Tue", "wed", "Thu", "Fri", "Sat", "Sun"];
const [, , , thu, fri] = days;
console.log(thu, fri);
```

## 6 Rest and Spread

### 6.1 Introduction to Spread

**Spread**
(spread는 기본적으로 변수를 가져와서 풀어 헤치고 전개하는 것 -> … (점 3개))

**_Unpack_**

```JS index.js
const friends = [1, 2, 3, 4];
const family = ["a", "b", "c"];

// array 안에 있는 요소(element)들을 원할때
console.log([...friends, ...family]);

const sexy = {
  name: "heno",
  age: 20
};

const hello = {
  sexy: true,
  hello: "hello"
};

console.log({...sexy, ...hello});
```

### 6.2 Spread Applications

**ADD**

```JS index.js
const friends = ["nicol", "arug", "mina"];

const newFriends = [...friends, "Leb"];

console.log(newFriends);

const nico = {
  username: "nico"
};

console.log({ ...nico, password: 123 });
```

**좀더 복잡한 구성 예)**

```JS index.js
const first = ["Mon", "Tue", "Wed"];

const weeked = ["Sat", "Sun"];

const fullWeek = [...first, "Thu", "Fri", ...weeked];

console.log(fullWeek);
```

**conditional (조건부)**
(어떻게 하면 object에 속성(property)을 조건부로 추가할 수 있는가)

```JS index.js
const lastName = prompt("Last Name");

const user = {
  username: "nico",
  age: 32,
  ...(lastName !== "" && { lastName })
};

console.log(user);
```

### 6.3 Intro to Rest Parameters

끝도없는 paramenter를 전달받는 함수를 만들어 보자

**Rest**
rest는 모든 값을 하나의 변수로 축소(contract)시켜주는 거다

**_Contract_**

```JS index.js
const infiniteParams = (...heyman) => console.log(heyman);

infiniteParams("1", 2, true, "lalala", [1, 2, 3, 4]);
```

**_…rest 를 이용해 한개만 픽업하기_**

```JS index.js
const bestFriendMaker = (firstOne, ...rest) => {
console.log(`My best friend is ${firstOne}`);
  console.log(rest);
};

bestFriendMaker("jhe", "sodn", "aaw", "upps");
```

### 6.4 Rest + Spread + Restructure Magic

#### 패스워드를 제거하고 싶을때 예)

**basic**

```JS index.js
const user = {
  name: "aeq",
  age: 13,
  password: 12345
};

user["password"] = null;

console.log(user);
```

**cleaning object**

```JS index.js
const user = {
  name: "aeq",
  age: 13,
  password: 12345
};

const killPassword = ({ password, ...rest }) => rest;

const cleanUser = killPassword(user);

console.log(cleanUser);
```

**setting default - 기본값 설정하기**

```JS index.js
const user = {
  name: "nico",
  age: 24,
  password: 12345
};

const setCountry = ({ country = "KR", ...rest }) => ({ country, ...rest });

console.log(setCountry(user));
```

**rename property - 속성명 바꾸기**

```JS index.js
const user = {
  NAAME: "nico",
  age: 24,
  password: 12345
};

const rename = ({ NAAME: name, ...rest }) => ({ name, ...rest });

console.log(rename(user));
```

## 7 For … of

자바스크립트의 새로운 루프에 대해 배워보기
(루프는 기본적으로 같은 일을 반복적으로 하는 거다)

**기본적인 루프**

```JS index.js
const friends = ["win", "cool", "sexy", "cuty"];

for (let i = 0; i < 20; i++) {
  console.log("I still loving you");
}
```

**forEach 루프**

```JS index.js
const friends = ["win", "cool", "sexy", "cuty"];

// const addHeart = (currentItem, currentindex, currentArray) =>
// console.log(currentItem, currentindex, currentArray);

const addHeart = (c, i, a) => console.log(c, i, a);

friends.forEach(addHeart);
```

**For of 루프**
(For of 에서는 선언을 const 로 할지 let로 할지 선택할 수 있다)
(가끔 루프를 멈추고 싶을 때, for of를 쓰면 된다)

```JS index.js
const friends = [
  "win",
  "cool",
  "sexy",
  "cuty",
  "many friends",
  "a lot of friends",
  "more then friends"
];

for (const friend of friends) {
  console.log(friend);
}
```

**_예) sexy를 찾는 순간 루프를 멈추게 하고 싶을 때는_**

```JS index.js
const friends = [
  "win",
  "cool",
  "sexy",
  "cuty",
  "many friends",
  "a lot of friends",
  "more then friends"
];

for (const friend of friends) {
  if (friend === "sexy") {
    break;
    } else {
    console.log(friend);
  }
}
```

## 8 Promises

### 8.1 Introduction to Async

```JS index.js
// 비동기적 프로그래밍
const hello = fetch("https://www.google.com/");

console.log("something is wrong!");
console.log(hello);
```

### 8.2 Creating Promises

Promise는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다

```JS index.js
//resolve : 야, 이게 네 값이야. 자바스크립트로 돌아가!
//reject : 야, 미안한데 에러가 있어!

const amIsexy = new Promise((resolve, reject) => {
  setTimeout(resolve, 3000, "yes you are");
});

console.log(amIsexy);

setInterval(console.log, 1000, amIsexy);
```

### 8.3 Using Promises

자바스크립트에 promise가 끝난 이후의 명령어를 전달하려면, 언제 끝나는건 중요하지 않고 끝나는 이후에 값을 돌려달라고 명령어를 내리는 것

**기본형**

```JS index.js
const amIsexy = new Promise((resolve, reject) => {
  setTimeout(resolve, 3000, "yes you are");
});

amIsexy.then(value => console.log(value));
```

**만약 promise에 에러가 생기면 우린 그걸 catch하면 된다**

**_catch는 then이랑 비슷하지만 에러를 잡기 위해 사용한다._**
then이 실행되면 catch는 절대 실행되지 않는다, 반대로 catch가 실행되면 then또한 절대로 실행되지않는다

```JS index.js
const amIsexy = new Promise((resolve, reject) => {
  setTimeout(reject, 1000, "You are sily");
});

amIsexy
  .then(result => console.log(result)) //resolve
  .catch(error => console.log(error)); //reject
```

### 8.4 Chaining Promises

promise들을 엮고 싶을 때는 기존의 then에서 return 값이 있어야 한다
(then은 넣고 싶은 만큼 넣어서 chaining을 해주면 되는거)

```JS index.js
const amIsexy = new Promise((resolve, reject) => {
  resolve(2);
});

// 결과값이 여러개 나오는 경우
amIsexy
  .then(number => {
  console.log(number * 2);
  return number * 2;
})
  .then(otherNumber => {
  console.log(otherNumber * 2);
});
```

**Array function으로 간단하게**

```JS index.js
const amIsexy = new Promise((resolve, reject) => {
  resolve(2);
});

amIsexy
.then(number => number * 2)
.then(number => number * 2)
.then(number => number * 2)
.then(number => number * 2)
.then(number => number * 2);
```

**Function을 추가하여 정리**

```JS index.js
const amIsexy = new Promise((resolve, reject) => {
resolve(2);
});

const timeTwo = number => number * 2;

amIsexy
.then(timeTwo)
.then(timeTwo)
.then(timeTwo)
.then(timeTwo)
.then(timeTwo)
.then(lastNumber => console.log(lastNumber));
```

**여기서 하나의 then이 에러를 발생시키면 어떻게 될까 ?**

```JS index.js
  const amIsexy = new Promise((resolve, reject) => {
resolve(2);
});

const timeTwo = number => number * 2;

amIsexy
.then(timeTwo)
.then(timeTwo)
.then(timeTwo)
.then(timeTwo)
.then(timeTwo)
.then(() => {
  throw Error("Something is wrong");
})
.then(lastNumber => console.log(lastNumber))
.catch(error => console.log(error));
```

### 8.5 Promise.all

Promise.all은 주어진 모든 Promise를 싱행한 후 진행되는 하나의(마지막) Promise를 반환한다.

```JS index.js
//하나의 API가 아닌 3개, 4개의 API에서 값을 불러와야 할 때
const p1 = new Promise(resolve => {
  setTimeout(resolve, 5000, "first");
});

const p2 = new Promise(resolve => {
  setTimeout(resolve, 1000, "second");
});

const p3 = new Promise(resolve => {
  setTimeout(resolve, 3000, "third");
});

const allPromise = Promise.all([p1, p2, p3]);

allPromise.then(value => console.log(value));
```

**resolve를 하는 대신 Reject가 되게 바꿔보자**

```JS index.js
//하나가 reject되면 전체가 reject된다.
const p1 = new Promise(resolve => {
  setTimeout(resolve, 5000, "first");
});

const p2 = new Promise((resolve, reject) => {
  setTimeout(reject, 1000, "I love JS");
});

const p3 = new Promise(resolve => {
  setTimeout(resolve, 3000, "third");
});

const allPromise = Promise.all([p1, p2, p3]);

allPromise.then(value => console.log(value)).catch(err => console.log(err));
```

### 8.6 Promise.race

Promise.all과 다르게 어느것이 먼저 되는지 상관없이 가장 빠른걸 반환한다.

```JS index.js
const p1 = new Promise(resolve => {
  setTimeout(resolve, 5000, "first");
});

const p2 = new Promise((resolve, reject) => {
  setTimeout(reject, 5000, "I love JS");
});

const p3 = new Promise(resolve => {
  setTimeout(resolve, 3000, "third");
});

const allPromise = Promise.race([p1, p2, p3]);

allPromise.then(value => console.log(value)).catch(err => console.log(err));
```

**좀더 간결한 코드**

```JS index.js
const p1 = new Promise(resolve => {
  setTimeout(resolve, 5000, "first");
});

const p2 = new Promise((resolve, reject) => {
  setTimeout(reject, 5000, "I love JS");
});

const p3 = new Promise(resolve => {
  setTimeout(resolve, 3000, "third");
});

Promise.race([p1, p2, p3])

  .then(value => console.log(value))
  .catch(err => console.log(err));
```

### 8.7 .finally

finalize하는데 성공하든지 실패하든지 결과에 상관없이 반환한다
finall는 보통…API를 호출할 때 쓴다. 로딩할 때, 하나를 얻고 두개를 얻고 세개를 얻고
마지막으로 데이터를 보여주거나, 로딩을 멈추거나 뭔가를 하거나 할때.

```JS index.js
const p1 = new Promise((resolve, reject) => {
  setTimeout(reject, 5000, "first");
})
  .then(value => console.log(value))
  .catch(e => console.log(`${e} X`))
  .finally(() => console.log("Im done"));
```

### 8.8 Real world Promises

Promise를 return하는 fetch (fetch는 Promise를 return한다 )

```JS index.js
fetch("https://yts.lt/api/v2/list_movies.json")
.then(response => {
console.log(response);
return response.json();
})
.then(json => console.log(json))
.catch(err => console.log(`${err} XXX`));
```

practice api :
https://jsonplaceholder.typicode.com/

## 9 Async / Await

### 9.1 Async Await

Async/await는 두 Promise의 없데이트다

then, then, then, then은 별로다. 이것들은 코드를 좋지 않게 보이게 한다.
Async/await는 기본적으로 Promise를 사용하는 코드를 더 좋게 보이게 하는 문법이다.

> 먼저, await는 혼자서는 사용할 수 없다<br/>
> await는 항상 async function안에서만 사용할 수 있다.<br/>
> await는 기본적으로 Promise가 끝나길 기다린다

**.then / .catch를 사용한 경우**

```JS index.js
const getMoviesAsync = () => {
  fetch("https://yts.lt/api/v2/list_movies.json")
  .then(response => {
  console.log(response);
  return response.json();
})
  .then(json => console.log(json))
  .catch(e => console.log(`XXX ${e}`));
}; // Promise one
```

**async / await를 사용한 경우**

```JS index.js
// 기본 형식으로의 표현
// async function getMovies() {

// }

const getMoviesAsync = async () => {
  const response = await fetch("https://yts.lt/api/v2/list_movies.json");
  const json = await response.json();
  console.log(json);
}; //async one

getMoviesAsync();
```

> 6 Reasons Why JavaScript Async/Await Blows Promises Away (Tutorial) <br/> https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9

### 9.3 Parallel Async Await

```JS index.js
const getMoviesAsync = async () => {
  try {
    const [moviesResponse, suggestionsResponse] = await Promise.all([
      fetch("https://yts.lt/api/v2/list_movies.json"),
      fetch("https://yts.lt/api/v2/movie_suggestions.json")
    ]);
    const [movies, suggestions] = await Promise.all([
      moviesResponse.json(),
      suggestionsResponse.json()
    ]);
    console.log(movies, upcoming);
  } catch (error) {
    console.log(`XXX! ${error}`);
  } finally {
    console.log("We are done!");
  }
};

getMoviesAsync();
```
