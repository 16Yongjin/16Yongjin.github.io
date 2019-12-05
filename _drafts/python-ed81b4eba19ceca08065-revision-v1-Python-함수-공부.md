---
id: 865
title: Python 함수 공부
date: 2019-04-21T15:17:32+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/65-revision-v1/
permalink: /2019/04/21/65-revision-v1/
---
<img class="alignnone size-full wp-image-66" src="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194.png" alt="스크린샷 2017-04-08 오후 9.48.34" width="1144" height="578" srcset="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194.png 1144w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194-300x152.png 300w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194-768x388.png 768w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194-1024x517.png 1024w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194-1000x505.png 1000w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-48-34-e1491655817194-594x300.png 594w" sizes="(max-width: 1144px) 100vw, 1144px" />

파이썬으로 배우는 실전 알고리즘 p.47 예제

클로저, 내부함수.

함수의 반환 값으로 함수가 나와서 이를 이용할 수 있다.

<img class="alignnone size-full wp-image-78" src="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-58-39.png" alt="스크린샷 2017-04-08 오후 9.58.39.png" width="418" height="396" srcset="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-58-39.png 418w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-58-39-300x284.png 300w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-9-58-39-317x300.png 317w" sizes="(max-width: 418px) 100vw, 418px" /> 

값 여러개를 튜플로 반환 할 수도 있다.

if 리턴값 개수 == 할당 받을 변수 개수 : 각 변수마다 리턴값 할당됨

else if 변수 개수 == 1: 변수에 튜플로 묶인 값이 할당됨

else: 에러 # 리턴 개수 ≠ 변수 개수

<img class=" size-full wp-image-80 alignleft" src="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-16-41.png" alt="스크린샷 2017-04-08 오후 10.16.41" width="770" height="340" srcset="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-16-41.png 770w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-16-41-300x132.png 300w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-16-41-768x339.png 768w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-16-41-679x300.png 679w" sizes="(max-width: 770px) 100vw, 770px" /> 

가변 인수도 받을 수 있다.

\* 이면 그냥 인수, \**이면 이름 있는 인수로 인식된다.

그리고 특성상 매개 변수 가장 뒤에 써야 한다. 특히 **는 가장 뒤에

x = 1, 2가 x=1 하고 2가 아니라 x=(1,2) 니까

<img class=" size-full wp-image-81 alignleft" src="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-17-06.png" alt="스크린샷 2017-04-08 오후 10.17.06.png" width="954" height="288" srcset="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-17-06.png 954w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-17-06-300x91.png 300w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-17-06-768x232.png 768w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-10-17-06-800x242.png 800w" sizes="(max-width: 954px) 100vw, 954px" /> 

튜플이나 리스트 값 앞에 *을 붙여서 Unpack할 수도 있다.

***(1, 2)와** ****{&#8216;a&#8217; = 1, &#8216;b&#8217; = 2}**가 매개변수 1과 2로 인식한다.

*안붙이고 튜플 넘기면 인수 더 달라고 에러 뜸

<p style="color:white;background-color:black;">
  >>> a = [1,2,3,4,5,6]<br /> >>> list(map(lambda x: x+2, a))<br /> [3, 4, 5, 6, 7, 8]
</p>

람다를 이용해 map 함수를 적용할 수도 있다.  
파이썬 버전 2대는 list()를 안써도 되는 것 같은데  
3대는 map함수 적용한 값을 그대로 건내주는지 list()를 안씌우면 포인터값(?)이 반환된다.

그와중에 캡쳐하기 귀찮아서 html 문법 공부함 style=&#8221;특성:값;&#8221;