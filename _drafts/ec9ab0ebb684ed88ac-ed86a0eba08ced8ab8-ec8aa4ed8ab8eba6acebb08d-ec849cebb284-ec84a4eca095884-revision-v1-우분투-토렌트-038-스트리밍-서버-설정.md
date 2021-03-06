---
id: 899
title: '우분투 토렌트 &#038; 스트리밍 서버 설정'
date: 2019-05-19T11:37:22+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/05/19/884-revision-v1/
permalink: /2019/05/19/884-revision-v1/
---
### 개요

  1. 구글 클라우드 플랫폼에서 가상머신을 생성한다.
  2. 방화벽을 설정한다. 외부에서 서버에 접속하기 위해서다.
  3. Transmission-daemon을 설치한다. 토렌트를 다운받기 위해서다.
  4. plex media server를 설치한다. 웹브라우저에서 영화를 보기 위해서다.

### 1. 가상머신 생성하기

구글 클라우드 플랫폼에 가입하고 신용카드를 등록하면 1년간 쓸 수 있는 크레딧 300달러를 준다.

Compute Engine 메뉴로 들가서 인스턴스(가상머신)를 만든다.

<div class="wp-block-image">
  <figure class="aligncenter"><img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/인스턴스만들기버튼.png" alt="" class="wp-image-887" /><figcaption>클릭</figcaption></figure>
</div><figure class="wp-block-image">

<img src="https://i2.wp.com/yongj.in/wp-content/uploads/2019/05/인스턴스만들기.png?fit=602%2C1024&ssl=1" alt="" class="wp-image-886" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/인스턴스만들기.png 758w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/인스턴스만들기-176x300.png 176w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/인스턴스만들기-602x1024.png 602w" sizes="(max-width: 758px) 100vw, 758px" /> <figcaption>인스턴스 설정 예시</figcaption></figure> 

지역: 도쿄  
운영체제: 우분투 18.04  
디스크: 500GB 로 설정했다.

### 2. 방화벽 만들기

[좌측 상단 메뉴] &#8211; [VCN 네트워크] &#8211; [방화벽 규칙]에 들어가서 방화벽 규칙을 만든다

9091 포트를 열어서 토렌트를 업로드할 때 쓰는 웹페이지에 접속하기 위함이다.  


<div class="wp-block-image">
  <figure class="aligncenter"><img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/방화벽규칙만들기버튼.png" alt="" class="wp-image-888" /><figcaption>클릭</figcaption></figure>
</div><figure class="wp-block-image">

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/방화벽규칙만들기.png" alt="" class="wp-image-889" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/방화벽규칙만들기.png 595w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/방화벽규칙만들기-213x300.png 213w" sizes="(max-width: 595px) 100vw, 595px" /> </figure> 

이름: allow-torrent (아무거나 적는다.)  
대상 태그: torrent  
소스 IP 범위: 0.0.0.0/0  
지정된 프로토콜 및 포트: tcp: 9091

만들기 버튼 눌러서 저장

### 3. 방화벽을 가상머신에 적용하기

Compute Engine 메뉴로 돌아간다.

VM 인스턴스 리스트에 있는 가상머신의 이름(instance-1)을 클릭 후 [VM 인스턴스 세부정보] 페이지로 들어간다. 

상단의 수정 버튼으로 수정 모드로 들간 뒤<figure class="wp-block-image">

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/네트워크태그설정.png" alt="" class="wp-image-890" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/네트워크태그설정.png 924w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/네트워크태그설정-300x126.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/네트워크태그설정-768x322.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/네트워크태그설정-716x300.png 716w" sizes="(max-width: 924px) 100vw, 924px" /> <figcaption>방화벽 아래에 네트워크 태그</figcaption></figure> 

네트워크 태그에 방금 만든 방화벽의 태그인 torrent를 입력한다.

저장 버튼 눌러서 저장

### 4. SSH 접속

<a rel="noreferrer noopener" href="https://m.blog.naver.com/6116949/221244246623" target="_blank">윈도우10에 우분투 설치 및 사용</a> 을 보고 우분투를 설치한다.

  1. &#8216;Windows 기능 켜기/끄기&#8217;에서 &#8216;Linux용 Windows 하위 시스템&#8217; 활성화하고 재부팅
  2. 마이크로소프트 스토어에서 Ubuntu 설치

[GCP에 SSH 접속하기](https://ruuci.tistory.com/6) 를 보고 가상머신에 접속한다.

  1. SSH키 생성: ssh-keygen -t rsa -f ~/.ssh/[KEY\_FILE\_NAME] -C [USERNAME]
  2. 공개키 복사: cat ~/.ssh/[KEY\_FILE\_NAME].pub 입력 후 결과값 복사
  3. [Compute Engine] &#8211; [메타데이터] &#8211; [SSH 키] 에 추가
  4. ssh -i ~/.ssh/\[KEY\_FILE\_NAME\] \[USERNAME\]@[서버IP]로 접속

### 5. 토렌트 설치

토렌트 클라이언트인 Transmission-daemon을 설치한다.<figure class="wp-block-embed-wordpress wp-block-embed is-type-wp-embed is-provider-online-it">

<div class="wp-block-embed__wrapper">
  <blockquote class="wp-embedded-content" data-secret="FLGLIHXcrc">
    <a href="https://online-it.nu/install-transmission-torrent-client-ubuntu-18-04-bionic-beaver/">How To Install Transmission Torrent Client Ubuntu 18.04 Bionic Beaver</a>
  </blockquote>
</div></figure> 

위 글보고 따라하면 된다.

명령어 입력 시 &#8220;username&#8221;을 꼭 바꾸고 입력해야 한다. 안 했다가 오류나서 당황했다.

링크글 2.1에 오타가 있어서 `sudomkdir~/Downloads/Completed`명령어는 `sudomkdir~/Downloads/Complete` 로 입력하는 게 낫다.

추가로, 보안을 위해 `"rpc-authentication-required": true,` 로 설정하고 &#8220;rpc-username&#8221; 과 &#8220;rpc-password&#8221;를 설정하는 게 낫다.  


설정을 마치면 [서버주소]:9091로 접속하고 이름, 비밀번호 입력 시  
<figure class="wp-block-image">

<img src="https://i2.wp.com/yongj.in/wp-content/uploads/2019/05/토렌트페이지.png?fit=840%2C500&ssl=1" alt="" class="wp-image-894" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/토렌트페이지.png 1358w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/토렌트페이지-300x178.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/토렌트페이지-768x457.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/토렌트페이지-1024x609.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/토렌트페이지-1000x595.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/토렌트페이지-504x300.png 504w" sizes="(max-width: 1358px) 100vw, 1358px" /> </figure> 

토렌트를 업로드할 수 있는 페이지가 나온다.

앞에서 방화벽으로 9091포트를 설정한 것이 이 페이지에 접속하기 위해서였다.

### 6. 스트리밍 서버 설치

[Install Plex Media Server on Ubuntu 18.04](https://www.linode.com/docs/applications/media-servers/install-plex-media-server-on-ubuntu-18-04/) 를 보고 Plex Media 서버를 설치한다.

라이브러리 추가 시 토렌트 다운로드 폴더를 추가한다.  


설정을 마친 후 <http://app.plex.tv/desktop?secure=0> 로 접속하면 외부에서도 서버에 저장된 미디어를 볼 수 있다.<figure class="wp-block-image">

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/플렉스.png" alt="" class="wp-image-897" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/플렉스.png 767w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/플렉스-300x168.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2019/05/플렉스-536x300.png 536w" sizes="(max-width: 767px) 100vw, 767px" /> </figure> 

뒤에 ?secure=0은 꼭 붙여야한다. 보안 연결 설정이 잘 안되기 때문이다.

### 마무리

집 가고 싶다