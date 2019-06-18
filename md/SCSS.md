---
title: SCSS의 기본적인 사용 방법
date: 2019-06-18 14:10:17
tags: 
   - Front-end
   - CSS
thumbnail: /img/sass.png
---


기본 코딩
------

## 자식요소

{} 괄호안의 자식요소에 태그(class, ID등)를 넣으면 자동으로 부모요소를 확인시켜준다.

``` Html index.html
<div>
  <p>여행 가고 싶다!</p>
</div>
```

``` scss style.scss
div {
  background: red;
  width: 400px;
  height: 400px;
  p {
    color: white;
    font-weight: bold;
    text-align: center;
  }
}
```

**⬇️출력결과**

``` css style.css
div {background: red; width: 400px; height: 400px;}
div p {color: white; font-weight: bold; text-align: center;}
```

## 「&」으로 연결하기

위의 방식은 부모와 지식형식만으로 표현하지만 아래의 예 처럼 태그를 연결할 경우에는 「&」을 사용한다.

**아래 처럼 출력하기**

``` css style.css
div {width: 300px; height: 200px; background: red;}
div:before {content: ''; display: block; width: 300px; height: 150px; background: blue;}
div.sample {width: 150px; height: 29px; background: yellow;}
div .sample {width: 120px; height: 53px; background: green;} 
```

**&사용하는 SCSS**
``` scss style.scss
div {
  width: 300px;
  height: 200px;
  background: red;
  &:before {
    content: '';
    display: block;
    width: 300px;
    height: 150px;
    background: blue;
  }
  &.sample { /* div.className */
    width: 150px;
    height: 29px;
    background: yellow;
  }
  .sample { /* div안에 class 가 존재하는 경우 div .className */
    width: 120px;
    height: 53px;
    background: green;
  }
}
```

편리 포인트
------

## 변수

변수 사용가능
```
/* 변수 선언 방법*/
$변수명: 값;
```

``` scss style.scss
$main_color: red; 
$sub_color: blue;
$font_size: 16px;

div {
  color: $main_color;
  font-size: 18px;
  p {
    border: 1px solid $main_color;
    color: $sub_color;
    font-size: $font-size;
  }
}
```


**⬇️출력결과**

``` css style.css
div {color: red; font-size: 18px;}
div p {border: 1px solid red; color: blue; font-size: 16px;}
```

#### 조건부
조건문 사용가능

##### if 문

``` scss style.scss
div {
  @if 1 + 1 == 2 { width: 100%; } // 1+1=2 => true
  @if 1 > 2 {width: 50%;} // 1 > 2 => false
  @if null {width: 10%;} // null => false
}
```

**⬇️출력결과**

``` css style.css
div {
    width: 100%;
  }
```

##### else & else if 문

``` scss style.scss
$color = red;
div {
  @if $color == blue {
    background: blue;
  } @else if $color == yellow {
    background: yellow;
  } @else if $color == red {
    background: red;
  } @else {
    background: white;
  }
}
```

**⬇️출력결과**

``` css style.css
div {
  background: red;
}
```

#### 반복처리

##### for 문

``` scss for.scss
@for $i from 1 through 3 {
  .sample-#{$i} {width: 100px * $i;} // 문자열$i을 사용 할 경우, 「$i」이 아니고「#{$i}」로 쓰기
}
```

**⬇️출력결과**

``` css for.css
.sample-1 {width: 100px;}
.sample-2 {width: 200px;}
.sample-3 {width: 300px;}
```

##### while 문

``` scss while.scss
$i: 1;
@while $i < 4 {
  .sample-#{$i} {width: 100px * $i;}
  $i: $i + 1;
}
```

**⬇️출력결과**

``` css while.css
.sample-1 {width: 100px;}
.sample-2 {width: 200px;}
.sample-3 {width: 300px;}
```

##### each 문

``` scss while.scss
@each $var in <list> 
/* $var -> 임의 변수 */
/* <list> -> ,(콤마)로 구분 하는 리스트
```

``` scss each.scss
@each $sample in a, b, c {
  .#{$sample}-icon {
    background-image: url('/images/#{$sample}.png');
  }
}
```

**⬇️출력결과**

``` css each.css
.a-icon {
  background-image: url('/images/a.png');
}
.b-icon {
  background-image: url('/images/b.png');
}
.c-icon {
  background-image: url('/images/c.png');
}
```

## 함수

함수 사용 가능
```
/* 함수 선언 방법 */
@mixin 함수명(인수１, 인수２, ...) {
  ...
}

/* 함수 불러오기 */
@include 함수명(인수１, 인수２, ...);
```

## 미디어쿼리

``` scss media-queries.scss
$breakpoint-tablet: 1024px; /* 함수 선언 */
$breakpoint-mobile: 640px; /* 변수 선언 */

/* $break-point 이하 */
@mixin max-screen($break-point) { 
  @media screen and (max-width: $break-point) {
    @content;
  }
}
/* $break-point 이상 */
@mixin max-screen($break-point) { 
  @media screen and (min-width: $break-point) {
    @content;
  }
}
/* $break-point-min이상、$break-point-max이하 */
@mixin screen($break-point-min, $break-point-max) { 
  @media screen and (min-width: $break-point-min) and (max-width: $break-point-max) {
    @content;
  }
}

/* 사용 예 */
div {
  @include max-screen($breakpoint-mobile) { /* 640px이하 */
    width: 100%;
  }
  @include min-screen($breakpoint-tablet) { /* 1024px이상 */
    width: 50%;
  }
  @include screen($breakpoint-mobile, $breakpoint-tablet) { /* 640px이상 1024px이하 */
    width: 80%;
  }
}
```

**⬇️출력결과**

``` css media-queries.css
@media screen and (max-width: 640px) {
  div {width: 100%;}
}
@media screen and (min-width: 1024px) {
  div {width: 50%;}
}
@media screen and (min-width: 640px) and (max-width: 1024px) {
  div {width: 80%;}
}
```

## 벤더 프리픽스

``` scss vender-prefix.scss
$set-prefix: '', '-moz-', '-webkit-'; 

@mixin ProprtySetPrefix($name, $value) {
  @each $prefix in $set-prefix {
    #{$prefix}#{$name}: $value;
  }
}

@mixin ValueSetPrefix($name, $value) {
  @each $prefix in $set-prefix {
    #{$name}: #{$prefix}$value;
  }
}

/* 적용 예 */
div {
  @include ProprtySetPrefix(transition, .2s);
}
```

**⬇️출력결과**

``` css vender-prefix.css
div {
  transition: .2s;
  -moz-transition: .2s;
  -webkit-transition: .2s;
}
```

## 폰트

``` scss font.scss
@mixin font-face($name, $path, $weight: null, $style: null, $exts: otf ttf) {
  $src: null;
  $formats: (
    otf: "opentype",
    ttf: "truetype"
  );
  @each $ext in $exts {
    $format: map-get($formats, $ext);
    $src: append($src, url(quote($path)) format(quote($format)), comma);
  }
  @font-face {
    font-family: quote($name);
    font-style: $style;
    font-weight: $weight;
    src: $src;
  }
}

/* 적용 예 */
@include font-face('Note Serif', '../../../../fonts/NotoSerif-Regular.otf', 400, null, otf);

p {
  font-family: 'Noto Serif', sans-serif;
}
```
**⬇️출력결과**

``` css font.css
@font-face {
  font-family: 'Noto Serif';
  font-weight: 400;
  src: url(../fonts/NotoSerif-Regular.otf) format("opentype");
}

p {
  font-family: 'Noto Serif', sans-serif;
}
```


이상 SCSS의 기본 사용 방법에 관한 내용이었습니다.