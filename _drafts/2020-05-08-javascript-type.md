---
layout: article-view
categories: post
title:  "[JavaScript] 데이터 타입"
summary: "summary 내용 삽입 해주세요."
date:   2020-05-08 00:00:00 +0900
---

## 타입(Type)

최신 ECMAScript 표준은 다음과 같은 7개의 자료형을 정의한다.

**기본 (Primitive values)** 
- Boolean
- Null
- Undefined
- Number
- String
- Symbol (ES6부터 추가됨)

**객체**
- Object

### 타입 확인하기

`typeof` 연사자를 사용하면 값의 타입을 문자열로 확인할 수 있다.

```javascript
typeof true; // 'boolean'
typeof null; // 'object'
typeof undefined; // 'undefined'
typeof 1108; // 'number'
typeof 'wanho1108'; // 'string'
typeof Symbol(); // 'symbole'
typeof {}; // 'object'
typeof []; // 'object'
```

여기서 흥미로운 결과를 볼 수 있는데 `typeof null`의 예상 타입은 `null`이었지만 실제 결과를 보면 `object`를 출력한다. 이는 자바스크립트 버그이며 `null` 타입 비교 시 주의하여 사용해야 한다.

```javascript
function sum(a, b) {
  return a + b;
}

typeof sum; // 'function'
```

`typeof`에는 위 7가지 타입외에 하나 더 반환하는데 이는 `function`이며 `function`은 `object`의 하위 타입이다.

