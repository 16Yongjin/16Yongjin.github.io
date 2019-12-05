---
id: 845
title: '[Codewars] Moves in squared strings (II)'
date: 2019-04-21T15:13:15+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/675-revision-v1/
permalink: /2019/04/21/675-revision-v1/
---
n 라인의 문자열을 180도, 360도 회전시키는 문제

예시:

[code language=&#8221;javascript&#8221;]

|rotation |selfie\_and\_rot  
|abcd &#8211;> ponm |abcd &#8211;> abcd&#8230;.  
|efgh lkji |efgh efgh&#8230;.  
|ijkl hgfe |ijkl ijkl&#8230;.  
|mnop dcba |mnop mnop&#8230;.  
&#8230;.ponm  
&#8230;.lkji  
&#8230;.hgfe  
&#8230;.dcba"  
[/code]

<div>
   답안 1등
</div>

[code language=&#8221;javascript&#8221;]

function rot(s) {  
return s.split("").reverse().join("");  
}

function selfieAndRot(s) {  
return (s = s.replace(/.+/g, t => t + t.replace(/./g, "."))) + "\n" + rot(s);  
}

[/code]

<div>
  replace 메서드에 함수 적용
</div>

<div>
   /.+/ 는 \n 등을 제외함
</div>

<div>
  매개변수를 변수로 재사용함
</div>

<div>
  대입문을 표현식으로 사용함
</div>