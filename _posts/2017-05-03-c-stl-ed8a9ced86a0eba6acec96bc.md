---
id: 299
title: C++ STL 튜토리얼
date: 2017-05-03T21:20:38+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=299
permalink: '/2017/05/03/c-stl-%ed%8a%9c%ed%86%a0%eb%a6%ac%ec%96%bc/'
categories:
  - Development
tags:
  - C++
  - Tutorial
---
<div>
  effective c++을 읽는데 공부 안한 c++ stl의 벡터와 반복자가 나왔다.
</div>

<div>
</div>

<div>
  그래서
</div>

<div>
  <a href="https://www.tutorialspoint.com/cplusplus/cpp_stl_tutorial.htm">https://www.tutorialspoint.com/cplusplus/cpp_stl_tutorial.htm</a>
</div>

<div>
  을 번역했다.
</div>

<div>
</div>

<div>
  C++ 의 Standard Template Library는 세 가지로 구성되어있음
</div>

<div>
</div>

<div>
  1. Containers : 객체 모여있는 거 관리하는 용임. 그 유명한 덱, 리스트, 벡터, 맵 등이 해당함
</div>

<div>
  2. 알고리즘 : 컨테이너에 사용함. 초기화, Sorting, 검색, 안에 들어있는 값 수정 등을 할 수 있음
</div>

<div>
  3. 반복자 Iterators : 컨테이너에 들어 있는 것을 훑어 볼 수 있음
</div>

<div>
</div>

<div>
  벡터 컨테이너 예제
</div>

<div>
</div>

<div>
  <p>
    [code language=&#8221;cpp&#8221;]<br /> #include <iostream><br /> #include <vector><br /> using namespace std;
  </p>
  
  <p>
    int main() {<br /> // 정수 보관하는 벡터 만들기<br /> vector vec;<br /> int i;
  </p>
  
  <p>
    // 벡터의 사이즈를 보여줌<br /> cout << "vector size = " << vec.size() << endl;
  </p>
  
  <p>
    // 벡터 안에 값을 뒤로 밀어 넣음<br /> for(i = 0; i < 5; i++){<br /> vec.push_back(i);<br /> }
  </p>
  
  <p>
    // 값이 들어간 벡터의 사이즈를 보여줌<br /> cout << "extended vector size = " << vec.size() << endl;
  </p>
  
  <p>
    // 벡터 안의 값에 접근함<br /> for(i = 0; i < 5; i++){<br /> cout << "value of vec [" << i << "] = " << vec[i] << endl;<br /> }
  </p>
  
  <p>
    // 반복자를 사용해서 벡터 안의 값에 접근함<br /> vector::iterator v = vec.begin();<br /> while( v != vec.end()) {<br /> cout << "value of v = " << *v << endl;<br /> v++;<br /> }
  </p>
  
  <p>
    return 0;<br /> }<br /> [/code]
  </p>
  
  <div>
  </div>
  
  <div>
    결과는 이러함
  </div>
  
  <div>
    <p>
      [code]vector size = 0<br /> extended vector size = 5<br /> value of vec [0] = 0<br /> value of vec [1] = 1<br /> value of vec [2] = 2<br /> value of vec [3] = 3<br /> value of vec [4] = 4<br /> value of v = 0<br /> value of v = 1<br /> value of v = 2<br /> value of v = 3<br /> value of v = 4<br /> [/code]
    </p>
  </div>
</div>

<div>
  C++ Standard Library는 두 개로 분류됨
</div>

<div>
</div>

<div>
  1. The Standard Function Library : C언어에서 온 건데, 어떤 클래스에도 속해있지 않고 일반적으로 사용할 수 있는 함수들이 들어있음
</div>

<div>
</div>

<div>
  또 이렇게 분류됨
</div>

<div>
  1) 입출력
</div>

<div>
  2) 문자, 문자열 다루기
</div>

<div>
  3) 수학 계산용
</div>

<div>
  4) 시간, 날짜, 지역
</div>

<div>
  5) 동적 할당
</div>

<div>
  6) Miscellaneous, 잡동사니, misc.
</div>

<div>
  7) 넓은 문자열 함수 ex) islower()
</div>

<div>
</div>

<div>
  2. The Object Oriented Class Library : 클래스랑 클래스와 관련된 함수들 모아둔 것
</div>

<div>
</div>

<div>
  1) 표준 C++ 입출력 클래스
</div>

<div>
  2) 문자열 클래스
</div>

<div>
  3) 숫자 클래스
</div>

<div>
  4) STL 컨테이너
</div>

<div>
  5) STL 알고리즘
</div>

<div>
  6) STL 함수 객체
</div>

<div>
  7) STL 반복자
</div>

<div>
  8) STL 할당자
</div>

<div>
  9) 지역화 라이브러리
</div>

<div>
  10) 오류 처리 클래스
</div>

<div>
  11) 기타 등등
</div>

<div>
</div>

<div>
  이러고 책 읽으라면서 책 추천해주면서 끝남 ㅡㅡ;
</div>

<div>
</div>

<div>
  std::vector<int>::iterator iter = vec.begin(); 에서
</div>

<div>
</div>

<div>
</div>

<div>
  const std::vector<int>::iterator iter = vec.begin(); 면
</div>

<div>
  iter가 가르키는, 벡터 안에 있는 요소는 변경할 수 있지만 (*iter)
</div>

<div>
  iter값 자체가 상수화되어서 변경 불가
</div>

<div>
</div>

<div>
  *iter 즉, 벡터 안에 있는 값을 상수화하기 위해서는
</div>

<div>
  std::vector<int>::const_iterator cIter = vec.begin(); 이렇게 해야함
</div>

<div>
</div>

<div>
  그러면 반복을 신나게 할 수 있는데 벡터의 값은 변경으로부터 보호함
</div>

<div>
</div>

<div>
</div>

<div>
</div>