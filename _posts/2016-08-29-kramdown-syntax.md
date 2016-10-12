---
layout: post
title:  "markdown vs kramdown 차이점"
cover: default.png
date:   2016-08-29 19:43:17 +0900
categories: posts
tags: 마크다운
---

필자는 마크다운을 접한지는 1년정도 되었다. 한때 강의 필기도 마크다운으로 할 만큼 굉장히 재미들렸던 적도 있다. 무엇보다 마크다운을 쓰게된 것은 텍스트를 쓰는 도중에 설정할 수 없는 진한 글, 기울여진 글 등을 편하게 쓸 수 있기 때문이다. 아래 글을 보며 자세히 살펴보자.

## 마크다운(Markdown)이란?

마크다운은 어떤 문서, 즉 txt(텍스트 파일), hwp(한글 파일), doc등을 작성할때의 문법 종류 중 하나를 말한다.

가령 본인이 "나는 알고리즘을 공부한다."를 작성하고 싶다고 가정하자. 이 문장을 txt, html, markdown으로 작성한다면 이렇다.

### txt의 경우.
{% highlight plaintext linenos %}
나는 알고리즘을 공부한다.
{% endhighlight %}

### html의 경우.
{% highlight html linenos %}
<p>나는 알고리즘을 공부한다.</p>
{% endhighlight %}

### markdown의 경우.
{% highlight markdown linenos %}
나는 알고리즘을 공부한다.
{% endhighlight %}

얼핏보면 txt와 markdown으로 작성하는 문장은 작성방법이 같다고 생각할 수 있지만, 실제론 다른점이 많다. 예를 들어 위 문장을 진하게, 즉 **bold** 처리 하고 싶다면 이런식이다.

### txt의 경우.
{% highlight plaintext linenos %}
나는 알고리즘을 공부한다.
=> 이후 텍스트 편집기 메뉴에서 진하게 처리 한다.
{% endhighlight %}

### markdown의 경우.
{% highlight markdown linenos %}
** 나는 알고리즘을 공부한다.**
{% endhighlight %}

다시 말하자면, hwp는 글씨를 **진하게**(**bold**), 글씨를 *기울게*(*italic*) 등을 할 경우, 글씨를 쓰는 도중에 글에 블록을 씌우고 버튼이던, 단축키던 눌러야 하지만, 마크다운의 경우 글을 쓰는동안에도 멈추지않고 계속 쓸 수 있는 장점이 있다.

이는 빠르게 적는 강의 필기에서 매우 강점을 보인다. 예를 들어, 자신이 강의 필기를 하는 중에 어떤 글을 강조하고 싶을 때, 글을 멈추지 않고 바로 하이라이트 표시 할 수 있다는 것이다.

마크다운은 이 외에도, 머릿말, 표, 하이퍼링크, 그림 등을 넣을때 어려움없이 바로 넣을 수 있다. 심지어 이 블로그의 모든 글은 마크다운으로 작성되어있다(!).

## 크렘다운(Kramdown)은 뭐지?

이런 마크다운이라도 역시 한계가 있기 마련이다. 이런 마크다운을 약간 개조한 것 으론 Github-Flavored Markdown, GFM 등이 있고, 지금부터 소개할 Kramdown 역시 개조판이다. Kramdown은 이 블로그의 엔진인 Jekyll에서 필자가 채택한 마크다운 엔진 이라, 알아보게 되었다.

헷갈릴만한 문법 중 하나를 예를 들어 소개해보자 한다. 먼저 헤더, headers가 다르다. 예를 들면 이렇다.

{% highlight plaintext linenos %}
##나는 알고리즘을 공부한다.
=> 마크다운은 ##과 텍스트 사이에 띄어쓰기를 안해야 한다.
## 나는 알고리즘을 공부한다.
=> 크렘다운은 ##과 텍스트 사이에 띄어쓰기를 해야 한다.
{% endhighlight %}

필자는 이 요소때문에 헤더를 아예 안쓰다가 최근에 쓰기 시작했다(...). 이 이외에 차이점은 하단의 관련문서를 확인하시라.

## 관련문서

- [마크다운](https://namu.wiki/w/마크다운)
- [Kramdown Quick Reference](http://kramdown.gettalong.org/quickref.html)
