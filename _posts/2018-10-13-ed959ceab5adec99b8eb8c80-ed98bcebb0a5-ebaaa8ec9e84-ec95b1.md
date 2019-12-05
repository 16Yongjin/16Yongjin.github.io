---
id: 799
title: 한국외대 혼밥 모임 앱
date: 2018-10-13T23:19:32+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=799
permalink: '/2018/10/13/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ed%98%bc%eb%b0%a5-%eb%aa%a8%ec%9e%84-%ec%95%b1/'
timeline_notification:
  - "1539440374"
categories:
  - Development
tags:
  - Node.js
  - Vue.js
---
<div class="">
  <div>
  </div>
  
  <div class="_1mf _1mj">
    <span>기존의 학교 계정으로 가입 가능</span>
  </div>
  
  <div>
  </div>
</div>

<div class="">
</div>

<div class="">
  <div>
  </div>
</div>

<div>
  <strong>프런트엔드</strong>
</div>

<div>
</div>

<div class="">
  <div class="_1mf _1mj">
    <span>1. 타입스크립트 사용했고 Vuex Store까지 타입 도입</span>
  </div>
  
  <div>
  </div>
  
  <div>
    <div class="">
      <div class="_1mf _1mj">
        <span>2. 로그인 & 회원가입 창을 통합하고</span>
      </div>
      
      <div>
      </div>
    </div>
    
    <div class="">
      <div class="_1mf _1mj">
        <span>모임 생성 시 정보를 한번에 하나씩 입력하는 UI를 적용해서 </span>인지 부담을 줄임
      </div>
    </div>
  </div>
</div>

<div>
</div>

<div>
  3. Vue도 상태없는 함수형 컴포넌트를 사용하면 편하다는 것을 깨달음
</div>

<div>
</div>

<div>
  Vuex 액션 단에서 대부분의 로직 처리 후
</div>

<div>
</div>

<div>
  템플릿에 데이터만 연결하면 스크립트 코드가 없어서 뇌가 편함
</div>

<div>
</div>

<div>
  ex)
</div>

<div>
  <img class="alignnone size-full wp-image-801" src="https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46.png" alt="스크린샷 2018-10-13 오후 11.08.46" width="1076" height="886" srcset="https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46.png 1076w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46-300x247.png 300w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46-768x632.png 768w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46-1024x843.png 1024w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46-1000x823.png 1000w, https://yongj.in/wp-content/uploads/2018/10/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-10-13-e1848be185a9e18492e185ae-11-08-46-364x300.png 364w" sizes="(max-width: 1076px) 100vw, 1076px" />
</div>

<div>
</div>

<div>
</div>

<div class="">
  <div class="_1mf _1mj">
    <strong>백엔드</strong>
  </div>
  
  <div>
  </div>
  
  <div class="_1mf _1mj">
    <span>1. 변수 사용 안 함</span>
  </div>
</div>

<div>
</div>

<div>
  2. JWT 사용
</div>

<div class="">
  <div>
  </div>
  
  <div class="_1mf _1mj">
    <span>3. 읽기 쉬운 평서문 코드 작성하려고 고민 많이 함 (ex, user.join(meetup))</span>
  </div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
  <strong>보완점</strong>
</div>

<div>
</div>

<div>
  &#8211; DB  모델을 Meetup, User에서 Meeup, Chat, User 세 개로 나누기
</div>

<div>
</div>

<div>
  Meetup 안에 Chat이 들어있어서 Meeup 리스트 가져올 때마다 Chat 전체도 가져와야 함
</div>

<div>
</div>

<div>
  <strong>추가 기능</strong>
</div>

<div>
</div>

<div>
  &#8211; 내가 쓴 채팅 색깔 다르게 표시
</div>

<div>
</div>

<div>
  &#8211; 채팅창 밖에서 받은 채팅 스낵바로 표시
</div>

<div>
</div>

<div>
  &#8211; 모임 생성 시 lento.in의 장소 데이터와 연동할 수 있게 하기
</div>

<div>
</div>

<div>
  &#8211; Nest.js 도입하기
</div>

<div>
</div>

<div>
</div>

<div>
  약 40시간 뒤 입대&#8230; 군대가서 완성해야 겠다.
</div>