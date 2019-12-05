---
id: 911
title: 청소구역뽑기 앱을 만드는 여정
date: 2019-06-23T20:10:00+09:00
author: yongjin0802
layout: post
guid: https://yongj.in/?p=911
permalink: '/2019/06/23/%ec%b2%ad%ec%86%8c%ea%b5%ac%ec%97%ad%eb%bd%91%ea%b8%b0-%ec%95%b1%ec%9d%84-%eb%a7%8c%eb%93%9c%eb%8a%94-%ec%97%ac%ec%a0%95/'
categories:
  - Development
  - Web Programming
tags:
  - Python
  - React.js
  - Vue.js
---
청소시간에 청소구역을 추첨하는 시간을 줄이고자 청소구역뽑기 앱을 만들고있다.

지금까지 4가지 버전이 나왔다.

  1. Pythonista로 만든 단순 랜덤
  2. React로 만든 랜덤 뽑기
  3. Vue로 만든 카드 옮기기
  4. Vue로 만든 스마트tv에서 사용가능한 랜덤뽑기

### 1. Pythonista로 만든 단순 랜덤<figure class="wp-block-image">

<img src="https://yongj.in/wp-content/uploads/2019/04/kakaotalk_20190415_192700687.jpg" alt="" class="wp-image-804" srcset="https://yongj.in/wp-content/uploads/2019/04/kakaotalk_20190415_192700687.jpg 960w, https://yongj.in/wp-content/uploads/2019/04/kakaotalk_20190415_192700687-300x225.jpg 300w, https://yongj.in/wp-content/uploads/2019/04/kakaotalk_20190415_192700687-768x575.jpg 768w, https://yongj.in/wp-content/uploads/2019/04/kakaotalk_20190415_192700687-401x300.jpg 401w" sizes="(max-width: 960px) 100vw, 960px" /> </figure> 

랜덤으로 청소구역을 할당한다. 

구현은 간단했지만 문제가 많았다. 

5일 연속으로 화장실 청소를 하게된 인원의 불만과 개발자에 대한 조작 의혹 생겨났다. 

다른 방식을 생각해내야했다.

### 2. React로 만든 랜덤 뽑기<figure class="wp-block-image">

<img src="https://i2.wp.com/yongj.in/wp-content/uploads/2019/06/파일_001.png?fit=840%2C630&ssl=1" alt="" class="wp-image-912" srcset="https://yongj.in/wp-content/uploads/2019/06/파일_001.png 2732w, https://yongj.in/wp-content/uploads/2019/06/파일_001-300x225.png 300w, https://yongj.in/wp-content/uploads/2019/06/파일_001-768x576.png 768w, https://yongj.in/wp-content/uploads/2019/06/파일_001-1024x768.png 1024w, https://yongj.in/wp-content/uploads/2019/06/파일_001-1000x750.png 1000w, https://yongj.in/wp-content/uploads/2019/06/파일_001-400x300.png 400w" sizes="(max-width: 2732px) 100vw, 2732px" /> </figure> 

가위바위보로 정한 순서대로 랜덤으로 섞인 청소구역을 고르는 방식이다.

추첨 방식의 공정한 덕분에 몇달동안 불만없이 잘 사용했다.

개발 당시 웹 프로그래밍을 3달만에 처음한 상태라 만드는데 시간이 많이 걸렸다.

싸지방을 들락거리며 카드 뒤집기 효과와 리액트로 돔 업데이트하는 법을 찾아 만들었다.

### 3. Vue로 만든 카드 옮기기 <figure class="wp-block-image">

<img src="https://i0.wp.com/yongj.in/wp-content/uploads/2019/06/청소인원뽑기1.png?fit=840%2C495&ssl=1" alt="" class="wp-image-913" srcset="https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기1.png 1354w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기1-300x177.png 300w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기1-768x452.png 768w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기1-1024x603.png 1024w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기1-1000x589.png 1000w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기1-510x300.png 510w" sizes="(max-width: 1354px) 100vw, 1354px" /> <figcaption>청소자의 이름이 적힌 카드를 옮겨 청소구역을 정한다.</figcaption></figure> <figure class="wp-block-image"><img src="https://i1.wp.com/yongj.in/wp-content/uploads/2019/06/청소인원뽑기2.png?fit=840%2C495&ssl=1" alt="" class="wp-image-915" srcset="https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기2.png 1349w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기2-300x177.png 300w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기2-768x453.png 768w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기2-1024x604.png 1024w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기2-1000x590.png 1000w, https://yongj.in/wp-content/uploads/2019/06/청소인원뽑기2-508x300.png 508w" sizes="(max-width: 1349px) 100vw, 1349px" /><figcaption>콤보박스로 쉽게 인원을 추가하고 삭제할 수 있다.</figcaption></figure> 

가위바위보 순서대로 청소구역을 선택하는데 자신뿐만 아니라 남의 청소구역을 정할 수 있다.

맘에 안드는 사람을 공공구역으로 보내버릴 수 있는 재미를 추가했다.

추가로

  1. 공공구역과 청소자, 청소인원을 수정하기 쉽다.
  2. PWA 파일 캐시 기능과 LocalStorage 기능을 사용하여 아이패드에서 앱처럼 다운 받고 오프라인으로 사용가능하다.
  3. 휴가/근무자에 인원을 추가하면 청소구역이 인원에 맞게 조정되는데 이미 옮긴 카드 중 변동이 없는 구역의 카드는 그대로 둔다. 옮긴 카드를 다시 옮기는 수고를 덜 수 있다.

한편, 청소자들이 구역 선택 고민하느라 시간이 소모되고 남을 공공구역으로 보냈다가 자신도 공공구역에 끌려가는 복수를 당하는 일이 빈번했다.

기존의 랜덤 뽑기 방식이 낫다는 의견을 수용하여 이 앱은 폐기하고 2번 앱으로 회귀했다.

소스코드 : <https://github.com/16Yongjin/vue-cleaner-picker> 

### 4. Vue로 만든 스마트tv 리모컨 랜덤뽑기

생활관에 있는 기가지니는 웹브라우저가 내장되어있다.<figure class="wp-block-image">

![](https://t1.daumcdn.net/cfile/tistory/267FDC3858880E7515) <figcaption>기가지니 리모컨  
출처: 스마트블로그</figcaption></figure> 

웹브라우저 사용 시 리모컨 숫자 키패드를 누르면 일반 키보드 입력처럼 keypress 이벤트가 발생한다.

이를 2번 랜덤뽑기 방식에 적용해 리모컨으로 청소구역을 뽑을 수 있게 했다.<figure class="wp-block-image">

<img src="https://i0.wp.com/yongj.in/wp-content/uploads/2019/06/청소뽑기-티비.png?fit=840%2C492&ssl=1" alt="" class="wp-image-916" srcset="https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비.png 1349w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비-300x176.png 300w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비-768x450.png 768w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비-1024x600.png 1024w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비-1000x586.png 1000w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비-512x300.png 512w" sizes="(max-width: 1349px) 100vw, 1349px" /> </figure> 

청소인원을 선택 후<figure class="wp-block-image">

<img src="https://i0.wp.com/yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1.png?fit=840%2C495&ssl=1" alt="" class="wp-image-917" srcset="https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1.png 2692w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1-300x177.png 300w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1-768x453.png 768w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1-1024x604.png 1024w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1-1000x590.png 1000w, https://yongj.in/wp-content/uploads/2019/06/청소뽑기-티비2-1-509x300.png 509w" sizes="(max-width: 2692px) 100vw, 2692px" /> <figcaption>1 ~ 6 사이 숫자를 누르면 구역이 선택된다. 0을 누르면 인원을 선택하는 페이지로 되돌아간다.</figcaption></figure> 

번호에 해당하는 카드를 리모컨 숫자버튼으로 선택한다.

내 아이패드가 없어도 청소구역을 뽑을 수 있고, 다른 생활관에서도 사용가능하다.

기가지니 내장 브라우저가 구형이라 polyfill을 사용했고 backface-visibility와 margin: auto 속성이 적용이 안돼서 실제 사용 중인 버전에서는 카드 뒤집기 효과를 뺀 게 조금 아쉽다.

소스코드 : <https://github.com/16Yongjin/vue-cleaner-card-for-TV>

### 마치며

군대에서도 일상의 불편함을 발견하고 프로그래밍으로 해결하는 것이 가능하다.