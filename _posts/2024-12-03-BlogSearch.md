---
title: "github.io 검색엔진(구글)에 노출시키기"
date: 2024-06-22 19:33:00 +09:00
categories: [Blog]
tags:
  [
    blog
  ]
---

# 검색엔진 노출시키기

힘들게 github.io로 블로그를 만들어도 구글같은 검색 엔진에 검색이 안된다면 의미가 없기 때문에 먼저 구글에 노출시키는게 좋다고 생각했다.


## Google search console

![1](./assets/img/postsImg/20241203/googlesearch.png)


[Google search console](https://search.google.com/search-console/about)은 구글에 내 블로그 내용이 검색되도록 해주는 서비스다. 

링크에 들어가 시작하기를 누르고 오른쪽 도메인에 블로그 주소를 적어준다.

![1](./assets/img/postsImg/20241203/googlesearch2.png)

![1](./assets/img/postsImg/20241203/googlesearch3.png)

그리고 html 파일을 다운받는데 이 파일을 내 깃허브 블로그 root 위치에 추가해주고 커밋, 푸쉬를 하면 1~2분 정도 뒤에 소유권 인정이 된다.

![1](./assets/img/postsImg/20241203/googlesearch4.png)



## sitemap.xml, robots.txt 추가하기
```
---
layout: null
---

<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    {% for post in site.posts %}
    <url>
        <loc>{{ site.url }}{{ post.url }}</loc>
        {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
        {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
        {% endif %}

        {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
        {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
        {% endif %}

        {% if post.sitemap.priority == null %}
        <priority>0.5</priority>
        {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
        {% endif %}

    </url>
    {% endfor %}
</urlset> 
```
sitemap.xml을 root에 만들고 복사 붙여넣기 한다. sitemap.xml을 통해 Google 크롤러가 url을 체크할 수 있게된다. 아까 구글 서치 콘솔에서 속성 -> Sitemaps에 추가해 알 수 있다.

```
User-agent: *
Allow: /
Sitemap: {{ '/sitemap.xml' | relative_url | prepend: site.url }}
```
robots.txt또한 root에 똑같이 만들어 추가한다. 

접근하는 크롤러는 robots.txt를 보고 접근하고자 하는 sitemap의 위치를 확인하고,
제한을 확인하여 본래의 웹사이트로 가져가게 된다.
