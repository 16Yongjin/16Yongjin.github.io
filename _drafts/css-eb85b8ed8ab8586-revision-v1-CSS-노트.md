---
id: 823
title: CSS 노트
date: 2019-04-21T15:03:41+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/586-revision-v1/
permalink: /2019/04/21/586-revision-v1/
---
<span style="color:#6090ac;"><span style="font-size:medium;">box-sizing</span></span><span style="color:#858585;"><span style="font-size:medium;">: </span></span><span style="color:#be7c63;"><span style="font-size:medium;">border-box</span></span><span style="color:#858585;"><span style="font-size:medium;">;</span></span>  
<span style="color:#858585;"><span style="font-size:medium;">margin, padding</span></span><span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">이</span></span></span><span style="color:#858585;"><span style="font-size:medium;"> </span></span></span><span style="color:#858585;"><span style="font-size:medium;">width, height </span></span><span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">박스에 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">다 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">포함되어 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">부모</span></span></span></span><span style="color:#858585;"><span style="font-size:medium;">.</span></span><span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">자식이 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">들어맞게 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">된다</span></span></span></span><span style="color:#858585;"><span style="font-size:medium;">.</span></span><span style="color:#858585;"> </span>

<div dir="LTR" lang="en-US" style="border:none;padding:0;">
  <p style="margin-bottom:0;line-height:.24in;">
    <span style="color:#6090ac;"><span style="font-size:medium;">position</span></span><span style="color:#858585;"><span style="font-size:medium;">: </span></span><span style="color:#be7c63;"><span style="font-size:medium;">relative</span></span><span style="color:#858585;"><span style="font-size:medium;">;</span></span>
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span style="color:#858585;"><span style="font-size:medium;">absolute </span></span><span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">포지션을 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">가진 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">자식 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">요소가 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">위치를 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">참조할 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">수 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">있게한다</span></span></span></span><span style="color:#858585;"><span style="font-size:medium;">. </span></span>
  </p>
  
  <p>
    &nbsp;
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span style="color:#6090ac;"><span style="font-size:medium;">clip-path</span></span><span style="color:#858585;"><span style="font-size:medium;">: </span></span><span style="color:#868762;"><span style="font-size:medium;">polygon</span></span><span style="color:#858585;"><span style="font-size:medium;">(</span></span><span style="color:#778c6c;"><span style="font-size:medium;">0 0</span></span><span style="color:#858585;"><span style="font-size:medium;">, </span></span><span style="color:#778c6c;"><span style="font-size:medium;">100% 0</span></span><span style="color:#858585;"><span style="font-size:medium;">, </span></span><span style="color:#778c6c;"><span style="font-size:medium;">100% 75vh</span></span><span style="color:#858585;"><span style="font-size:medium;">, </span></span><span style="color:#778c6c;"><span style="font-size:medium;">0 100%</span></span><span style="color:#858585;"><span style="font-size:medium;">);</span></span>
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">이건 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">어려우니까 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">이걸 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">여러모양으로 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">만들어주는 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">사이트를 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">참조할 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">것</span></span></span></span>
  </p>
  
  <p>
    &nbsp;
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span style="color:#6090ac;"><span style="font-size:medium;">animation</span></span><span style="color:#858585;"><span style="font-size:medium;">: moveInBottom </span></span><span style="color:#778c6c;"><span style="font-size:medium;">.5s </span></span><span style="color:#be7c63;"><span style="font-size:medium;">ease-out </span></span><span style="color:#778c6c;"><span style="font-size:medium;">.75s</span></span><span style="color:#858585;"><span style="font-size:medium;">;</span></span>
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">순서</span></span></span></span><span style="color:#858585;"><span style="font-size:medium;">: name duration timing-function delay</span></span>
  </p>
  
  <p>
    &nbsp;
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span style="color:#6090ac;"><span style="font-size:medium;">animation-fill-mode</span></span><span style="color:#858585;"><span style="font-size:medium;">: </span></span><span style="color:#be7c63;"><span style="font-size:medium;">backwards</span></span><span style="color:#858585;"><span style="font-size:medium;">; </span></span>
  </p>
  
  <p style="margin-bottom:0;line-height:.24in;">
    <span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">애니메이션 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">실행 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">전에 </span></span></span></span><span style="color:#858585;"><span style="font-size:medium;">animation-name</span></span><span lang="zh-CN"><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">의 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">초기값이 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">적용되도록 </span></span></span><span style="color:#858585;"><span style="font-family:AppleSDGothicNeo-Regular;"><span style="font-size:medium;">함</span></span></span></span>
  </p>
</div>

&nbsp;

<div style="direction:ltr;border-width:100%;">
  <div style="direction:ltr;margin-top:0;margin-left:0;width:5.1763in;">
    <div style="direction:ltr;margin-top:0;margin-left:0;width:5.1763in;">
      <p style="margin:0;font-family:'Malgun Gothic';font-size:11pt;">
        <span lang="en-US">CSS Cascade, </span><span lang="ko-KR">적용</span> <span lang="ko-KR">순서</span>
      </p>
      
      <ol style="margin-left:.375in;direction:ltr;unicode-bidi:embed;margin-top:0;margin-bottom:0;font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;" type="1">
        <li style="margin-top:0;margin-bottom:0;vertical-align:middle;" value="1">
          <span style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">!important</span> <ol style="margin-left:.375in;direction:ltr;unicode-bidi:embed;margin-top:0;margin-bottom:0;font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;" type="a">
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;" value="1">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">User</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">의 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">!important</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">선언</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">Author</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">!important</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">선언</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">Author</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의 선언</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">User</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의 선언</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span style="font-family:'Malgun Gothic';font-size:11pt;">브라우저의 기본 선언</span>
            </li>
          </ol>
        </li>
        
        <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
          <span style="font-family:'Malgun Gothic';font-size:11pt;">Specificity</span> <ol style="margin-left:.375in;direction:ltr;unicode-bidi:embed;margin-top:0;margin-bottom:0;font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;" type="a">
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;" value="1">
              <span style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">인라인 스타일</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span style="font-family:'Malgun Gothic';font-size:11pt;">아이디</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">클래스</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">, </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의사 클래스</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">, </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">속성</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">요소</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">, </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의사 요소</span>
            </li>
          </ol>
        </li>
        
        <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
          <span style="font-family:'Malgun Gothic';font-size:11pt;">코드의 순서</span>
        </li>
      </ol>
      
      <p style="margin:0;margin-left:.375in;font-family:'Malgun Gothic';font-size:11pt;">
        <span lang="ko-KR">가장 마지막 선언이 다른 선언 다 덮어쓴다</span><span lang="en-US">.</span>
      </p>
      
      <p lang="en-US" style="margin:0;margin-left:.375in;font-family:'Malgun Gothic';font-size:11pt;">
        <p style="margin:0;font-family:'Malgun Gothic';font-size:11pt;">
          <span lang="en-US">Value </span><span lang="ko-KR">값이 정해지는 과정</span>
        </p>
        
        <ol style="margin-left:.375in;direction:ltr;unicode-bidi:embed;margin-top:0;margin-bottom:0;font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;" type="1">
          <li style="margin-top:0;margin-bottom:0;vertical-align:middle;" value="1">
            <span style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">값 선언</span>
          </li>
          <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
            <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">Cascade </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">이후</span>
          </li>
          <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
            <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">Cascade</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">가 없는 경우 기본</span> <span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">초기 값들</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;"> (</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">마진</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">, </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">패딩은 기본 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">0)</span>
          </li>
          <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
            <span style="font-family:'Malgun Gothic';font-size:11pt;">상대값을 절대값으로 변환</span>
          </li>
          <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
            <span style="font-family:'Malgun Gothic';font-size:11pt;">레이아웃을 보고 값을 계산함</span>
          </li>
          <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
            <span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">브라우저와 장치의 제한</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">(</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">소수점을 없애는 반올림 등</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">)</span>
          </li>
        </ol>
        
        <p lang="en-US" style="margin:0;margin-left:.375in;font-family:'Malgun Gothic';font-size:11pt;">
          <p style="margin:0;font-family:'Malgun Gothic';font-size:11pt;">
            <span lang="ko-KR">상대값이 절대값으로 변환되는</span> <span lang="ko-KR">방법</span>
          </p>
          
          <ol style="margin-left:.375in;direction:ltr;unicode-bidi:embed;margin-top:0;margin-bottom:0;font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;" type="1">
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;" value="1">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">% fonts &#8211; </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">부모의 계산완료된 폰트크기 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;font-weight:normal;font-style:normal;">* x%</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">% lengths &#8211; </span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">부모의 계산완료된 </span><span lang="ko-KR" style="font-weight:bold;font-family:'Malgun Gothic';font-size:11pt;">넓이</span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;"> * x%</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">em fonts &#8211; </span><span lang="ko-KR" style="font-weight:bold;font-family:'Malgun Gothic';font-size:11pt;">부모</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의 계산완료된 폰트크기 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">* x</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">em lengths &#8211; </span><span lang="ko-KR" style="font-weight:bold;font-family:'Malgun Gothic';font-size:11pt;">현재</span> <span lang="ko-KR" style="font-weight:bold;font-family:'Malgun Gothic';font-size:11pt;">요소</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의 계산완료된 폰트크기 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">* x</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">rem &#8211; </span><span lang="ko-KR" style="font-weight:bold;font-family:'Malgun Gothic';font-size:11pt;">루트</span><span lang="ko-KR" style="font-family:'Malgun Gothic';font-size:11pt;">의 폰트크기 </span><span lang="en-US" style="font-family:'Malgun Gothic';font-size:11pt;">* x</span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span style="font-family:'Malgun Gothic';font-size:11pt;">vh </span>
            </li>
            <li style="margin-top:0;margin-bottom:0;vertical-align:middle;">
              <span style="font-family:'Malgun Gothic';font-size:11pt;">vw</span>
            </li>
          </ol>
          
          <p lang="en-US" style="margin:0;font-family:'Malgun Gothic';font-size:11pt;">
            <p style="margin:0;font-family:'Malgun Gothic';font-size:11pt;">
              <span lang="ko-KR">이런 거 쓰는 이유 </span><span lang="en-US">:</span>
            </p>
            
            <p style="margin:0;margin-left:.375in;font-family:'Malgun Gothic';font-size:11pt;">
              폰트 크기만 바꿔도 레이아웃 크기를 자동으로 조정할 수 있어
            </p>
            
            <p style="margin:0;margin-left:.375in;font-family:'Malgun Gothic';font-size:11pt;">
              <span lang="ko-KR">더 </span><span lang="en-US">Responsive</span><span lang="ko-KR">한 레이아웃을 만들 수 있음</span><span lang="en-US">.</span>
            </p></div> </div> </div>