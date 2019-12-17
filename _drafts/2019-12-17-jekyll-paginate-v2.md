---
layout: article-view
categories: post
title:  "Jekyll Paginate V2 적용 실패 사례"
summary: "메뉴를 분리하기 위해 카테고리에 대한 페이지 매김을 어떻게 처리해야 할까 싶어 방법을 모색하던 중 jekyll-paginate-v2 플러그인을 알게 되었다. 딱 내가 원하던 기능이라 한 치의 고민 없이 바로 블로그에 적용하기로 했다. 그리고 이는 앞으로 적용하기 전에 무엇이든 문서를 꼼꼼히 읽어야겠다는 교훈을 심어 주었다."
date:   2019-12-17 16:00:00 +0900
---

블로그를 만들고 나서 TIL(Today I Learned)도 함께 정리해 게시하면 좋겠다는 생각이 문득 들었다. 이미 완성된 블로그이기에 별도의 추가 작업 없이 포스트를 척척 작성해 나가면 되지만 앞으로 작성될 주제들(스터디, 실패 사례 등)이 비교적 많이 작성될 TIL 포스트에 묻혀버리지 않을까 하는 걱정에 별도의 메뉴로 분리하기로 했다.

메뉴를 분리하기 위해 카테고리에 대한 페이지 매김을 어떻게 처리해야 할까 싶어 방법을 모색하던 중 [jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2) 플러그인을 알게 되었다. 딱 내가 원하던 기능이라 한 치의 고민 없이 바로 블로그에 적용하기로 했다. 그리고 이는 앞으로 적용하기 전에 무엇이든 문서를 꼼꼼히 읽어야겠다는 교훈을 심어 주었다.

## 설치하기

아래의 명렁어를 통해 플러그인을 설치한다.

```bash
$ gem install jekyll-paginate-v2
```

## 설정하기

`Gemfile` 파일에 설치한 jekyll-paginate-v2을 추가한다.

```bash
group :jekyll_plugins do
  ...
  gem "jekyll-paginate-v2"
end
```

`_config.yml` 파일도 플러그인을 추가하고 설정 옵션을 작성한다. 더 상세한 설정 방법은 [여기](https://github.com/sverrirs/jekyll-paginate-v2/blob/master/README-GENERATOR.md#filtering-categories){:target="_blank"}를 참고한다.

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

## 카테고리 분류

일반 포스트와 TIL 포스트의 노출을 분리하기 위해선 포스트 파일의 카테고리를 나눠야 했는데 `categories` 에 `post` 와 `today-i-learned` 이 두 가지로만 설정하기로 했다.

## 머리말 설정

> **참고하기!**
> - layout: 사용할 레이아웃 파일
> - permalink: 페이지 주소
> - pagination/enabled: 페이지 매김 활성화 여부
> - pagination/category: 노출할 포스트 카테고리

### 파일 생성

`today-i-learned.html` 파일을 새로 생성하고 TIL 포스트만 노출하기 위해 아래와 같이 설정한다.

```markdown
---
layout: article-list
permalink: /today-i-learned/
pagination: 
  enabled: true
  category: today-i-learned
---
```

### 파일 변경

`index.html` 파일에는 일반 포스트를 노출한다.

```markdown
---
layout: article-list
permalink: /
pagination: 
  enabled: true
  category: post
---
```

## 코드 변경

페이지 매김을 구현하기 위해 포스트 목록 레이아웃 파일을 변경한다.

### 목록

{% raw %}
```html
<div class="post-list">
  <h2 class="is-blind">포스트 목록</h2>
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

### 페이지 매김

{% raw %}
```html
<nav class="pagination">
  <div class="pagination__wrapper">
    <h2 class="is-blind">포스트 페이지 매김</h2>
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
              <em role="link" aria-disabled="true" aria-label="현재 페이지, {{ trail.num }}번 페이지" aria-current="page" class="pagination__anchor is-active">{{ trail.num }}</em>
            {% else %}
              <a href="{{ trail.path | prepend: site.baseurl | replace: 'index.html', '' }}" aria-label="{{ trail.num }}번 페이지" class="pagination__anchor">{{ trail.num }}</a>
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

플러그인 적용을 마무리하고 나는 바로 원격 저장소에 파일을 올려 확인하는 과정을 거쳤다. 그런데 로컬에서 확인한 결과와 다르게 게시글이 노출되지 않는 이슈가 생겼는데 어떠한 문제인지 잘 파악이 되지 않아서 다른 저장소를 생성하여 테스트해보는 형태로 문제점을 짚어나가기로 했다.

## 원인 및 해결 방안

테스트를 진행하면서 jekyll-paginate-v2를 적용하기만 하면 이상하게 게시글이 노출되지 않았다. 로컬에서는 분명 문제없이 잘 동작하는데 말이다. 나는 의아해하며 이 이슈를 구글에 검색하고 경악을 금치 못했는데 이유는 바로 플러그인 문서에 아래와 같이 기술이 되어 있었다.

> Please note that this plugin is currently NOT supported by GitHub pages. Here is a list of all plugins supported. There is work underway to try to get it added it but until then please follow this GitHub guide to enable it or use Travis CI.

그렇다. 이 플러그인은 Github Pages에서 지원([지원하는 플러그인 목록](https://pages.github.com/versions/){:target="_blank"})되지 않았다. 이를 사용하기 위해선 [Travis CI](https://ayastreb.me/deploy-jekyll-to-github-pages-with-travis-ci/){:target="_blank"} 또는 [GitLab](https://about.gitlab.com/devops-tools/){:target="_blank"}를 사용하는 등 여러 방법 중 하나를 택하여야 했다. 하지만 수많은 고민 끝에 번거롭거나 이렇게까지 해서 사용해야 하나 싶을 정도라 생각되어 코드를 원복하기로 했다.

## 마무리

결론은 jekyll-paginate-v2 적용에 실패했다. 문서만 꼼꼼히 읽었다면 이런 삽질은 안 했어도 됐을 텐데 말이다. 이는 내 습관이 불러온 결과라 앞으로 어떻게 개선해 나가야 할지 몹시 고민이다. 그리고 이 사례가 내 블로그에서 일어나서 정말 다행이였는데 개인 작업이 아닌 회사 업무였다면 정말 지금 생각만 해도 너무 아찔하다.

카테고리 메뉴 분리 작업은 차차 진행하기로 하고 우선 포스트의 작성에 집중하기로 마음을 바꿨다. TIL 포스트는 하루하루가 아닌 일주일 간격으로 작성해 일반 포스트가 TIL 포스트에 묻히지 않게끔 진행하기로 했다.

## 참고 문서

- [https://jekyllrb-ko.github.io/](https://jekyllrb-ko.github.io/){:target="_blank"}
- [https://github.com/sverrirs/jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2){:target="_blank"}
- [https://ayastreb.me/deploy-jekyll-to-github-pages-with-travis-ci/](https://ayastreb.me/deploy-jekyll-to-github-pages-with-travis-ci/){:target="_blank"}
- [https://about.gitlab.com/devops-tools/](https://about.gitlab.com/devops-tools/){:target="_blank"}
- [https://pages.github.com/versions/](https://pages.github.com/versions/){:target="_blank"}