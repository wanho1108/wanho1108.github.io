---
layout: article-view
categories: post
title:  "DocumentFragment로 리플로우 최소화"
summary: "DocumentFragment는 Document의 경량화된 버전으로 여러 노드로 이루어진 문서의 구조를 담을 수 있지만 활성화된 문서 트리의 일부가 아니기 때문에 문서에 영향을 주지 않고 리플로우를 발생하지 않으며 성능에 큰 영향을 미치지 않습니다."
date:   2019-12-02 10:40:00 +0900
---

`DocumentFragment`는 `Document`의 경량화된 버전으로 여러 노드로 이루어진 문서의 구조를 담을 수 있지만 활성화된 문서 트리의 일부가 아니기 때문에 문서에 영향을 주지 않고 리플로우를 발생하지 않으며 성능에 큰 영향을 미치지 않습니다.

## 어쩌다

토이 프로젝트 중에 로컬 스토리지의 데이터를 리스트로 출력하는 작업이 있었는데 데이터만큼의 리플로우가 발생했다.

```typescript
function showItems(items: IItems[])) {
  const $list = document.querySelector('.list') as HTMLUListElement;

  for (let item of items) {
    const $item = document.createElement('li') as HTMLLIElement;
    $item.textContent = item.name;
    $list.appendChild($item);
  }
}
```

innerHTML 

```typescript
function showItems(items: IItems[])) {
  const $list = document.querySelector('.list') as HTMLUListElement;
  let $item: string;

  for (let item of items) {
    $item += `<li>${item.name}</li>`;
  }

  $list.innerHTML($item);
}
```

DocumentFragment

```typescript
function showItems(items: IItems[])) {
  const $list = document.querySelector('.list') as HTMLUListElement;
  const $fragment = document.createDocumentFragment();

  for (let item of items) {
    const $item = document.createElement('li') as HTMLLIElement;
    $item.textContent = item.name;
    $fragment.appendChild($item);
  }
  
  $list.innerHTML($item);
}
```

## 참고 문서
- https://developer.mozilla.org/ko/docs/Web/API/DocumentFragment