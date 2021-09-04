---
title: 구글 Meet를 3D 가상교실로 만드는 크롬 확장 프로그램
date: 2021-06-22T21:00:00+09:00
author: yongjin0802
categories:
  - Development
tags:
  - Metaverse
---

구글 Meet를 가상 교실로 바꿔서 지루한 화상 수업을 재밌고 인터랙티브하게 만드는 프로그램이다.

![image](https://user-images.githubusercontent.com/22253556/132088981-e9737d44-c195-48f4-a1d0-b81de2d21b34.png)

21-1 종합설계 팀 프로젝트로 진행했고 기술적 난이도 때문에 거의 혼자 다 만들었다.

## 기술 스택

### 프론트엔드

- `React.js` - 컴포넌트 라이프 사이클 관리
- `React Three Fiber` - 3D 화면
- `React Three Cannon` - 3D 객체 충돌
- `Evergreen UI` - UI
- `Zustand` - 상태 관리

### 백엔드

- `Node.js`
- `Socket.io`

## 기능

- 구글 미트 화면을 가상 교실로 만들기
- 3D 오브젝트 교실에 불러와서 인터랙션 하기
- 화면 공유 시 칠판에 화면 표시
- 감정 표현 애니메이션 등

&nbsp;

# 개발과정

## 그래픽스 기초 다지기

- 고려대 [컴퓨터 그래픽스](https://www.youtube.com/playlist?list=PLYEC1V9tJOl03WLDoUEKbiYW_Xt4W6LTl) 강의를 보면서 행렬 연산에 대한 두려움을 없앴다.

## 3D 게임 개발 기초 다지기

- 유데미의 [Create a 3D multi-player game using THREE.js and Socket.IO](https://www.udemy.com/course/create-a-3d-multi-player-game-using-threejs-and-socketio/) 강의를 보면서 3D 게임 제작과 클라이언트 데이터 동기화 기술을 익혔다.

- 유튜브의 [Building JavaScript Minecraft in 1 Hour [React & Three.js Tutorial]](https://youtu.be/ZnXKmODEFHA)를 보면서 `React Three Fiber`와 `Cannon` 사용법을 익혔다.

## 가상 교실 만들기

### 1. 교실 3D 모델 다운로드

- SketchFab에서 [무료 3D 교실 모델](https://sketchfab.com/3d-models/anime-classroom-3f49271eb0dc404e87333baebca59886)을 다운로드했다.

### 2. 교실 모델 수정

- [블렌더 기초 강의](https://www.youtube.com/playlist?list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6)를 보면서 교실에서 불필요한 개체를 제거하고 크기와 위치를 조절했다.

### 3. 교실 모델 내보내기

- [Blender How to Export FBX with Texture - Tutorial](https://youtu.be/kEP34CbPWUo)를 보고 교실에 텍스쳐를 입혀서 FBX 파일로 저장했다.

## 캐릭터 구현하기

### 1. 캐릭터 FBX 파일 다운로드

![image](https://user-images.githubusercontent.com/22253556/132090166-5d09f7d1-2293-41ce-b83d-3a4acedef6fe.png)

- 무료 에셋인 [Ultimate Animated Character Pack](https://quaternius.com/packs/ultimatedanimatedcharacter.html)를 다운받아서 사용했다.

### 2. 캐릭터 애니메이션

- [Loading Animated Characters in React Three Fiber](https://youtu.be/q7yH_ajINpA)를 보면서 [Mixamo](https://www.mixamo.com/)에서 가져온 애니메이션을 적용했다.
- 애니메이션 FBX 파일을 불러와서 캐릭터의 `animations` 배열에 넣는다.
- `AnimationMixer`를 사용해서 애니메이션을 재생한다.

### 3. 캐릭터 컨트롤

- [camera-controls](https://github.com/yomotsu/camera-controls) 라이브러리와 [meshwalk의 `TPSCameraControls`](https://github.com/yomotsu/meshwalk/blob/master/src/TPS/TPSCameraControls.js)를 참조해서 [Sketchbook 데모](https://jblaha.art/sketchbook/0.4/) 같은 자연스러운 3인칭 카메라 컨트롤을 구현했다.

### 4. 캐릭터 중복 사용 허용하기

- 다른 사용자가 같은 캐릭터를 사용하는 경우가 있다.
- 다른 컴포넌트에서 동일한 캐릭터 FBX 객체를 사용하는 경우 에러가 발생한다.
- `SkeletonUtils.clone`으로 FBX 객체를 복사하고 `useMemo`해서 사용하면 문제가 해결된다.

## 3D 오브젝트 불러오기

- SketchFab의 3D 모델을 교실에 불러올 수 있는 기능을 제공한다.

<video width="500px" src="https://user-images.githubusercontent.com/22253556/132090623-58abcca7-a4ed-4a0d-a530-fc3f44aa1490.mp4">
<center><summary>3D 모델 검색, 로딩, 조작, 자세히 보기를 하는 모습</summary></center>

### 3D 오브젝트 검색 기능

- 모델 검색 기능은 스케치팹의 공개 API와 그리드 레이아웃 적용해서 간단하게 구현했다.

### 3D 오브젝트 로딩 기능

- 문제는 3D 모델 다운로드 요청 시 zip 파일 다운로드 경로가 응답으로 왔다.

- 클라이언트에서 zip 파일 압축을 해제할까 생각했지만, 서버에 자원을 모아두고 클라이언트에서 불러오는 게 여러 측면에서 효율적이라 모델 불러오기 서버 API를 따로 구현했다.

```js
/** 스케치팹 3D 모델 다운로드 유틸 함수 */
const downloadSketchFab = async (uid) => {
  const dirPath = getModelPath(uid) // 모델 폴더 경로
  const zipPath = getModelPath(uid + '.zip') // 모델 압축 파일 경로
  // 이미 있는 파일이거나 압축 해제 중이면 나가기
  if ((await existDir(zipPath)) || (await existDir(dirPath))) return

  const zipUrl = await fetchModelZipUrl(uid) // 모델 zip 다운로드 URL 가져오기
  await download(zipUrl, zipPath) // 다운로드
  await unzip(zipPath) // 압축 해제
  await deleteFile(zipPath) // zip 파일 제거
}
```

- 모델의 `uid`를 받으면 모델의 Zip 파일을 다운로드해서 압축을 해제한다.

> 위 코드에는 문제가 하나 있는데, zip 파일이 존재하는 상태라면, zip 파일을 다운로드하거나 압축을 푸는 중이므로, 해당 작업이 종료될 때가지 함수 종료를 막아야 할 것 같다.

## 의자 앉기 기능

- 의자에 투명한 박스를 놓는다.
- 박스에 마우스를 올리면 박스가 나타나게 한다.
- 박스 클릭 시 캐릭터를 의자로 이동시키고 캐릭터의 앉기 애니메이션을 실행한다.

## 캐릭터, 3D 오브젝트 동기화

- 클라이언트는 현재 상태(캐릭터와 오브젝트의 위치, 방향)를 40ms마다 서버에 보낸다.
- 서버는 받은 정보를 종합해서 클라이언트에 40ms마다 브로드캐스팅한다.

## 크롬 확장 프로그램 포팅

<video width="500px" src="https://user-images.githubusercontent.com/22253556/132100820-48dab946-c8fa-43d8-ab2e-8968fa38c161.mp4">

- [Create chrome extension with ReactJs using inject page strategy](https://itnext.io/create-chrome-extension-with-reactjs-using-inject-page-strategy-137650de1f39)를 보고 앱을 크롬 확장 프로그램으로 포팅했다.

### 웹팩 설정 변경

1. `yarn run eject`로 `create-react-app`의 기본 웹팩 설정 파일을 추출한다.

2. [Make extension compatible with Create React App v2.x](https://github.com/satendra02/react-chrome-extension/issues/2)를 보면서 `[ROOT]/config/webpack.config.js` 파일을 수정한다.

   - `entry`로 `content`를 추가한다.
   - 번들된 파일에 해시가 들어가지 않게 한다.

3. 크롬 확장의 메인 파일과 같은 `content.js`를 만든다.

4. `manifest.json`에 `content.js`와 빌드된 파일의 경로를 추가한다.

### 스태틱 에셋 URL 변경

크롬 확장에서 스태틱 파일(캐릭터나 교실 FBX 파일)을 불러올 때는 `chrome.runtime.getURL` 함수를 사용해야 한다.

URL로 에셋을 가져올 때는 아래 함수를 사용한다.

```js
/* global chrome*/

/** 프로덕션에서 크롬 확장에 맞게 URL을 가져오는 함수 */
export const getUrl =
  process.env.NODE_ENV === 'production' ? chrome.runtime.getURL : (v) => v
```

## 구글 Meet의 `Content Security Policy` 우회

- 물리 엔진 라이브러리인 `Cannon` 내부에서 Web Worker 사용한다.
- 구글 Meet의 `index.html` 파일을 불러올 때
  응답 헤더가 `Content Security Policy`가 `script-src 'self'`로 설정되어 있다.
- 이로 인해, Web Worker 스크립트 생성이 브라우저 보안 정책에 위배된다.
- 그래서 Web Worker 생성 시 에러가 발생하고 확장 프로그램이 정상적으로 실행되지 않음

### CSP 우회 방법

1. [Disable Content-Security-Policy](https://chrome.google.com/webstore/detail/disable-content-security/ieelmcmcagommplceebfedjlakkhpden?hl=en) 크롬 확장 프로그램 설치하거나
2. 현재 프로그램도 크롬 확장이므로, 직접 크롬의 웹 요청을 가로챈 뒤 `content-security-policy` 헤더 제거하면 된다.

```js
/*global chrome*/

const onHeadersReceived = function (details) {
  if (details.initiator !== 'https://meet.google.com') return

  for (let i = 0; i < details.responseHeaders.length; i++) {
    if (
      details.responseHeaders[i].name.toLowerCase() ===
      'content-security-policy'
    ) {
      details.responseHeaders[i].value = ''
    }
  }

  return {
    responseHeaders: details.responseHeaders,
  }
}

const onHeaderFilter = { urls: ['*://*/*'], types: ['main_frame', 'sub_frame'] }

// Send a message to the active tab
chrome.webRequest.onHeadersReceived.addListener(
  onHeadersReceived,
  onHeaderFilter,
  ['blocking', 'responseHeaders']
)

chrome.browserAction.onClicked.addListener(async () => {
  chrome.tabs.query({ active: true, currentWindow: true }, (tabs) => {
    const activeTab = tabs[0]
    chrome.tabs.sendMessage(activeTab.id, {
      message: 'clicked_browser_action',
    })
  })
})
```

## 구글 Meet와 확장 프로그램 연동하기

다음 정보를 구글 Meet 앱에서 가져와서 3D 화면에 표시하고 있다.

1. 이름
2. 아이디
3. 공유된 화면
4. 채팅

### 이름과 아이디 가져오기

1. 사용자 목록을 연다.
2. 사용자 목록 맨 위 항목 요소의 `data-participant-id`에서 아이디를, 항목의 첫 번째 `span`의 텍스트에서 이름을 가져온다.

### 공유된 화면 가져오기

<video width="500px" src="https://user-images.githubusercontent.com/22253556/132100785-95576288-b6d2-4ae3-9899-f481803f3223.mp4">

- 화면 공유는 3가지 상태를 갖는다.

  1. 발표가 없는 상태 (`발표 시작` 버튼이 존재)
  2. 내가 발표 중인 상태 (`본인이 발표 중입니다.` 버튼이 존재)
  3. 남이 발표 중인 상태 (1, 2가 아닌 경우)

- 위 3가지 상태를 0.5초마다 확인해서 상태가 변경된 경우 `칠판 컴포넌트`에 발표 중인 `video` 요소를 전달한다.

### 채팅 가져오기

<video width="500px" src="https://user-images.githubusercontent.com/22253556/132100822-3d27aeb2-7c31-4da4-8c9e-9195aa9afd0a.mp4">

- `data-sender-id` 속성을 가진 요소는 채팅이다.
- 채팅 요소에서 `senderId`, `timestamp`, `innerText`를 가져와서 `채팅 컴포넌트`에 전송한다.

### 3D 화면 삽입하기

- 카메라 화면이 나오는 비디오 컨테이너에 3D 화면을 삽입하고 있다.
- `data-allocation-index` 속성을 가진 요소의 부모 요소이다.
- 구글 Meet의 JS 라이브러리의 UI 리렌더링 시 3D 화면이 소멸되지 않는 최적의 위치다.

---

## 의의

- 요즘 트렌드인 메타버스를 주제로 프로젝트를 진행했다.
- 구글 Meet의 인프라를 재활용하므로 서버의 부담이 적다.
- 3D 오브젝트를 수업에 활용할 수 있다. ex) 천문학 수업에서 태양계 보여주기
- 현실과 비슷한 상호작용을 할 수 있다. ex) 궁금하면 손들기, 박수 치기, 큐플레이 같은 OX 퀴즈

## 느낀 점

- 기능 구현에만 신경을 써서 코드 상태가 안 좋다. 다음엔 테스트 가능한 코드를 작성하고 싶다.
- 리액트가 3D 컴포넌트의 생애주기를 관리해줘서, 코드를 작성하기 너무 편하다.
  - 컴포넌트 제거 시, 제거 메서드를 호출하는 대신 그냥 컴포넌트를 렌더링 안 하면 된다.
- Fiber로 동기적인 Hook 코드를 작성하는 건 신세계다.
- WebGL을 좀 더 파봐야겠다.
