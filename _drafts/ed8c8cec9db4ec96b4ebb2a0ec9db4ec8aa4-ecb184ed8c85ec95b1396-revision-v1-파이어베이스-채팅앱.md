---
id: 855
title: 파이어베이스 채팅앱
date: 2019-04-21T15:15:25+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/396-revision-v1/
permalink: /2019/04/21/396-revision-v1/
---
<img class="alignnone size-full wp-image-389" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr.jpg" alt="20170601_193618_HDR" width="4160" height="2340" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr.jpg 4160w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr-300x169.jpg 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr-768x432.jpg 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr-1024x576.jpg 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr-1000x563.jpg 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/20170601_193618_hdr-533x300.jpg 533w" sizes="(max-width: 4160px) 100vw, 4160px" />

<img class="alignnone  wp-image-412" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/ec8aa4ed81aceba6b0ec83b7-2017-08-22-ec98a4eca084-2-30-14.png" alt="스크린샷 2017-08-22 오전 2.30.14.png" width="393" height="557" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/ec8aa4ed81aceba6b0ec83b7-2017-08-22-ec98a4eca084-2-30-14.png 1004w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/ec8aa4ed81aceba6b0ec83b7-2017-08-22-ec98a4eca084-2-30-14-212x300.png 212w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/ec8aa4ed81aceba6b0ec83b7-2017-08-22-ec98a4eca084-2-30-14-768x1088.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/ec8aa4ed81aceba6b0ec83b7-2017-08-22-ec98a4eca084-2-30-14-723x1024.png 723w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/08/ec8aa4ed81aceba6b0ec83b7-2017-08-22-ec98a4eca084-2-30-14-1000x1416.png 1000w" sizes="(max-width: 393px) 100vw, 393px" /> 

2017년 6월 1일 IT동아리 학술제 때 발표자와 청중 간 소통을 위한 채팅앱을 만들었다.

데이버베이스 서버 이외에 다른 서버 없이 클라이언트 간의 메시지 교환만으로 만든 앱이다.

자바스크립트로 HTML에 텍스트 삽입도 할 줄 몰랐지만 마감일이 있다는 게 뭔지 400줄이 넘는 코드를 2주 동안 수업도 안들으면서 계속 작성했다.

닉네임 변경, 비트코인 보내기, img src보내기, 파일 업로드해서 보내기 등등 기능을 넣었다.

특히 /파일 기능은 가장 신경써서 만들었다.

파이어베이스 스토리지에 파일을 보낸 후 다운로드 url을 콜백으로 받아 채팅창에 띄우는 거였는데 아무도 사용하지 않았지만 만들면서 가장 재밌었고 그 당시 나에게 가장 높은 수준의 공학이었다.

또 비트코인 충전 시, 충전용 메시지와 충전 알림용 메시지 보내고 하나는 지워서 새로 들어오는 사람의 비트코인 충전을 막았다.

&nbsp;

주소: https://chataddict-8b4bc.firebaseapp.com

깃허브: https://github.com/16Yongjin/chatAdd-ICT

&nbsp;