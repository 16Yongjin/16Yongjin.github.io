---
title: TypeSafe한 Axios API 만들기
date: 2021-06-25T21:00:00+09:00
author: yongjin0802
categories:
  - Tutorials
---

타입 안전한 API를 만드는 방법. API 정의와 호출 분리를 통해 얻는 장점 등

예시 깃헙: https://github.com/16Yongjin/tutoring-app/tree/main/src/api

- [clean-architecture-example-vue](https://github.com/andoshin11/clean-architecture-example-vue/tree/master/src/network)에서 찾은 코드를 발전시켰다.
- `APIRequest`, `APIResponse`, `APIError`와 `ApiClient`로 구성된다.

# 구성 방식

## 모든 요청은 `APIRequest`를 상속받는다.

```ts
interface APIResponse {}
```

## 모든 응답은 `APIResponse`를 상속받는다.

```ts
type APIRequest<R extends APIResponse> = {
  response: R // 응답 타입
  path: string // API 루트
  method: HTTPMethod // HTTP 메서드
  params?: any // 쿼리 패러미터
  data?: any // 바디
  baseURL?: string // 서버 호스트 주소
  headers?: Record<string, string> // 헤더
  parse?: (data: AxiosResponse<R>) => R // 응답 객체 파서, 보통 `data`
  convertBody?: (data: any) => any // 응답 바디 변환, 보통 `JSON.parse`
}
```

## `APIError`

- 서버 구성에 따라 다르다.

```ts
interface APIError {
  message: string
  status: number
  errors: Record<string, string>
  raw: AxiosError
  response?: AxiosResponse
}
```

## `APIClient`는 `APIRequest`를 받아서 `APIResponse` 또는 `APIError`를 반환한다.

- 의존성 역전을 통해, `axois`나 `fetch` 등 아무거나 사용할 수 있다.

&nbsp;

# API 정의 방법

- 리뷰를 생성하는 API를 예시로 들었다.

## 1. 엔티티를 정의한다.

- 리뷰 엔티티를 정의한다. 서버 측 엔티티와 타입이 같다.

```ts
type Review = {
  id: number
  text: string
  rating: number
}
```

## 2. 요청을 정의한다.

- 리뷰를 생성에 필요한 데이터 타입이다.

```ts
type CreateReviewRequest = {
  userId: number
  tutorId: number
  rating: number
  text: string
}
```

## 3. 응답을 정의한다.

리뷰를 생성하면 리뷰를 반환한다.

```ts
type CreateReviewResponse = Review
```

## 4. API를 정의한다.

- API의 경로와 입력 데이터, HTTP 메서드를 정의한다.
- API에 요청 데이터를 넣어서 API를 생성할 수 있다.

```ts
class CreateReview<R extends CreateReviewResponse> implements APIRequest<R> {
  method = HTTPMethod.POST
  response!: R
  auth = true
  path = '/reviews/'
  constructor(public data: CreateReviewRequest) {}
}
```

## 5. API를 호출할 수 있는 함수를 생성한다.

```ts
const createReview = APIClient.of(ReviewAPI.CreateReview)
```

- `of()` 메서드가 API를 해석해서 호출 함수를 만든다.
- 호출 함수는 API 생성자를 인자로 받아 API 응답을 반환한다.
- 아래 함수는 리뷰 생성 인자를 받아서, 서버에 리뷰 생성 요청을 보내고, 리뷰를 반환한다.

![image](https://user-images.githubusercontent.com/22253556/132954849-573388d6-fe6d-49d1-bfc5-0d4f772cc4a7.png)

# [`APIClient`](https://github.com/16Yongjin/tutoring-app/blob/main/src/api/apiClient.ts)

- `APIClient`는 자기 자신을 싱글턴으로 갖고 `request` 스태틱 메서드로 서버 요청을 보낼 수 있다.
- `toCallable` 메서드는 API를 받아 API 호출 함수를 간편하게 만들어준다.
  - 타입 정의하는데만 하루가 걸렸다.

```ts
type Constructor<T> = new (...args: any[]) => T

type ResponseType<T> = T extends APIRequest<infer T> ? T : never

class APIClient {
  // API Client Singleton
  static shared = new APIClient()

  static request<U extends APIResponse>(request: APIRequest<U>): Promise<U> {
    return APIClient.shared.request(request)
  }

  /** API를 받아서 호출할 수 있는 함수로 변환합니다. */
  static toCallable<
    T extends Constructor<any>,
    U extends InstanceType<T>,
    R extends ResponseType<U> & APIError
  >(api: T) {
    return (...args: ConstructorParameters<T>) =>
      APIClient.request<R>(new api(...args))
  }

  /** `toCallable`의 alias */
  static of = APIClient.toCallable

  request<U extends APIResponse>(request: APIRequest<U>): Promise<U> {
    return axios.request({
      /** 유연한 axios 호출 코드, APIReqest 인터페이스에 의존 */
    })
  }
}
```

- `toCallable`의 별칭인 `of` 함수는 아래와 같이 적어야 하는 코드를 짧게 바꿔준다.

```ts
// 이런 긴 코드를
const createReview = (data: CreateReview) =>
  APIClient.request(new CreateReview(data))

// 이렇게 짧게 바꿔준다.
const createReview = APIClient.of(ReviewAPI.CreateReview)
```

## `request` 메서드 구현

- API 정의에 따라 서버에 요청을 보낸다.
- 최대한 유연하게 작성해서 많은 요구사항을 처리할 수 있게 한다.

```ts
class APIClient {
  baseURL = API_URL // API Endpoint

  timeout = 20 * 1000 // 타임 아웃

  request<U extends APIResponse>(request: APIRequest<U>): Promise<U> {
    return new Promise<U>((resolve, reject) => {
      axios
        .request({
          url: request.path,
          method: request.method,
          params: request.params,
          data: (request.convertBody || this.convertBody)(request.data),
          timeout: this.timeout,
          baseURL: request.baseURL || this.baseURL,
          headers: this.createHeaders(request),
          responseType: 'json',
        })
        .then((data: AxiosResponse<U>) => {
          const response = request.parse
            ? request.parse(data)
            : this.parse<U>(data)
          resolve(response)
        })
        .catch((err) => {
          const apiError = this.normalizeError(err)
          this.errorMiddleware(apiError)
          reject(apiError)
        })
    })
  }

  // 응답 바디 변환 함수, 케이스 변환(ex, 스네이크 -> 카멜) 기능이 들어가도 됨
  private convertBody = JSON.stringify

  private parse<U extends APIResponse>(data: AxiosResponse<U>): U {
    return data.data
  }

  private errorMiddleware(error: APIError): void {
    if (error.status === 401) // 인증 오류 발생 시 로그인 페이지로 쫓아냄
  }

  // Axios 에러를  APIError 변환
  private normalizeError(error: AxiosError): APIError {
    return {
      status: error.response?.status!,
      message: error.response?.data?.message || error.message,
      errors: error.response?.data?.errors,
      raw: error,
      response: error.response,
    }
  }

  // 헤더 생성
  private createHeaders<U extends APIResponse>(request: APIRequest<U>): any {
    // 인증 토큰 삽입
    // POST, PUT인 경우 Content-Type을 `application/json`로 설정
  }
}
```

&nbsp;

# 장점

## 코드 중복을 줄일 수 있다.

- API 정의와 호출을 분리한다.
- API가 클래스로 정의되는데, 상속을 통해 정의를 재활용 할 수 있어서 코드 중복을 줄일 수 있다.

### 리뷰 가져오기 코드 중복 줄이기

- 리뷰 가져오기는 요구 사항에 따라 일반 리뷰, 추천 리뷰, 모든 리뷰 목록을 가져온다.
- 요청과 응답은 같고, API 경로만 다르다.
- 리뷰 가져오기를 하나 정의하고, 상속해서 경로만 바꿔서 재활용할 수 있다.

```ts
export class GetReviews implements APIRequest<Review[]> {
  method = HTTPMethod.GET
  response!: Review[]
  auth = true
  path = '/reviews/'
}
export class GetFeaturedReviews extends GetReviews {
  path = '/reviews/featured'
}

export class GetAdminFeaturedReviews extends GetReviews {
  path = '/reviews/featured/admin'
}
```
