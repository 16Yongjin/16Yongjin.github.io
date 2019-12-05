---
id: 33
title: Mac os에서 Windows 용 exe파일을 실행하는 법
date: 2017-04-08T17:20:04+09:00
author: yongjinsite
layout: post
guid: https://yongjinsite.wordpress.com/?p=33
permalink: '/2017/04/08/mac-os%ec%97%90%ec%84%9c-windows-%ec%9a%a9-exe%ed%8c%8c%ec%9d%bc%ec%9d%84-%ec%8b%a4%ed%96%89%ed%95%98%eb%8a%94-%eb%b2%95/'
categories:
  - Utility
tags:
  - Wine
---
윈도우 프로그램을 돌릴려면 가상머신으로 윈도우를 설치하면 된다.

하지만 귀찮다.

이를 해결해주는 오픈소스 프로그램인 **WineBottler**

http://winebottler.kronenberg.org

간단히 설치만으로 플래시 잔뜩 들어있는 윈도우 프로그램을 맥에서 돌리게 해준다.

그리고 실행 뿐만 아니라 프로그램 설치도 가능하다.

<img class="alignnone size-full wp-image-38" src="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-5-06-41.png" alt="스크린샷 2017-04-08 오후 5.06.41.png" width="1386" height="1462" srcset="https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-5-06-41.png 1386w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-5-06-41-284x300.png 284w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-5-06-41-768x810.png 768w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-5-06-41-971x1024.png 971w, https://yongj.in/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-08-ec98a4ed9b84-5-06-41-1000x1055.png 1000w" sizes="(max-width: 1386px) 100vw, 1386px" /> 

&nbsp;

Wine(Wine Is Not an Emulator)은 유닉스 API 규격인 **POSIX**(Portable Operating System Interface)와 호환되는 운영체제에서 윈도우 프로그램을 실행하게 해준다. 즉 .exe를 맥, 유닉스 등에서 사용할 수 있다.

**GNU Lesser General Public License** (**LGPL**)를 따르고 있어서 상업적으로 이용해도 소스코드를 공개 안해도 된다.