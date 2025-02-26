---
tags:
  - jekyll
Created: Invalid date
Updated: Invalid date
---
# 지킬(Jekyll) 블로그 카테고리(category) 만들기

AUGUST 7, 2018

<p>포스트 개수가 많아지다 보니 관리가 힘들어서 카테고리를 만들었다. 카테고리 만든 방법을 간단하게 정리하였다.</p>

> 1. _layouts 폴더에 category.html 파일 생성

먼저 _layouts 폴더에 category.html 파일을 생성해준다.

![[untitled 10.jpg|untitled 10.jpg]]

category.html은 category 이름에 맞는 포스트들의 타이트들을 리스트로 보여준다. 코드는 아래와 같다.

---

layout: default

---

**<ul** class="posts-list"**>**

{% assign category = page.category | default: page.title %}

{% for post in site.categories[category] %}

**<li>**

**<h3>**

**<a** href="{{ site.baseurl }}{{ post.url }}"**>**

{{ post.title }}

**</a>**

**<small>**{{ post.date | date_to_string }}**</small>**

**</h3>**

**</li>**

{% endfor %}

**</ul>**

> 2. _includes 폴더의 index.html 파일 수정

아래의 내용과 같이 수정한다.

**<header** class="site-category"**>**

**<ul>**

{% assign pages_list = site.pages %}

{% for node in pages_list %}

{% if node.title != null %}

{% if node.layout == "category" %}

**<li><a** class="category-link {% if page.url == node.url %} active{% endif %}"

href="{{ site.baseurl }}{{ node.url }}"**>**{{ node.title }}**</a></li>**

{% endif %}

{% endif %}

{% endfor %}

**</ul>**

**</header>**

> 3. category 폴더 생성

(맨 바깥의 디렉토리) [계정명.github.io](http://xn--989aw4xurk.github.io/) 폴더 안에 category 폴더를 만들어준 다음 원하는 카테고리 명의 markdown 파일을 추가해준다.

![[untitled 1 4.jpg|untitled 1 4.jpg]]

마크다운 파일 내용은 아래와 같다.

---

layout: category

title: 여기에 카테고리 이름 입력!

---

예를들어, docker 카테고리를 만들고 싶다면 category 폴더의 docker.md의 내용은 다음과 같다.

![[untitled 2 3.jpg|untitled 2 3.jpg]]

> 4. 블로그 포스트에 category 추가하기

위의 세가지 셋팅 후 포스트를 작성 시 카테고리 항목만 추가하여 주면 카테고리 지정이 된다.

![[untitled 3 3.jpg|untitled 3 3.jpg]]

위의 이미지처럼 categories 항목을 추가해주고 원하는 카테고리 이름을 작성해주면 된다. (복수 카테고리도 가능하다.)

주의 해야 할 점은 반드시! category 폴더에 원하는 category를 만들어주고 포스트에 같은 카테고리 명을 입력해야 한다.