---
id: 838
title: 포르투갈어 동사변형 앱
date: 2019-04-21T15:11:09+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/719-revision-v1/
permalink: /2019/04/21/719-revision-v1/
---
<div id='gallery-12' class='gallery galleryid-838 gallery-columns-3 gallery-size-thumbnail'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon landscape'>
    <a href='https://yongj.in/2018/05/04/%ed%8f%ac%eb%a5%b4%ed%88%ac%ea%b0%88%ec%96%b4-%eb%8f%99%ec%82%ac%eb%b3%80%ed%98%95-%ec%95%b1/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-05-04-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-5-33-03/'><img width="150" height="150" src="https://yongj.in/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-04-e1848be185a9e18492e185ae-5-33-03-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://yongj.in/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-04-e1848be185a9e18492e185ae-5-33-03-150x150.png 150w, https://yongj.in/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-04-e1848be185a9e18492e185ae-5-33-03-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/05/04/%ed%8f%ac%eb%a5%b4%ed%88%ac%ea%b0%88%ec%96%b4-%eb%8f%99%ec%82%ac%eb%b3%80%ed%98%95-%ec%95%b1/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-05-04-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-5-33-32/'><img width="150" height="150" src="https://yongj.in/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-04-e1848be185a9e18492e185ae-5-33-32-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://yongj.in/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-04-e1848be185a9e18492e185ae-5-33-32-150x150.png 150w, https://yongj.in/wp-content/uploads/2018/05/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-05-04-e1848be185a9e18492e185ae-5-33-32-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure>
</div>

&nbsp;

1시험 1앱 프로젝트의 일환로 만들었다.

<p style="text-align:center;">
  <strong>서버</strong>
</p>

  * 서버는 함수를 조합해서 만들었다.
  * getConj 함수는 매개변수 없이 Pointfree 스타일로 작성했다.
  * takeFive 함수는 지연평가를 통해 불필요한 배열 순회를 줄였다.

https://gist.github.com/16Yongjin/38acbf4442f4e8eec19c865878269a32

<p style="text-align:center;">
  <strong>클라이언트</strong>
</p>

  * 자동 완성 검색창과 지우기 버튼으로  사용이 편리한 UI를 만들었다.
  * v-select의 input 요소에 접근하기 위해 $refs 접근을 두번해야 했다.

&nbsp;

&nbsp;