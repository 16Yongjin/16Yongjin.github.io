---
id: 835
title: 한국외대 주변 식당 추천앱 Lento
date: 2019-04-21T15:10:25+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/736-revision-v1/
permalink: /2019/04/21/736-revision-v1/
---
겨울방학때부터 아르바이트 하고 남는 시간에 만든 학교 주변 식당 앱이다.

서버는 타입스크립트, koa.js, 몽고db를 사용했고

클라이언트는 Vuetify.js와 Nuxt.js 서버 사이드 렌더링을 통해

어드민은 Vuetify.js SPA로 만들었다.

&nbsp;

앱 이름은 포르투갈어로 게으른, 느린이라는 뜻을 가진 단어 Lento인데

사용자들이 이 앱을 통해 점심 고민할 때만은 게을러지길 바라는 목적에서 지은 이름이다.

&nbsp;

**카카오톡 플러스친구**

og-image로 식당의 음식 사진이나 구글 지도를 보여주는 카톡 플러스친구는 친구 100을 넘었다.

Nuxt로 SSR을 했기에 카톡 크롤러가 이미지를 가져와서 미리보기를 보여줄 수 있었다.

<div id='gallery-10' class='gallery galleryid-835 gallery-columns-3 gallery-size-thumbnail'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/05/20/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%a3%bc%eb%b3%80-%ec%8b%9d%eb%8b%b9-%ec%b6%94%ec%b2%9c%ec%95%b1-lento/kakaotalk_photo_2018-05-20-21-53-11_30/'><img width="150" height="150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/kakaotalk_photo_2018-05-20-21-53-11_30-150x150.jpeg" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/kakaotalk_photo_2018-05-20-21-53-11_30-150x150.jpeg 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/kakaotalk_photo_2018-05-20-21-53-11_30-85x85.jpeg 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/05/20/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%a3%bc%eb%b3%80-%ec%8b%9d%eb%8b%b9-%ec%b6%94%ec%b2%9c%ec%95%b1-lento/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-05-20-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-10-30-15/'><img width="150" height="150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-30-15-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-30-15-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-30-15-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure>
</div>

**어드민 대시보드**

JWT 토큰을 이용하여 로그인 기능을 구현했다.

<img class="alignnone  wp-image-737" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03.png" alt="스크린샷 2018-05-20 오후 10.14.03" width="675" height="414" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03.png 1259w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03-300x184.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03-768x471.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03-1024x628.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03-1000x613.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-03-489x300.png 489w" sizes="(max-width: 675px) 100vw, 675px" /> 

로그 수집을 시작하여 서버 요청 수를 보여주는 대시보드를 만들었다.

<img class="alignnone size-full wp-image-738" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29.png" alt="스크린샷 2018-05-20 오후 10.14.29" width="1256" height="768" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29.png 1256w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29-300x183.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29-768x470.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29-1024x626.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29-1000x611.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-29-491x300.png 491w" sizes="(max-width: 1256px) 100vw, 1256px" /> 

공 들여 만든 식당 관리 페이지다.

식당 카드에 마우스를 올리면 자세한 정보가 보인다.

<img class="alignnone size-full wp-image-739" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51.png" alt="스크린샷 2018-05-20 오후 10.14.51" width="1254" height="770" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51.png 1254w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51-300x184.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51-768x472.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51-1024x629.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51-1000x614.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-14-51-489x300.png 489w" sizes="(max-width: 1254px) 100vw, 1254px" /> 

수정하기 버튼을 누르면 나오는 식당 정보 수정 다이얼로그다.

기존 정보와 수정된 정보를 비교해서 필요한 정보만 업데이트한다.<img class="alignnone size-full wp-image-741" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51.png" alt="스크린샷 2018-05-20 오후 10.15.51" width="1254" height="769" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51.png 1254w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51-300x184.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51-768x471.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51-1024x628.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51-1000x613.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-15-51-489x300.png 489w" sizes="(max-width: 1254px) 100vw, 1254px" />

카드뷰로만 식당 정보를 관리하는데에 한계를 느껴 만든 테이블이다.

검색 필터링 기능을 유용하게 사용하고 있다.<img class="alignnone size-full wp-image-742" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11.png" alt="스크린샷 2018-05-20 오후 10.16.11" width="1258" height="772" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11.png 1258w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11-300x184.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11-768x471.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11-1024x628.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11-1000x614.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-11-489x300.png 489w" sizes="(max-width: 1258px) 100vw, 1258px" />

정보 셀을 누르면 나오는 수정 창이다.

맨 왼쪽의 사진 아이콘을 누르면 사진을 추가하는 창이 내려온다.<img class="alignnone size-full wp-image-743" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51.png" alt="스크린샷 2018-05-20 오후 10.16.51" width="1260" height="771" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51.png 1260w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51-300x184.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51-768x470.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51-1024x627.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51-1000x612.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-16-51-490x300.png 490w" sizes="(max-width: 1260px) 100vw, 1260px" />

**클라이언트 https://lento.in**

클라이언트의 메인 페이지다.

음식종류별로 보기 기능을 넣었다.

서버에 부담 가지 않도록 종류별로 가져온 음식을 Vuex에 캐싱한다.

덕분에 네비게이션 시 리랜더링이 되지 않아 스크롤 위치가 보존된다.

밤에 앱 접속 시 눈 부시지 않도록 다크 모드도 넣었다.

시간에 맞추어 모드가 자동으로 설정된다.

<div id='gallery-11' class='gallery galleryid-835 gallery-columns-3 gallery-size-thumbnail'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/05/20/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%a3%bc%eb%b3%80-%ec%8b%9d%eb%8b%b9-%ec%b6%94%ec%b2%9c%ec%95%b1-lento/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-05-20-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-10-18-51/'><img width="150" height="150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-51-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-51-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-51-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/05/20/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%a3%bc%eb%b3%80-%ec%8b%9d%eb%8b%b9-%ec%b6%94%ec%b2%9c%ec%95%b1-lento/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-05-20-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-10-18-57/'><img width="150" height="150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-57-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-57-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-57-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure>
</div>

식당 상세 페이지다.

직접 만든 사진 캐러셀, 사진 등록 다이얼로그, 메뉴 더보기, 식당 위치 구글 지도가 눈에 띈다.

<img class="alignnone size-full wp-image-744" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-14.png" alt="스크린샷 2018-05-20 오후 10.18.14" width="1287" height="1589" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-14.png 1287w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-14-243x300.png 243w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-14-768x948.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-14-829x1024.png 829w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-14-1000x1235.png 1000w" sizes="(max-width: 1287px) 100vw, 1287px" /> 

학식을 볼 수 있는 페이지<img class="alignnone size-full wp-image-745" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-30.png" alt="스크린샷 2018-05-20 오후 10.18.30" width="762" height="824" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-30.png 762w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-18-30-277x300.png 277w" sizes="(max-width: 762px) 100vw, 762px" />

**서버**

Koa.js와 타입스크립트를 사용했다.

DB 스키마와 함수들에 타입을 다 정해주었다.<img class="alignnone size-full wp-image-749" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-21-43.png" alt="스크린샷 2018-05-20 오후 10.21.43" width="943" height="998" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-21-43.png 943w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-21-43-283x300.png 283w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-21-43-768x813.png 768w" sizes="(max-width: 943px) 100vw, 943px" />

API 문서 없이도(만들어 놓긴 했다) 기능을 파악할 수 있도록 신경 써서 코드를 작성했다.<img class="alignnone size-full wp-image-748" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46.png" alt="스크린샷 2018-05-20 오후 10.20.46" width="909" height="904" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46.png 909w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46-300x298.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46-768x764.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46-85x85.png 85w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-20-e1848be185a9e18492e185ae-10-20-46-302x300.png 302w" sizes="(max-width: 909px) 100vw, 909px" />

&nbsp;