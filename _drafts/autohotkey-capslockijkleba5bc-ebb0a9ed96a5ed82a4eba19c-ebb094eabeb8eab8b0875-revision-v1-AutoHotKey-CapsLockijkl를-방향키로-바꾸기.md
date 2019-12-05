---
id: 935
title: '[AutoHotKey] CapsLock+ijkl를 방향키로 바꾸기'
date: 2019-07-03T18:38:48+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/07/03/875-revision-v1/
permalink: /2019/07/03/875-revision-v1/
---
[gist]1ed465c8acb2d716f945ac09518e3aaf[/gist]

### 설명

맥에서 karabiner로 사용하던 단축키 그대로 사용하기 위한 오토핫키 스크립트다.

캡스락을 활성화/비활성화 하려면 캡스락 + f를 누른다.

캡스락 + ijkl 나 wasd를 방향키로 사용할 수 있다.

캡스락 + nm,. 을 각각 Home, End, PgUp, PgDn에 대응했다.

덕분에 손목을 거의 움직이지 않고 코드를 작성할 수 있다.

### Alt와 Ctrl 키 전환

오토핫키 스크립트로 Alt와 Ctrl 키를 전환할 수 있지만 가끔씩 키가 계속 눌리게 되는 오류가 자주 발생한다.

간단하게 레지스터 수정으로 Alt와 Ctrl 키를 바꿀 수 있다.

  1. Win + R 실행 &#8211; regedit 입력, 열기
  2. 컴퓨터\HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout 접속
  3. 오른쪽 마우스 클릭 &#8211; [새로 만들기] &#8211; [이진값 추가] 해서 Scancode Map 입력
  4. 아래의 값 입력<figure class="wp-block-image">

<img src="https://i0.wp.com/yongj.in/wp-content/uploads/2019/07/image-1.png?fit=840%2C522&ssl=1" alt="" class="wp-image-934" srcset="https://yongj.in/wp-content/uploads/2019/07/image-1.png 1243w, https://yongj.in/wp-content/uploads/2019/07/image-1-300x186.png 300w, https://yongj.in/wp-content/uploads/2019/07/image-1-768x477.png 768w, https://yongj.in/wp-content/uploads/2019/07/image-1-1024x636.png 1024w, https://yongj.in/wp-content/uploads/2019/07/image-1-1000x621.png 1000w, https://yongj.in/wp-content/uploads/2019/07/image-1-483x300.png 483w" sizes="(max-width: 1243px) 100vw, 1243px" /> </figure> 

5. 재시작 또는 로그아웃 후 로그인 시 적용됨

### 스크립트를 작성하면서 알게된 사실

  1. 한자 키나 한/영 키는 물리적으로 pressDown만 되고 pressUp 이벤트가 발생하지 않아 다른 단축키로 바꾸기 애매하다.
  2. 서피스 프로 타입 커버의 한/영 키와 오른쪽 Alt 키는 기능이 중복되어있고 이를 고칠 방법은 없다. (오른쪽 Alt키를 한영전환이 아닌 그냥 Alt키로 사용할 수가 없다.)