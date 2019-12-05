---
id: 1005
title: Get better at JavaScript with just JavaScript
date: 2019-11-26T00:58:36+09:00
author: yongjin0802
layout: post
guid: https://yongj.in/?p=1005
permalink: /2019/11/26/get-better-at-javascript-with-just-javascript__trashed/
mytory_md_path:
  - https://raw.githubusercontent.com/16Yongjin/TIL/master/Javascript/Get-better-at-JavaScript-with-just-JavaScript.md
mytory_md_text:
  - ""
mytory_md_mode:
  - url
categories:
  - Javascript
tags:
  - DOM
  - javascript
---
### 출처: https://youtu.be/pws4qzGn5ak

# Intersection Observer

한 요소가 화면 안으로 들어왔는지 확인할 때 사용한다.

  * 스크롤 시 요소에 애니메이션 넣기
  * 스크롤 시 비디오 재생
  * 이미지 지연로딩
  * 광고 노출수 세기
  * 스티키 헤더

등에 사용할 수 있다.

### 1. 옵션 설정

`javascript<br />
const options = {<br />
  root: document.querySelector(".scrollingDiv"),<br />
  rootMargin: "100px",<br />
  // 화면에 없을 때, 반만, 완전히 들어왔을 때 알려줌<br />
  threshold: [0, 0.5, 1.0]<br />
};`

### 2. 빈 Observer 생성

`javascript<br />
const observer = new IntersectionObserver(callback, options);`

### 3. 콜백 전달하기

`javascript<br />
const callback = (entries, observer) => {<br />
  entries.forEach(entry => {<br />
    console.log(entry);<br />
    // threshold가 1일 때(요소가 완전히 들어왔을 때)만 보이게 하기<br />
    if (entry.isIntersecting && entry.intersectionRatio >= 1) {<br />
      entry.target.classList.add("visible");<br />
    } else {<br />
      entry.target.classList.remove("visible");<br />
    }<br />
    observer.unobserve(entry.target);<br />
  });<br />
};`

### 4. 관찰 시작

`javascript<br />
const boxes = document.querySelectorAll(".box");<br />
boxes.forEach(box => observer.observe(box));`

* * *

# Resize Observer

요소의 크기 변경을 확인할 수 있다.

### 기본 예제

&#8220;\`javascript const callback = (entries, observer) => { entries[0].target.innerHTML = `<pre><br />
      ${JSON.stringify(entries[0].contentRect, null, " ")}<br />
    </pre>`; };

const observer = new ResizeObserver(callback);

const element = document.querySelector(&#8220;.resize&#8221;); observer.observe(element); &#8220;\`

요소 크기를 Viewport에 맞추는게 아니라 다른 요소가 얼마나 큰지, 어디에 있는 지 등, 내가 원하는 대로 지정하고 싶을 때 사용할 수 있다.

&#8220;\`javascript const callback = (entries, observer) => { const { width } = entries[0].contentRect; if (width > 400) { size = &#8220;large&#8221;; } else if (width > 300) { size = &#8220;medium&#8221;; } else { size = &#8220;small&#8221;; }

entries[0].target.classList.remove(&#8220;small&#8221;, &#8220;medium&#8221;, &#8220;large&#8221;); entires[0].target.classList.add(size); };

const observer = new ResizeObserver(callback); const element = document.querySelector(&#8220;.videos__list&#8221;); observer.observe(element); &#8220;\`

* * *

# DOM Element Methods

## 1. .closest()

입력받은 선택자에 일치하는 가장 가까운 조상요소를 찾는다.

`HTML<br />
<div class="cards"><br />
  <div class="card"><br />
    <p>I'm a Card</p><br />
    <button>Delete</button><br />
  </div><br />
  <div class="card"><br />
    <p>I'm a Card</p><br />
    <button>Delete</button><br />
  </div><br />
</div>`

2개의 카드가 있는 div요소가 있고 각 카드는 삭제 버튼이 있다.

`javascript<br />
document.querySelectorAll(".card button").forEach(button => {<br />
  button.addEventListener("click", e => {<br />
    e.currentTarget.closest(".card").remove();<br />
  });<br />
});`

closest 메서드로 버튼의 조상인 .card div를 찾아서 삭제한다.

&#8220;\`javascript const p = document.querySelector(&#8220;p&#8221;);

document.addEventListener(&#8220;click&#8221;, e => { const isOutsize = !e.target.closest(&#8220;.modal-inner&#8221;); p.textContent = `You Clicked ${isOutsize ? "Outsize" : "Insize"}!`; }); &#8220;\`

요소 밖을 클릭했는지 안을 클릭했는지 확인할 때도 유용하다.

## 2. .matches()

한 요소가 선택자와 일치하는지 확인한다.

`javascript<br />
button.addEventListener("click", e => {<br />
  if (e.currentTarget.matches(".available[data-price]")) {<br />
    // .. 처리<br />
  }<br />
});`

버튼이 data-price 라는 애트리뷰트를 갖고 있는지 확인한다.

`javascript<br />
// list는 JS로 아이템을 추가/삭제하는 빈 요소임<br />
list.addEventListener("click", e => {<br />
  if (e.target.matches("button")) {<br />
    deleteItem(parseFloat(e.target.value));<br />
  }<br />
});`

Event Delegation에도 사용한다. 모든 리스트 내의 아이템에 이벤트 리스너를 붙일 필요가 없다.

## 3. .contains()

&#8220;\`javascript const modal = document.querySelector(&#8220;.modal&#8221;); modal.contains(button); // true

modal.querySelector(&#8220;button&#8221;); // <button></button> // contains 메서드와 같음 !!modal.querySelector(&#8220;button&#8221;); // true &#8220;\`

* * *

# Bling.js

바닐라 JS앱을 만들 때 있으면 유용한 11줄짜리 라이브러리

&#8220;\`javascript window.$ = document.querySelector.bind(document); window.$$ = document.querySelectorAll.bind(document);

Node.prototype.on = window.on = function(name, fn) { this.addEventListener(name, fn); };

NodeList.prototype.**proto** = Array.prototype;

NodeList.prototype.on = function(name, fn) { this.forEach(function(elem, i) { elem.on(name, fn); }); }; &#8220;\`

입력하기 힘든 document.querySelector를 \$ 한 문자로 줄임

NodeList에서 Array의 메서드를 사용할 수 있게 함

* * *

# 데이터 다루기

## 1. Array.from()

&#8220;\`javascript Array.from({ length: 3 }); // => [undefined, undefined, undefined]

Array.from({ length: 3 }, () => `💰`); // => [&#8220;💰&#8221;, &#8220;💰&#8221;, &#8220;💰&#8221;] &#8220;\`

iterable을 array로 변환한다.

``javascript<br />
Array.from({ length: 3 }, (_, i) => `day-${i + 1}`);<br />
// => [ "day-1", "day-2", "day-3" ]``

하드코딩을 피하고 원하는 데이터가 담긴 리스트 생성할 때 유용하다.

&#8220;\`javascript Array.from({ length: 12 }, (x, index) => new Date(0, index + 1, 0).toLocaleDateString(&#8220;en-US&#8221;, { month: &#8220;short&#8221; }) ); // => [ &#8220;Jan&#8221;, &#8220;Feb&#8221;, &#8220;Mar&#8221;, &#8220;Apr&#8221;, &#8220;May&#8221;, &#8220;Jun&#8221;, &#8220;Jul&#8221;, &#8220;Aug&#8221;, &#8220;Sep&#8221;, &#8220;Oct&#8221;, &#8220;Nov&#8221;, &#8220;Dec&#8221;]

Array.from({ length: 12 }, (x, index) => new Date(0, index + 1, 0).toLocaleDateString(&#8220;ko-KR&#8221;, { month: &#8220;short&#8221; }) );

// => [ &#8220;1월&#8221;, &#8220;2월&#8221;, &#8220;3월&#8221;, &#8220;4월&#8221;, &#8220;5월&#8221;, &#8220;6월&#8221;, &#8220;7월&#8221;, &#8220;8월&#8221;, &#8220;9월&#8221;, &#8220;10월&#8221;, &#8220;11월&#8221;, &#8220;12월&#8221;] &#8220;\`

달 이름 생성할 때 사용할 수 있다.

* * *

# 중복 요소 제거하기

&#8220;\`javascript const values = [1, 2, 3, 1, 2]

Array.from(new Set(values)) // [1, 2, 3]

[&#8230;new Set(values)] // [1, 2, 3] &#8220;\`

* * *

# &#8230;spread and &#8230;rest

&#8220;\`javascript // 1:1 복사 const copyOfHuman = { &#8230;human };

// 복사 후 덮어쓰기 const copyNewId = { &#8230;human, id: &#8220;das-vader&#8221; };

// id를 뺀 모든 것 const { id, &#8230;withoutId } = human; &#8220;\`

객체 다루기

`javascript<br />
// 기존 배열를 변경하지 않고 배열 뒤집기<br />
const reversed = [...names].reverse();`

* * *

# 에러 핸들링

`javascript<br />
process.on("unhandledRejection", error => {<br />
  console.log("unhandledRejection", error);<br />
});`

근데 위와 같이 에러를 무시할 바엔 unhandledRejection 발생 시 프로세스를 종료하고 다시 시작하는게 낫다고 노드 베스트 프랙티스에 나와있다.

* * *

# Web 음성인식

SpeechRecognition API로 음성인식이 가능하다.

* * *

# Shape Detection

얼굴, 바코드, 텍스트를 인식할 수 있다.