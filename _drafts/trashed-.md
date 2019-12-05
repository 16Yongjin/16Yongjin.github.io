---
id: 585
date: 2018-01-19T21:58:48+09:00
author: yongjinsite
layout: post
guid: https://yongjinsite.wordpress.com/?p=585
permalink: /2018/01/19/__trashed/
categories:
  - 기타
---
&nbsp;

Vue.js + Vue material로 음식추천앱 UI를 만들었다.

Vuetify라는 대안도 있었지만 Vue material이 더 안드로이드다운 느낌을 준다.

다만, 타이틀바와 바텀 네비게이션을 제외한 메인뷰의 높이를 바닐라 자바스크립트로 구하고 있는데

그 높이를 반응형으로 만드는 게 가장 큰 과제이다.

이 글을 쓰다가 방법이 생각났다.

바로 js listen to user screen size 을 구글링하면 되는 거였다.

<pre class="default prettyprint prettyprinted"><code>&lt;span class="pln">window&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">addEventListener&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str">'resize'&lt;/span>&lt;span class="pun">,&lt;/span> &lt;span class="kwd">function&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="kwd">event&lt;/span>&lt;span class="pun">){&lt;/span>
  &lt;span class="com">// do stuff here&lt;/span>
&lt;span class="pun">});&lt;/span></code></pre>

을 코드에 추가하면 된다.