---
layout: article-view
title:  "Welcome to Jekyll!"
summary: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.
date:   2019-04-15 12:06:41 +0900
categories: today-i-learned
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

<pre class="codepen" data-height="470" data-type="result" data-href="kjmBd" data-user="andymcfee" data-safe="true"><code></code><a href="http://codepen.io/andymcfee/pen/kjmBd">Check out this Pen!</a></pre>
<script async src="http://codepen.io/assets/embed/ei.js"></script>

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

```javascript
function example() {
  alert('example alert!');
}

example();
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

- 나라별 시간대 차이에 대한 더 자세한 내용은 여기를 참고해주세요.

    - Test List Item 01
    - Test List Item 02
    - Test List Item 03
- Test List 02
- 나라별 시간대 차이에 대한 더 자세한 내용은 여기를 참고해주세요.

    - Test List Item 01
    - Test List Item 02
    - Test List Item 03
- 나라별 시간대 차이에 대한 더 자세한 내용은 여기를 참고해주세요.

- 나라별 시간대 차이에 대한 더 자세한 내용은 여기를 참고해주세요.


1. 시간대를 명시합시다.
1. 시각을 애플리케이션 로직이나 데이터베이스에서 저장할 때는 UTC로 사용하고, 유저에게 표시할 때만 유저의 시간대로 변환하여 보여주도록 합시다.
1. 시간대를 명시합시다.
1. 시각을 애플리케이션 로직이나 데이터베이스에서 저장할 때는 UTC로 사용하고, 유저에게 표시할 때만 유저의 시간대로 변환하여 보여주도록 합시다.
1. 시간대를 명시합시다.
1. 시각을 애플리케이션 로직이나 데이터베이스에서 저장할 때는 UTC로 사용하고, 유저에게 표시할 때만 유저의 시간대로 변환하여 보여주도록 합시다.

## h2 Heading
### h3 Heading
---

## Emphasis

**This is bold text**

__This is bold text__

*This is italic text*

_This is italic text_

~~Strikethrough~~

---

## Blockquotes


> Blockquotes can also be nested...
>> ...by using additional greater-than signs right next to each other...
> > > ...or with spaces between arrows.

> Blockquotes can also be nested...
> 1. Lorem ipsum dolor sit amet
> 2. Consectetur adipiscing elit
> 3. Integer molestie lorem at massa

---

Unordered

+ Create a list by starting a line with `+`, `-`, or `*`
+ Sub-lists are made by indenting 2 spaces:
  - Marker character change forces new list start:
    * Ac tristique libero volutpat at
    + Facilisis in pretium nisl aliquet
    - Nulla volutpat aliquam velit
+ Very easy!

Ordered

1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa


1. You can use sequential numbers...
1. ...or keep all the numbers as `1.`

Start numbering with offset:

57. foo
1. bar

## Code

Inline `code`

Indented code

    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code


Block code "fences"

```
Sample text here...
```

Syntax highlighting

``` js
var foo = function (bar) {
  return bar++;
};

console.log(foo(5));
```

## Tables

| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

Right aligned columns

| Option | Description |
| ------:| -----------:|
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |

