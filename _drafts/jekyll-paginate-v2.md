---
layout: article-view
category: post
title:  Jekyll Paginate V2 적용 실패 사례
summary: summary 내용 삽입 해주세요.
date:   2019-12-12 10:40:00 +0900
---

블로그를 만들고 나서 TIL(Today I Learned)도 함께 정리해 게시하면 좋겠다는 생각이 문득 들었다. 이미 완성된 블로그이기 때문에 별도의 추가 작업 없이 포스트를 작성해 나가면 되지만 앞으로 작성될 주제들(스터디, 실패 사례 등)이 비교적 많이 작성될 TIL에 묻혀버릴까 하는 걱정에 별도의 메뉴로 분리하기로 했다.

방법을 모색하던 중 [jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2) 플러그인을 알게 되었는데 카테고리 및 모음에 대한 페이지 매김이 가능했다. 내가 딱 원하던 기능이라 한 치의 고민 없이 바로 블로그에 적용하기로 헸디. 그리고 이는 앞으로는 무엇이든 적용하기전에 문서를 꼼꼼히 읽어 보아야겠다는 교훈을 주는 사례가 되었다.

## 플러그인 설치하기

```bash
$ gem install jekyll-paginate-v2
```

## 환경 설정 변경하기

`Gemfile` 플러그인 부분에 jekyll-paginate-v2을 추가한다.

```bash
group :jekyll_plugins do
  ...
  gem "jekyll-paginate-v2"
end
```

`_config.yml` 도 마찬가지로 jekyll-paginate-v2 추가하고 설정 옵션을 작성한다. 더 상세한 설정 방법은 [여기](https://github.com/sverrirs/jekyll-paginate-v2/blob/master/README-GENERATOR.md#filtering-categories)를 참고한다.

```bash
plugins:
  ...
  - jekyll-paginate-v2

pagination: 
  enabled: true
  per_page: 5
  sort_reverse: true
  title: ':title'
  trail:
    before: 2
    after: 2        
```

## 게시글 리스트 파일 변경하기

{% raw %}
```html
... raw if else endif 에러 나는거 확인하기
```
{% endraw %}


## 참고 문서

- [https://github.com/sverrirs/jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2)