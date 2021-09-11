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

# 서버 구현

## 기술 스택

- Nest.js
- TypeScript
- TypeORM
- Postgres

## Nest.js

- [Nest.js 공식 문서](https://docs.nestjs.com/)를 정독하면서 필요한 기능을 구현했다.
- 기능을 서비스, 컨트롤러, 모듈로 나누고 합칠 수 있는게 복잡성 증가 속도를 늦춘다.
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

- 모델링의 편함을 위해 `User`와 `Tutor` 엔티티를 나눈게 후회된다.
- `Tutor`가 `User` 엔티티를 [상속](https://orkhan.gitbook.io/typeorm/docs/entity-inheritance#single-table-inheritance)받아야 했다.
- 두 엔티티에 대해 지원해야 하는 기능이 거의 비슷해서 기능을 두 개씩 구현해야 했다.
  - 로그인, 회원가입, 이메일 인증 기능도 유저따로 튜터따로 2개씩
  - 그로 인해 테스트도 2배, UI도 2배로 구현했다.

## 테스트

- 56개가 되는 컨트롤러를 Postman으로 하나하나 테스트할 수 없어서 테스트 코드를 열심히 작성했다.
- 암호화나 이메일 전송 등 비용이 큰 코드는 목업했다.
  - 참조한 블로그: [Testing NestJS services with integration tests](https://wanago.io/2020/07/13/api-nestjs-testing-services-controllers-integration-tests/)
- 서비스 유닛 테스트는 목업할 게 너무 많아서 `supertest`를 이용한 통합 테스트 코드를 주로 작성했다.

### 보완할 점

- 통합 테스트 전부를 실행하면 데드락이 발생한다.
  - TypeORM의 트랜잭션 매니저를 사용해도 마찬가지인데, 이건 좀더 경험이 필요한 부분인 것 같다.
- 테스트 DB를 인메모리 Sqlite로 교체해서 테스트 속도를 높이고 싶다.
  - `timestamptz`가 sqlite에 없는게 문제다.

## 예외로 코드 단순화하기

- 메서드의 깊이에 상관없이 예외로 컨트롤 플로우를 탈출할 수 있는 점을 활용했다.
- 없는 엔티티 참조나 비즈니스 로직 위반 발생 시 4XX 예외를 일단 발생시킨다.
  - 예외가 발생하지 않았으면 안전하게 엔티티를 참조하고 도메인 로직을 수행할 수 있다.
- 명확한 에러 메시지와 함께 예외 처리 책임을 클라이언트에 넘긴다.

&nbsp;

# 클라이언트 구현

## 기술 스택

- React + TypeScript
- Ant Design
- Formik
- MobX
- React Query
- Simple Peer WebRTC
- Socket.io

## TypeSafe한 Axios API 구현

- 내용이 길어서 [해당 포스트](https://yongj.in/2021-06-25-typesafe-api)에 따로 작성했다.

## 튜터링 예약

- 사용자는 튜터 스케줄을 예약해서 약속을 잡을 수 있다.
- 이때, 사용할 교재와 요청 사항을 입력한다.

<video width="100%" controls="controls">
  <source src="https://user-images.githubusercontent.com/22253556/132957380-7e6d5d3c-b534-4a06-8ee5-af1390d7f58d.mp4" type="video/mp4">
</video>

## 튜터링 진행

- 약속 1시간 전부터, 튜터링 페이지에 접근할 수 있다.
- `Ready` 버튼을 눌러 화상 채팅을 연결한다.
- 좌측의 교재를 선택하면, 상대의 교재도 변경된다.
- 문자 채팅도 지원한다.
- 그리드 레이아웃을 사용해서 데스크탑과 모바일을 모두 지원한다.

<video width="100%" controls="controls">
  <source src="https://user-images.githubusercontent.com/22253556/132957316-a29e9314-53c5-40f6-9160-adc099dad017.mp4" type="video/mp4">
</video>

.. 이후 내용은 내일 적어야겠다
