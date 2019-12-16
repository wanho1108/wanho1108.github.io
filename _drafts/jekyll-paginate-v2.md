---
layout: article-view
categories: post
title:  "Jekyll Paginate V2 적용 실패 사례"
summary: "summary 내용 삽입 해주세요."
date:   2019-12-12 10:40:00 +0900
---

블로그를 만들고 나서 TIL(Today I Learned)도 함께 정리해 게시하면 좋겠다는 생각이 문득 들었다. 이미 완성된 블로그이기에 별도의 추가 작업 없이 포스트를 척척 작성해 나가면 되지만 앞으로 작성될 주제들(스터디, 실패 사례 등)이 비교적 많이 작성될 TIL 포스트에 묻혀버리지 않을까 하는 걱정에 별도의 메뉴로 분리하기로 했다.

메뉴를 분리하기 위해 포스트의 카테고리 또는 모음에 대한 페이지 매김을 어떻게 처리해야할까 방법을 모색하던 중 [jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2) 플러그인을 찾게 되었다. 내가 딱 원하던 기능이라 한 치의 고민없이 바로 블로그에 적용하기로 했다. 그리고 이는 앞으로 무엇이든 적용하기전에 문서를 꼼꼼히 읽어 보아야겠다는 교훈을 주는 계기가 되었다.

## 플러그인 설치하기

```bash
$ gem install jekyll-paginate-v2
```

## 플러그인 추가 및 설정하기

`Gemfile` 플러그인 부분에 설치한 jekyll-paginate-v2을 추가한다.

```bash
group :jekyll_plugins do
  ...
  gem "jekyll-paginate-v2"
end
```

`_config.yml` 도 플러그인을 추가하고 설정 옵션을 작성한다. 더 상세한 설정 방법은 [여기](https://github.com/sverrirs/jekyll-paginate-v2/blob/master/README-GENERATOR.md#filtering-categories)를 참고한다.

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

## 파일 생성

today-i-learned 생성하기

```markdown
---
layout: article-list
permalink: /today-i-learned/
pagination: 
  enabled: true
  category: today-i-learned
---
```


## 코드 변경

{% raw %}
```html
# todo
- raw if else endif 에러 나는거 확인하기
- 목록 출력도 같이 적어주기

{% if paginator.total_pages > 1 %}
<ul>
  {% if paginator.previous_page %}
  <li>
    <a href="{{ paginator.previous_page_path | prepend: site.baseurl }}">Newer</a>
  </li>
  {% endif %}
  {% if paginator.next_page %}
  <li>
    <a href="{{ paginator.next_page_path | prepend: site.baseurl }}">Older</a>
  </li>
  {% endif %}
</ul>
{% endif %}
```
{% endraw %}


## 참고 문서

- [https://github.com/sverrirs/jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2)