---
title: Macintosh Classic II 개조 프로젝트
date: 2021-12-22T21:00:00+09:00
author: yongjin0802
categories:
  - Hardware
---

매킨토시 클래식II를 미니 PC로 개조하기

## 개요

- [개요](#개요)
- [프로젝트 시작 이유](#프로젝트-시작-이유)
- [중고 매킨토시 구매](#중고-매킨토시-구매)
- [매킨토시 분해하기](#매킨토시-분해하기)
- [CRT 모니터 방전시키기](#crt-모니터-방전시키기)
- [분해 완료](#분해-완료)
- [황변 제거하기](#황변-제거하기)
- [LCD 설치](#lcd-설치)
- [LCD 테스트](#lcd-테스트)
- [전원부 설치](#전원부-설치)
- [내부 부품 설치](#내부-부품-설치)
- [화면 설정](#화면-설정)
- [완성](#완성)

## 프로젝트 시작 이유

![macintosh 128k](https://user-images.githubusercontent.com/22253556/147051641-3908bc91-fa3e-43a8-8715-e8e9db7d3b77.png)

평소에 PC와 GUI의 시대를 연 매킨토시에 대한 로망이 있었다. 김종민님의 [Macintosh Classic iPad Air Stand](https://blog.cmiscm.com/?p=5765)와 닥터케이님의 [30년 전 올드맥에 새 생명을](https://m.blog.naver.com/drangra/221979390145) 글은 매킨토시에 아이패드나 맥미니를 결합해서 개조하는 것을 보여주는데, 감성이 장난 아니다. 이걸 보고 심미성과 기능성을 모두 만족하는 매킨토시를 만들어보자는 생각을 했다.

## 중고 매킨토시 구매

이베이에서 중고 매킨토시를 구매했다. 황변은 쉽게 제거되므로 사진을 꼼꼼히 보고 부서진 곳이나 스크래치가 없는 물품을 골랐다.

> 처음에 좀 싸게 사려고 경매를 시도를 했는데, 자동으로 비딩을 하는 봇한테 처참하게 발렸다.

![image](https://user-images.githubusercontent.com/22253556/147050389-40cb3645-a244-4fef-be9d-183b7e18b5a9.png)

도착한 맥이다. 다행히 배송 중에 부서진 곳은 없었다. 엄청 무겁고 생각보다 앞뒤로 길다.
![IMG_20210925_215507](https://user-images.githubusercontent.com/22253556/147055712-e958d104-e928-4d5a-bb23-acf74b5f0189.jpg)

같이 따라온 키보드는 애플로고와 키캡에 인쇄된 이탈릭체 덕분에 이쁘다. 신기한 점은 캡스락 키가 볼펜처럼 누르면 딸깍거리면서 들어가고, 다시 누르면 튀어나온다. 아쉬운 점은 연결부가 PS2 규격이지만, 내부적으로 애플 전용 인터페이스를 써서 윈도우에서 사용이 안 된다. (인식 불가 ㅜㅠ)

![IMG_20210923_171804](https://user-images.githubusercontent.com/22253556/147055704-4dfbf12e-6760-45bc-9360-a195a33c46c8.jpg)

중간고사 준비로 바빠서 바로 개조는 못하고 당분간 책꽂이로 썼다.

![IMG_20211005_025317](https://user-images.githubusercontent.com/22253556/147055710-50725fea-1efc-44fe-b2d1-31fdef5b826c.jpg)

## 매킨토시 분해하기

분해 전에 부품 사진을 찍었다.

- 멀티탭
- 아이패드 1 액정 + HDMI 연결을 위한 [AD 보드](https://ko.aliexpress.com/item/4000078058633.html)
- 안 쓰는 노트북 메인보드 (→ 이건 고장나서 미니PC로 변경한다.)

![IMG_20211017_173452](https://user-images.githubusercontent.com/22253556/147058811-990e3bb5-e038-4cff-a751-877e960e83d0.jpg)

15T 별 드라이버를 이용해서 뒷면 나사 4개를 빼면되는데, 위쪽 나사 구멍이 드라이버 길이보다 깊다.

![IMG_20211017_174042](https://user-images.githubusercontent.com/22253556/147058803-e7e8e539-6282-4b3a-86f3-f8df8e37394e.jpg)

롱 드라이버 즉시 구입
![IMG_20211020_181120](https://user-images.githubusercontent.com/22253556/147058801-e0670321-e5b0-4170-b98c-7d684fc939e9.jpg)
딱 대
![IMG_20211020_181238](https://user-images.githubusercontent.com/22253556/147058796-f3b48696-22b4-46e7-b994-9e5a90eda055.jpg)

케이스 분리 성공
![IMG_20211020_181845](https://user-images.githubusercontent.com/22253556/147058789-e0086db3-d1b0-4eea-879f-29ef76eb987c.jpg)

## CRT 모니터 방전시키기

CRT 모니터에 고전압이 흐르고 있어서, 분해 전에 내부 방전을 시켜야 한다. 안 하고 양손으로 만지다 감전되면 심장에 전기가 통해서 사망할 수도 있다고 한다. [Discharging the CRT in a compact Macintosh](https://youtu.be/x1DeMOl_nK4) 유튜브 영상을 참고했다. 전선을 모니터 접지부와 일자 드라이버에 연결하고, 모니터 옆 빨간선이 달려있는 애노드캡을 제거한다. 전류가 남아있으면 드라이버가 닿자마자 스파크가 튄다는데, 자연적으로 방전되서 아무 반응이 없었다.

![IMG_20211020_183123](https://user-images.githubusercontent.com/22253556/147058777-2e3e1fc7-5eaf-4a75-842c-fce3ca62d2b9.jpg)

## 분해 완료

열심히 분해해준다.
![IMG_20211020_184134](https://user-images.githubusercontent.com/22253556/147058771-ded33a5a-c857-486b-bd0c-6319d19aaf39.jpg)

30년된 하드
![IMG_20211020_184418](https://user-images.githubusercontent.com/22253556/147058765-e6caf6ac-e066-43d1-b59f-22a1ca629830.jpg)

메인보드. 칩들이 큼직큼직하다

![IMG_20211020_185324](https://user-images.githubusercontent.com/22253556/147058733-d547ec26-1116-4c16-95fe-dc625f8c5337.jpg)

분해된 부품. 분해에 2시간 정도 걸렸다.

![IMG_20211020_185255 (1)](https://user-images.githubusercontent.com/22253556/147058742-8495d21a-c0c7-4638-bcc8-73bef5645861.jpg)

## 황변 제거하기

플라스틱에 탈색제를 바르고 자외선에 노출시키면 황변이 제거된다.

준비물

- 탈색제
- 비닐장갑: 탈색제에 닿은 피부가 하얗게 괴사하는 것을 막는다.
- 비닐랩: 탈색제가 마르는 것을 막는다.

![IMG_20211104_175628](https://user-images.githubusercontent.com/22253556/147058722-654caa3e-be12-4470-8641-48bc7695ab15.jpg)

탈색제를 꼼꼼하게 바르고
![IMG_20211104_180825](https://user-images.githubusercontent.com/22253556/147058719-4e20ac13-38e4-4ecc-a1cc-c337c9cc1fa2.jpg)

비닐랩으로 싸면 된다.
![IMG_20211104_181209](https://user-images.githubusercontent.com/22253556/147058715-92f8c496-49bb-4707-acdc-6d20622aa93d.jpg)

래핑 완료

![IMG_20211104_190714](https://user-images.githubusercontent.com/22253556/147058702-1e0317ac-7f70-411d-ac5c-92991d75b2a1.jpg)
가을이라 햇빛에 3일 동안 뒀다.
![IMG_20211105_160901](https://user-images.githubusercontent.com/22253556/147058691-54e5ed28-d772-48c4-bd2a-6ab2b3910088.jpg)

비닐을 벗기고 나면 색이 공장초기화된다. 애플 로고엔 영향이 없다.
![IMG_20211107_164309](https://user-images.githubusercontent.com/22253556/147058688-5597f714-3283-41c6-9b2f-7c26cbf8bf21.jpg)

크
![IMG_20211107_164318](https://user-images.githubusercontent.com/22253556/147058683-e4a203d4-d929-41e5-b92a-8c0d3727e6e6.jpg)

## LCD 설치

LCD가 앞판에 밀착하도록 플라스틱 구조물을 떼어낸다. 플라스틱이 물러서 원예가위로 잘 잘린다.

![IMG_20211104_1751452](https://user-images.githubusercontent.com/22253556/147066902-6a7937db-36cd-4315-8f75-a39b9cc04064.jpg)

아이패드 1에서 떼낸 액정을 부착한다. 위쪽과 아래쪽 나사 기둥 덕분에 딱맞게 고정된다.

![IMG_20211107_191334](https://user-images.githubusercontent.com/22253556/147058675-abe62f1c-e211-4b70-9b03-d2d173d8744f.jpg)

## LCD 테스트

PC에 HDMI로 연결해서 [웹 WinXP](https://winxp.vercel.app/)와 [웹 맥 OS](https://macos.vercel.app/)를 띄워봤다. 레티나 디스플레이가 아니라 픽셀이 보이지만 10년 된 LCD 치고 색은 잘 나온다.

![IMG_20211107_193804](https://user-images.githubusercontent.com/22253556/147058669-7dae2edb-5904-412b-99b9-0c7c007b2ff5.jpg)

![IMG_20211107_194137](https://user-images.githubusercontent.com/22253556/147058656-f9685572-a636-474d-ac5a-cc88c3e63d56.jpg)

## 전원부 설치

기존 부품에서 전원 연결부와 스위치를 뗴어냈다.

![IMG_20211110_194041](https://user-images.githubusercontent.com/22253556/147058647-b0514d24-8d13-4e61-957c-8b3d31d8d82a.jpg)

배선은 [닥터케이님의 영상](https://youtu.be/a5XxrUhoXqE?t=508) 8분대를 참조해서 납땜을 했다.

![IMG_20211110_210930](https://user-images.githubusercontent.com/22253556/147058642-ac46d558-4b3b-4e39-b3fb-e2274d0059d2.jpg)

멀티탭은 이렇게 매킨토시 내부에서 미니 PC, 모니터, 스피커의 전원을 공급한다.

![IMG_20211110_212057](https://user-images.githubusercontent.com/22253556/147058638-974f8da6-55c6-4709-9c73-bad601bd74c2.jpg)

스위치와 전원부 고정을 위해 전선쫄대를 가공해서 거치대를 만들었다.
![IMG_20211112_142543](https://user-images.githubusercontent.com/22253556/147058636-df59dd27-57a0-4968-bea2-9940ea1dd51f.jpg)
부품을 끼우고
![IMG_20211112_142618](https://user-images.githubusercontent.com/22253556/147058634-62fbb94b-f69b-470b-a7c7-4ab3781e38fa.jpg)

매킨토시 뒷면에 고정한다. 근데 접착력이 약해서 너무 잘 떨어진다.. 하단의 USB 단자도 같은 방법으로 부착했다.

![IMG_20211112_153834](https://user-images.githubusercontent.com/22253556/147058631-1c6b3872-fc7a-476f-970c-5aa458cb0800.jpg)

## 내부 부품 설치

손바닥만한 [미니 PC](https://ko.aliexpress.com/item/1005001921619318.html)를 구입했다. 가격은 18만원에 스펙은 인텔 셀러론 J4125 / 8GB RAM / 128GB SSD이다.

![IMG_20211110_125024](https://user-images.githubusercontent.com/22253556/147058649-472fe891-9876-444d-b498-c1a0316748a9.jpg)

[USB 스피커](https://ko.aliexpress.com/item/1005001679890985.html)도 구입했다.
![image](https://user-images.githubusercontent.com/22253556/147070152-c9c03e05-5b00-42e5-8a2a-9e97371b0830.png)

내부에 미니PC, 스피커, AD 보드, 멀티탭을 설치한다. 접착제: 중력
![IMG_20211123_164636](https://user-images.githubusercontent.com/22253556/147058625-81f46844-5979-405c-8114-2fbbddc374ba.jpg)

매킨토시 좌측 버튼을 그대로 사용하기 위해, 미니PC와 AD보드 전원 버튼을 정렬했다.

![IMG_20211123_16422654 (1)](https://user-images.githubusercontent.com/22253556/147071057-415c61de-7024-467b-95dd-6a90b515ce76.jpg)

## 화면 설정

아이패드 화면이 매킨토시 모니터보다 커서 화면이 잘린다. 인텔 그래픽 설정에서 스케일링을 조절해서 좌우로 잘리는 부분을 없앤다.
![IMG_20211221_154214](https://user-images.githubusercontent.com/22253556/147058517-daf8a9e8-092d-4944-b1a0-36c23e37dbc8.jpg)

## 완성

뮤직 플레이어로 사용하기도 하고, 나중에 WebGL로 만든 작품들을 전시하는 용으로 사용할 계획이다. 키보드는 [Vortex Core](http://www.vortexgear.tw/vortex2_2.asp?kind=47&kind2=224&kind3=&kind4=1033)인데 맥과 잘 어울린다.

![IMG_20211127_122119](https://user-images.githubusercontent.com/22253556/147058583-6341a27a-e31f-4e54-8fba-e3bd46fdb5ba.jpg)

어울리는 마우스로 아래에 50 Fifty Concepts Retro Computer Mouse를 사려고 했는데, 배송비까지 5만원이나 해서 도저히 못 사겠다(마우스 1만원, 배송비 4만원).

![image](https://user-images.githubusercontent.com/22253556/147072828-9f893d91-bf37-4e9f-9ee2-5907f2b9ca54.png)

그래서 그냥 [Fluent Search](https://fluentsearch.net/)의 Screen Search 기능으로 마우스 없이 쓴다.

![image](https://user-images.githubusercontent.com/22253556/147073693-fe39c0b7-361f-4445-891c-a05928c3dd6d.png)

그리고 그 돈으로 아케이드 스틱을 구매했다.

![IMG_20211215_195354](https://user-images.githubusercontent.com/22253556/147058550-5afee388-9381-4be3-9b79-c6980bac69b2.jpg)

슬라이딩 서랍에 스틱을 올려놓고 쓴다.

![IMG_20211222_151452](https://user-images.githubusercontent.com/22253556/147058531-de681e8f-b7ac-41d0-b388-c645c95317dc.jpg)

심심할 때 메탈슬러그 한 판씩 하면 재밌다.

![IMG_20211222_151656](https://user-images.githubusercontent.com/22253556/147058493-0013563c-26ce-4084-a8cc-cc3746757f2c.jpg)

끝
