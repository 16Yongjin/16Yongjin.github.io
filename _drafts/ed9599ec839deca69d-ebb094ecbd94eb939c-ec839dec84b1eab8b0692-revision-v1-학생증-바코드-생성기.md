---
id: 841
title: 학생증 바코드 생성기
date: 2019-04-21T15:12:12+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/692-revision-v1/
permalink: /2019/04/21/692-revision-v1/
---
<img class="  wp-image-693 aligncenter" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/screenshot-2018-3-16.png" alt="Screenshot (2018. 3. 16" width="304" height="542" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/screenshot-2018-3-16.png 1440w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/screenshot-2018-3-16-168x300.png 168w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/screenshot-2018-3-16-768x1370.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/screenshot-2018-3-16-574x1024.png 574w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/03/screenshot-2018-3-16-1000x1784.png 1000w" sizes="(max-width: 304px) 100vw, 304px" />

https://hufs.surge.sh

학교 모바일 학생증 앱이 불편해서 만들었다.

기존 학생증 앱은

  1. 인터넷 연결이 필요하다.
  2. 아이디, 비밀번호를 입력해야한다.
  3. 로딩시간이 길다. (앱 구동 + 리소스 가져오기)
  4. 어쩌다가 앱이 튕기기도 한다.
  5. qr code를 발급받고 5분 내에 리더기에 찍어야한다.
  6. 보기 싫은 증명사진을 봐야한다.
  7. 화면밝기가 최대가 된다. 안드는 앱을 끄면 밝기가 복구되지만 아이폰은 그렇지 않다.

이 앱은

  1. 학번만 입력하면 된다. 
      * 학번을 제대로 입력했을 때 바코드가 나오고
      * 적게 입력했을 때는 바코드가 안나오고
      * 많이 입력했을 때는 사용 흐름을 막지 않기 위해 경고창만 나오게 했다.
      * 키보드를 닫을려면 커다란 [이동] 버튼을 누르면 된다.
      * 최소의 인터페이스를 최대로 이용했다.
  2. 인터넷 연결이 필요없다. 
      * PWA html, js 캐싱
      * localStorage로 학번 저장
      * 초기 앱 데이터(500kb 정도) 빼고 데이터 낭비가 없다.

https://gist.github.com/ac2e7c1b343490c6c80418e3d4b781e9

코드는 이게 전부다.