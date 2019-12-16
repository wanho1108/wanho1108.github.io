---
layout: article-view
categories: post
title:  "모바일 웹 접근성 실패 사례"
summary: "summary 내용 삽입"
date:   2019-12-12 10:40:00 +0900
---

다사다난 했던 모바일 웹 구축 프로젝트를 마무리 한 뒤 한국웹접근성인증평가원에서 접근성 심사를 접수하였다. 단 한번에 적합 판정을 받길 원했지만 부적합 결과가 나와 2차 심사를 받아야 하는 상황이 왔다.

## 주요 원인

여러 문제가 있었지만 부적합의 주요 원인은 `초점`과 `논리적인 콘텐츠 순서` 였다.

## 해결 방안

### Skip Navigation

스킵내비게이션은 기본적으로 화면 밖에 위치시키고 포커스가 되었을 때 화면에 노출되게끔 처리를 하였는데 클릭 시 `Talkback`에서 스킵내비게이션이 원래 있던 위치에 곂쳐있던 브라우저 상단 주소창이 클릭되는 이슈가 있었다.

```css
.skip-navigation__anchor {
  position: absolute;
  top: -100px;
  ...
}

.skip-navigation__anchor:focus {
  top: 0;
}
```

해결 방법은 기본 위치가 무엇과도 곂치지 않게 스타일을 수정하였다.

```css
.skip-navigation__anchor {
  position: absolute;
  top: 0;
  ...
}
```

### Heading

li 내 heading 작성 시 heading 인식 안됌.

**내용 보충하기**

### Anchor

IR 기법을 활용한 `<a>` 태그는 설정된 크기가 아닌 숨긴 텍스트의 위치와 크기에 초점이 잡혔다.

**코드와 해결방안 작성하기**

### Tab

`WAI-ARIA`를 활용하여 작성했지만 논리적인 컨텐츠 순서에 경고를 받음. 
`WAI-ARIA`에 너무 의존하면 안된다.. 는 내용으로 작성하기

**코드와 해결방안 작성하기**

### 텍스트 숨기기

당연한 얘기지만 font-size: 0, display: none, visibility: hidden 은 리더기가 읽지 않음

**내용 보충하기**

### Entity code

&가 안읽힘.

## 참고 문서