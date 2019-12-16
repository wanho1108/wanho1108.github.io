---
layout: article-view
categories: post
title:  "Jekyll Paginate V2 적용 실패 사례"
summary: "summary 내용 삽입 해주세요."
date:   2019-12-12 10:40:00 +0900
---

> 작성중인 포스트입니다.  
> 몇 가지 수정사항이 있습니다.  
> 내용을 완성하세요.  
> 오탈자, 맞춤법, 문맥을 확인하세요.

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

index 파일 수정

```markdown
---
layout: article-list
permalink: /
pagination: 
  enabled: true
  category: post
---
```

TIL 생성하기

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

article-list.html 의 게시글 목록 코드 변경

{% raw %}
```html
<div class="post-list">
  <h2 class="is-blind">게시글 목록</h2>
  <ul class="post-list__list">
    {%- for post in paginator.posts -%}
      <li class="post-list__listitem">
        {%- assign date_format = site.minima.date_format | default: "%b %d, %Y" -%}
        <h3 class="post-list__subject">
          <a href="{{ post.url | relative_url }}" class="post-list__subject-anchor">
            {{ post.title | escape }}
          </a>
        </h3>
        <p class="post-list__summary">{{ post.summary }}</p>
        <time datetime="{{ post.date }}" aria-label="작성일: {{ post.date | date: date_format }}" class="post-list__time">{{ post.date | date: date_format }}</time>
      </li>
    {%- endfor -%}
  </ul>
</div>
```
{% endraw %}

마찬가지로 게시글 페이지 목록 코드 변경

{% raw %}
```html
<nav class="pagination">
  <div class="pagination__wrapper">
    <h2 class="is-blind">게시글 페이지 목록</h2>
    {% if paginator.previous_page %}
      <a href="{{ paginator.previous_page_path | prepend: site.baseurl }}" class="pagination__anchor pagination__anchor--prev">이전 페이지</a>
    {% else %}
      <span role="link" aria-disabled="true" class="pagination__anchor pagination__anchor--prev is-disabled">이전 페이지</span>
    {% endif %}
    {% if paginator.next_page %}
      <a href="{{ paginator.next_page_path | prepend: site.baseurl }}" class="pagination__anchor pagination__anchor--next">다음 페이지</a>
    {% else %}
      <span role="link" aria-disabled="true" class="pagination__anchor pagination__anchor--next is-disabled">다음 페이지</span>
    {% endif %}
    <ul class="pagination__list">
      {% if paginator.page_trail %}
        {% for trail in paginator.page_trail %}
          <li class="pagination__listitem">
            {% if page.url == trail.path %}
              <em role="link" aria-disabled="true" aria-label="현재 페이지, {{ trail.num }}번 페이지 보기" aria-current="page" class="pagination__anchor is-active">{{ trail.num }}</em>
            {% else %}
              <a href="{{ trail.path | prepend: site.baseurl | replace: 'index.html', '' }}" aria-label="{{ trail.num }}번 페이지 보기" class="pagination__anchor">{{ trail.num }}</a>
            {% endif %}
          </li>
        {% endfor %}
      {% endif %}
    </ul>
  </div>
</nav>
```
{% endraw %}

## 배포하기

배포했는데! 목록이 뜨지 않았다.

## 원인 및 해결 방안

Github Pages는 Jekyll Paginate V2를 지원하지 않는다 ㅠㅠ.
Travis CI 를 통해서 해결하거나.. 등등 몇가지 방안이 있었음.

## 마무리

결국.. Jekyll Paginate V2를 포기하고 좀 더 어떻게 처리하면 좋을지 고민해야함.


## 참고 문서

- [https://github.com/sverrirs/jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2)