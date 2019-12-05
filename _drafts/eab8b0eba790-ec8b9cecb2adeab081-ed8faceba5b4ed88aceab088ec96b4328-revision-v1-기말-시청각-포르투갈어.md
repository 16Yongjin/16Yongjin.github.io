---
id: 857
title: 기말 시청각 포르투갈어
date: 2019-04-21T15:15:44+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/328-revision-v1/
permalink: /2019/04/21/328-revision-v1/
---
PC를 사용해야만 교재의 성우 녹음 파일을 들을 수 있어서

핸드폰으로도 대본보며 녹음파일을 들을 수 있게 어플 제작함.

&nbsp;

과정

1.  exe 파일 swf 파일로 전환 (SWF2EXE 사용)

2. swf 파일에서 스크립트, 번역본, mp3 녹음 파일 추출(SWF Decompiler 사용)

3. 대사 별로 한 줄씩 나눠져있던 파일 합치기 (DOS의 type *.txt > script.txt 명령어 사용)

4. 인코딩으로 인해 날아간 강세표시 고침(MS 워드용 포어 교정기가 안깔려서 맥의 pages 사용)

5. 각 줄마다 녹음 파일을 연결시켜야 돼서 다시 분할하고 이름 붙이기(Text Cleaver.exe, DarkNamer.exe) 사용

6. Android Studio, 뷰페이저, MediaPlayer, 텍스트뷰 동적 할당 등을 사용(98% 구글링)

7. 구글에서 무료 이미지, 아이콘 다운받아서 플레이스토어에 등록함

8. 홍보는 페이스북(5명)과 후배들이랑 친한 동기에게 부탁(12명 이상 효과)

9. ios버전은 없냐고 문의가 있어서 스탠포드 ios강좌 수강 중인데 재밌다.

10. 한편, 앱스토어 등록에 10만원 낼바엔 웹버전으로 만드는 게 나을지도 모르겠다.

&nbsp;

<img class="alignnone size-full wp-image-329" src="https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c.png" alt="기말시청각대시보드.png" width="1433" height="1285" srcset="https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c.png 1433w, https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c-300x269.png 300w, https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c-768x689.png 768w, https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c-1024x918.png 1024w, https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c-1000x897.png 1000w, https://yongj.in/wp-content/uploads/2017/06/eab8b0eba790ec8b9cecb2adeab081eb8c80ec8b9cebb3b4eb939c-335x300.png 335w" sizes="(max-width: 1433px) 100vw, 1433px" />