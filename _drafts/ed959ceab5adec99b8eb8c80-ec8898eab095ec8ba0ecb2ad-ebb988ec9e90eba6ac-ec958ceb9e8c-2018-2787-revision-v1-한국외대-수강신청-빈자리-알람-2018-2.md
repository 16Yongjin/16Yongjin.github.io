---
id: 829
title: 한국외대 수강신청 빈자리 알람 (2018-2)
date: 2019-04-21T15:07:59+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/787-revision-v1/
permalink: /2019/04/21/787-revision-v1/
---
<img class="  wp-image-790 aligncenter" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/group.png" alt="Group.png" width="304" height="304" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/group.png 479w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/group-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/group-300x300.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/group-85x85.png 85w" sizes="(max-width: 304px) 100vw, 304px" />

<p style="text-align:center;">
  직접 만든 로고
</p>

<div id='gallery-9' class='gallery galleryid-829 gallery-columns-3 gallery-size-thumbnail'>
  <figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/08/12/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%88%98%ea%b0%95%ec%8b%a0%ec%b2%ad-%eb%b9%88%ec%9e%90%eb%a6%ac-%ec%95%8c%eb%9e%8c-2018-2/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-08-12-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-3-36-50/'><img width="150" height="150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-08-12-e1848be185a9e18492e185ae-3-36-50-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-08-12-e1848be185a9e18492e185ae-3-36-50-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-08-12-e1848be185a9e18492e185ae-3-36-50-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure><figure class='gallery-item'> 
  
  <div class='gallery-icon portrait'>
    <a href='https://yongj.in/2018/08/12/%ed%95%9c%ea%b5%ad%ec%99%b8%eb%8c%80-%ec%88%98%ea%b0%95%ec%8b%a0%ec%b2%ad-%eb%b9%88%ec%9e%90%eb%a6%ac-%ec%95%8c%eb%9e%8c-2018-2/%e1%84%89%e1%85%b3%e1%84%8f%e1%85%b3%e1%84%85%e1%85%b5%e1%86%ab%e1%84%89%e1%85%a3%e1%86%ba-2018-08-12-%e1%84%8b%e1%85%a9%e1%84%92%e1%85%ae-3-37-52/'><img width="150" height="150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-08-12-e1848be185a9e18492e185ae-3-37-52-150x150.png" class="attachment-thumbnail size-thumbnail" alt="" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-08-12-e1848be185a9e18492e185ae-3-37-52-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2018/08/e18489e185b3e1848fe185b3e18485e185b5e186abe18489e185a3e186ba-2018-08-12-e1848be185a9e18492e185ae-3-37-52-85x85.png 85w" sizes="(max-width: 150px) 100vw, 150px" /></a>
  </div></figure>
</div>



&nbsp;

&nbsp;

<p style="text-align:center;">
  <strong>서버</strong>
</p>

  * <a href="https://marpple.github.io/partial.js/" target="_blank" rel="noopener noreferrer">Partial.js</a>를 사용했다.
  * DB는 JS 기본 객체를 사용해서 만들었다.
  * &#8217;10 / 50&#8242; 같은 인원정보에서 자리가 났는지 여부를 알아내기 위해 
      * 문자열끼리 나눗셈하면 숫자가 나오는 점
      * 비트연산 x | 1 을 하면 x가 1보다 작은 경우 falsy한 값인 0이 나오는점을 이용했다.

  * 강의 목록을 가져오는 함수의 결과를 캐싱하기 위해 asyncMemoize 함수를 만들었다.

<div style="background:#f0f3f3;overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;">
  <pre style="margin:0;line-height:125%;"><span style="color:#006699;font-weight:bold;">const</span> asyncMemoize <span style="color:#555555;">=</span> (fn, cache <span style="color:#555555;">=</span> {}) <span style="color:#555555;">=&gt;</span>
  arg <span style="color:#555555;">=&gt;</span> cache[arg] <span style="color:#555555;">?</span> Promise.resolve(cache[arg]) <span style="color:#555555;">:</span> fn(arg).then(res <span style="color:#555555;">=&gt;</span> (cache[arg] <span style="color:#555555;">=</span> res))
</pre>
</div>

&nbsp;

&nbsp;

<p style="text-align:center;">
  <strong>클라이언트</strong>
</p>

  * <a href="https://lusaxweb.github.io/vuesax/" target="_blank" rel="noopener noreferrer">VueSax</a>를 사용했다. 자주 쓰던 Vuetify의 컴포넌트보다 동글동글해서 편안한 느낌이다.
  * 서버 메시지를 오른쪽 하단에 보여줘서 마이크로인터랙션을 만들었다.
  * radio 컴포넌트 내 v-model이 작동을 안해서 @click을 붙여서 억지로 작동하게 만들었다.