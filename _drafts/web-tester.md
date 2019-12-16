---
layout: article-view
title:  모바일 웹 접근성 경험기
date:   2019-05-06 12:06:41
categories: post
---

## 시작하기 앞서

한국웹접근성인증평가원에서 웹 접근성 인증마크를 부여받기까지의 몇 가지 실수를 기록합니다.

## Skip Navigation

스킵내비게이션 스타일은 기본적으로 화면 밖에 위치시키고 포커스 되었을 때 보이게끔 처리를 하였는데  
클릭 시 `Talkback` 에서 스킵내비게이션이 아닌 위치가 곂쳐있던 브라우저 상단 주소창이 클릭되는 이슈가 있었다.

```css
.skip-navigation__anchor {
  position: absolute;
  top: -100px;
  ...
}

.skip-navigation__anchor:focus {
  top: 0;
  ...
}
```

이 황당한 이슈를 해결하기 위해 스킵내비게이션이 다른 요소와 곂치지 않게 스타일을 수정함.

```css
.skip-navigation__anchor {
  position: absolute;
  top: 0;
  ...
}

.skip-navigation__anchor:focus {
  ...
}
```

## Anchor

IR 기법을 활용한 `<a>` 태그 버튼은 설정한 크기가 아닌 숨긴 텍스트의 크기와 위치에 초점이 잡히는 이슈가 있었다. 

```html
<a href="/" class="site-logo">
  <span class="is-blind">Site Logo</span>
</a>
``` 

```css
.site-logo {
  display: inline-block;
  width: 100px;
  height: 100px;
  background: url(site-logo.svg) no-repeat 0 0;
  ...
}
```

