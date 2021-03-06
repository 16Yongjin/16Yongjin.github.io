---
id: 837
title: 포르투갈어 사전 자체 동사 스테밍 기능 추가
date: 2019-04-21T15:11:03+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/724-revision-v1/
permalink: /2019/04/21/724-revision-v1/
---
{ 변형: [원형] }으로 구성된 객체를 만들기 위해 작성한 스크립트

https://gist.github.com/16Yongjin/1a90ef0be57a465f1d350bbd2d934b6c

한 가지 일만 하는 함수를 작성하다 보니 재활용할 수 있는 함수가 조금씩 생긴다.

나중에 코드를 많이 작성하다 보면 자연스럽게 라이브러리가 생길 것 같다.

<h3 style="text-align:center;">
  <strong>성능 비교</strong>
</h3>

어근을 찾고 뜻까지 가져오는 테스트이다.

<img class="alignnone size-full wp-image-727" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e1848ce185a5e186ab-12-38-01.png" alt="스크린샷 2018-05-05 오전 12.38.01" width="728" height="214" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e1848ce185a5e186ab-12-38-01.png 728w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e1848ce185a5e186ab-12-38-01-300x88.png 300w" sizes="(max-width: 728px) 100vw, 728px" /> 

**기존 코드** &#8211; cooljugator.com/pt 의 api에서 데이터를 가져오기에 매우 느리다.

<img class="alignnone size-full wp-image-728" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e1848ce185a5e186ab-12-43-55.png" alt="스크린샷 2018-05-05 오전 12.43.55" width="714" height="200" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e1848ce185a5e186ab-12-43-55.png 714w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-05-e1848be185a9e1848ce185a5e186ab-12-43-55-300x84.png 300w" sizes="(max-width: 714px) 100vw, 714px" /> 

**자체 스테머 적용 후** &#8211; 10배 빠르다.

<h3 style="text-align:center;">
  <strong>마무리</strong>
</h3>

  * 성능이 어느 정도 나오기 때문에 포어 사전 크롬 익스텐션으로 만들어도 좋겠다.
  * 콜백 &#8211; 프로미스 &#8211; async/await &#8211; 쿼리 캐싱 &#8211; 스테머 추가 등으로 리팩터링을 진행 중이다.
  * 다음엔 partial.js를 사용해서 async / await 가 없는 코드로 리팩터링을 해야겠다.