---
title: 한국어 튜터링 플랫폼
date: 2021-06-26T21:00:00+09:00
author: yongjin0802
categories:
  - Development
---

WebRTC를 활용한 실시간 1:1 강의를 지원하는 튜터링 플랫폼

## 구현 동기

- 개인적으로 테이블 10개, 페이지 10개 이상인 서비스를 제작해보고 싶었다.
- 창업 동아리에 들어가서 적당한 규모의 아이템인 튜터링 플랫폼을 선택했다.
- 특히, 실시간 화상 대화 기능을 구현해보고 싶은 마음이 컸다.
- 기말고사 전 한 달 동안 수업 듣고 남는 시간에 만들었다.

## 기능

### 사용자

- 튜터링 약속 잡기/취소
- 튜터 리뷰

### 튜터

- 튜터링 스케쥴 관리
- 튜터링 후 사용자에게 피드백 주기

### 관리자

- 튜터 프로필 관리
- 튜터 승인
- 교재 관리
- 추천 리뷰 설정

### 튜터링 기능

- 실시간 화상 대화
- 문자 채팅
- 보고 있는 교재 동기화

### 인증

- 회원가입, 로그인
- 이메일 인증
- 비밀번호 변경

&nbsp;

# [서버](https://github.com/16Yongjin/tutoring-server) 구현

## 기술 스택

- Nest.js
- TypeScript
- TypeORM
- Postgres

## Nest.js

- [Nest.js 공식 문서](https://docs.nestjs.com/)를 정독하면서 필요한 기능을 구현했다.
- 기능을 서비스, 컨트롤러, 모듈로 나누고 합칠 수 있는 게 복잡성 증가 속도를 늦춘다.
  - 한 도메인에서 다른 도메인의 엔티티가 아닌 서비스를 사용함으로써 도메인 간 경계가 확실해지고 기능이 섞이는 일이 예방됐다.
- 다양한 데코레이터로 코드 중복을 줄일 수 있었다.
  - DTO에 붙은 [`class-validator`](https://github.com/typestack/class-validator)로 속성을 검증하는 `ValidationPipe`
  - `JWT`를 확인하는 `JwtAuthGuard`
  - 요청 내 사용자 정보의 권한을 확인하는 `RoleGuard`

## 엔티티 구성

[typeorm-uml](https://github.com/eugene-manuilov/typeorm-uml) 라이브러리로 그린 엔티티 관계도이다.

![typeorm-uml](https://user-images.githubusercontent.com/22253556/132950349-03c853f4-960e-4014-9543-f1531a42ebdc.png)

- 튜터는 튜터링 스케쥴(`Schedule`)을 생성한다.
- 사용자는 스케쥴에 따라 튜터링 약속(`Appointment`)을 생성한다.
- 튜터링을 마치고 튜터는 사용자에게 피드백(`Feedback`)을 남긴다.
- 사용자는 유저에게 리뷰(`Review`)를 남긴다.
- 관리자는 교재(`Material`)을 관리한다.
- 회원 가입 시 이메일 인증(`EmailVerification`)을 거친다.

### 보완할 점

- 모델링의 편함을 위해 `User`와 `Tutor` 엔티티를 나눈 게 후회된다.
- `Tutor`가 `User` 엔티티를 [상속](https://orkhan.gitbook.io/typeorm/docs/entity-inheritance#single-table-inheritance)받아야 했다.
- 두 엔티티에 대해 지원해야 하는 기능이 거의 비슷해서 기능을 두 개씩 구현해야 했다.
  - 로그인, 회원가입, 이메일 인증 기능도 유저 따로 튜터 따로 2개씩
  - 그로 인해 테스트도 2배, UI도 2배로 구현했다.

## 테스트

- 56개가 되는 컨트롤러를 Postman으로 하나하나 테스트할 수 없어서 테스트 코드를 열심히 작성했다.
- 암호화나 이메일 전송 등 비용이 큰 코드는 목업했다.
  - 참조한 블로그: [Testing NestJS services with integration tests](https://wanago.io/2020/07/13/api-nestjs-testing-services-controllers-integration-tests/)
- 서비스 유닛 테스트는 목업할 게 너무 많아서 `supertest`를 이용한 통합 테스트 코드를 주로 작성했다.

### 보완할 점

- 통합 테스트 전부를 실행하면 데드락이 발생한다.
  - TypeORM의 트랜잭션 매니저를 사용해도 마찬가지인데, 이건 좀 더 경험이 필요한 부분인 것 같다.
- 테스트 DB를 인메모리 Sqlite로 교체해서 테스트 속도를 높이고 싶다.
  - `timestamptz`가 sqlite에 없는게 문제다.

## 예외로 코드 단순화하기

- 메서드의 깊이에 상관없이 예외로 컨트롤 플로우를 탈출할 수 있는 점을 활용했다.
- 없는 엔티티 참조나 비즈니스 로직 위반 발생 시 4XX 예외를 일단 발생시킨다.
  - 예외가 발생하지 않았으면 안전하게 엔티티를 참조하고 도메인 로직을 수행할 수 있다.
- 명확한 에러 메시지와 함께 예외 처리 책임을 클라이언트에 넘긴다.

## 튜터 별점 실시간 평균 구하기

- 튜터 리뷰가 추가될 때마다 튜터의 평균 별점을 구해야 한다.
- 그때마다 모든 리뷰 목록을 가져와서 계산하는 건 비효율적이다.
- 튜터의 별점과 리뷰 개수만 알면, 실시간으로 평균 별점을 구할 수 있다.

```ts
if (tutor.reviewCount === 0) {
  tutor.reviewCount = 1
  tutor.rating = rating
} else {
  tutor.rating =
    (tutor.rating * tutor.reviewCount + rating) / (tutor.reviewCount + 1)
  tutor.reviewCount += 1
}
```

- 기존 별점 \* 리뷰 개수는 이전 별점의 총합이다.
- 여기에 새 별점을 더하고, 새 리뷰 개수로 나누면 된다.

&nbsp;

# [클라이언트](https://github.com/16Yongjin/tutoring-app) 구현

## 기술 스택

- React + TypeScript
- Ant Design
- Formik
- MobX
- React Query
- Simple Peer WebRTC
- Socket.io

## TypeSafe한 Axios API 구현

- 내용이 길어서 [해당 포스트](http://yongj.in/tutorials/typesafe-api/)에 따로 작성했다.
- API의 정의와 호출를 분리해서 코드 재사용성을 높였다.

## 튜터링 예약

- 사용자는 튜터 스케줄을 예약해서 약속을 잡을 수 있다.
- 이때, 사용할 교재와 요청 사항을 입력한다.

<video width="100%" controls="controls">
  <source src="https://user-images.githubusercontent.com/22253556/132957380-7e6d5d3c-b534-4a06-8ee5-af1390d7f58d.mp4" type="video/mp4">
</video>

### 빠른 유튜브 임베드

- 튜터 프로필 이미지 클릭 시, 튜터 소개 유튜브 영상이 나오게 된다.
- 유튜브 삽입 시 [lite-youtube-embed](https://github.com/paulirish/lite-youtube-embed)를 사용하면 기본 임베드 보다 200배 빠르다.

## 튜터링 진행

- 약속 1시간 전부터, 튜터링 페이지에 접근할 수 있다.
- `Ready` 버튼을 눌러 화상 채팅을 연결한다.
- 좌측의 교재를 선택하면, 상대의 교재도 변경된다.
- 문자 채팅도 지원한다.
- 그리드 레이아웃을 사용해서 데스크톱과 모바일을 모두 지원한다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/7idm4AtpPk8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 화상 대화 기능 구현

<iframe width="560" height="315" src="https://www.youtube.com/embed/oxFr7we3LC8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 위 강의를 보고 [Simple Peer](https://github.com/feross/simple-peer)와 React의 [Context API](https://reactjs.org/docs/context.html)를 사용해서 비디오 챗을 구현했다.
- `Peer` 생성 후 시그널링 데이터가 만들어지면 소켓 통신을 통해 상대방과 시그널을 주고받는다.
- P2P 연결 후, 스트림이 생성되면 이를 비디오 요소의 `srcObject`로 설정하면 된다.

### 비디오/오디오 켜기/끄기

```ts
// 비디오 토글
stream.getVideoTracks().forEach((track) => {
  track.enabled = !track.enabled
})

// 오디오 토글
stream.getAudioTracks().forEach((track) => {
  track.enabled = !track.enabled
})
```

### 가끔 리액트의 클래스 컴포넌트가 필요한 경우

- 튜터링 페이지를 나가면, 미디어 스트림을 끊어야 한다. 안 그러면 카메라가 계속 켜진 상태가 유지된다.
- `useEffect(fn, [])`는 렌더링된 비디오 요소가 사라진 뒤에 자원 해제가 실행된다.
- 클래스 컴포넌트의 `componentWillUnmount`를 사용해서 비디오 요소의 미디어 스트림을 해제했다.
- 근데, 가장 확실한 자원 해제 방법은 새로고침인 것 같다.

## 플랫한 네비게이션 라우터

<img height="500px" src="https://user-images.githubusercontent.com/22253556/132973413-e999684b-cfe6-4f98-acb1-4099ed43e742.png" alt="mobile-navigation">

- 모바일 네비게이션 드로어는 사용자, 튜터, 관리자 등의 역할에 따라 다르게 보인다.
- 처음에는 아래처럼 하나 프래그먼트 안에서 역할에 따라 분기했다.

```tsx
<Drawer>
  <Card>Home</Card>
  {user && <Card>About</Card>}
  {!isTutor && <Card>Tutors</Card>}
  {user && !isTutor && <Card>Appointments</Card>}
  {isAdmin && <Card>Dashboard</Card>}
  {/** 다른 네비게이션 */}
</Drawer>
```

- 갈수록 코드 분기가 복잡해져서 다음처럼 변경했다.
- 약간의 중복을 허용함으로써 코드는 보기 편해졌다.

```tsx
<Drawer>
  {isPublic && (
    <>
      <Card>Home</Card>
      <Card>About</Card>
      <Card>Material</Card>
    </>
  )}
  {isUser && (
    <>
      <Card>Home</Card>
      <Card>My Page</Card>
    </>
  )}
  {isTutor && (
    <>
      <Card>Home</Card>
      <Card>Main Page</Card>
    </>
  )}
  {isAdmin && (
    <>
      <Card>메인</Card>
      <Card>교재 관리</Card>
      <Card>튜터 관리</Card>
    </>
  )}
</Drawer>
```

- DRY 원칙을 가끔 어겨도 좋을 때가 있는 것 같다.

### 상태 기반 렌더링

- 위의 방식을 적용해서 코드의 복잡성을 제어한 사례가 하나 더 있다.

<img height="500px" src="https://user-images.githubusercontent.com/22253556/132973952-a3cb262b-8ee9-43a7-93ef-1fe75e7db141.png" alt="appointment-control">

- 튜터링 페이지는 시간과 상황에 따라 6가지 상태가 있다.
  - 시작 전
  - 1시간 안에 시작
  - 시작됨 (화상 연결 전)
  - 진행 중
  - 시간 초과
  - 끝남
- 튜터링까지 남은 시간과 화상대화 연결 여부에 따라 상태 중 하나를 결정한다.
- 각 상태에 맞게 필요한 컴포넌트를 렌더링한다. (위 사진의 빨간줄 부분)

## 코드 분할로 초기 로딩 속도 높이기

![material](https://user-images.githubusercontent.com/22253556/132974087-9975654c-817e-4319-9e9a-e4391274a4d7.png)

- 관리자는 교재의 연습문제를 수정할 수 있다.
- 연습문제 수정은 [`react-draft-wysiwyg`](https://www.npmjs.com/package/react-draft-wysiwyg)를 사용한다.
- 해당 라이브러리는 번들 크기를 300KB 정도 차지해서 초기 로딩 속도를 늦춘다.
- 해당 컴포넌트는 모든 사람이 사용하는게 아니므로 코드 분할을 통해 번들 크기를 줄이고 초기 로딩 속도를 높였다.

```tsx
const CourseDetail = React.lazy(() => import('../admin/CourseDetail'))

<Suspense fallback={<div>Loading...</div>}>
  <CourseDetail />
</Suspense>
```

## 배포

- [Netlify](https://www.netlify.com/)로 배포했다.
- 레포에 Push만 하면 자동으로 배포돼서 편하다.
- HTTPS 설정도 쉽다.
- 빌드 시 `CI=false` 설정을 해야, 경고가 발생해도 빌드가 멈추지 않는다.

&nbsp;

# 마무리

## 느낀 점

- 시간 압박 때문에 기능 구현에 집중하다가 테스트가 힘든 코드가 작성됐다.
  - 전 회사 코드가 이랬는데, 왜 그렇게 됐는지 이제 이해가 된다.
  - 비디오 채팅 같이 테스트가 힘든 부분도 테스트할 방법을 찾고 싶다.
- 작은 서비스라도 구현할 기능은 산더미다
  - 인증 이메일 다시 보내기와 약관 동의 등 빠뜨린 기능이 쌓여있다.
  - 교재 안에 토픽, 강의, 연습이 있는데 각각의 읽기, 생성, 수정, 삭제 기능 등, 반복되는 구현이 많았다.
    - 반복되는 CRUD 기능 구현을 자동화할 방법이 필요하다.
- 가장 중요한 건 서비스에 대한 애정과 책임감인 것 같다.
  - 이거 없으면 못하겠다… 디자인도 예쁘게 안 나옴.
