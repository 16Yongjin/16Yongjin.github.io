---
id: 826
title: matlab으로 Hough 직선 찾기
date: 2019-04-21T15:05:41+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/124-revision-v1/
permalink: /2019/04/21/124-revision-v1/
---

Udacity의 Intoduction to Computer Vision에서 퍼옴.

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/brazil.png" alt="Brazil.png" />

이렇게 생긴 이미지에서 선을 검출하기

```
img = imread('Brazil.png');
```

이미지를 불러와서

```
g = rgb2gray(img);
```

흑백사진으로 만든 다음에

```
edge = edge(g, 'canny');
```

모서리들을 뽑아낸다.

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/2.png" />

이제

모서리 점들을 hough 공간에다가 배치시킴

예를 들어 점 `x0`, `y0`이 있으면

이를 `y0 = m * x0 + b` 로 표현할 수 있는데

위 매개변수 인 `m`과 `b`로 된 2차원 공간으로 점 `x0`, `y0`을 옮길 수 있음.

즉 한 점이 나타낼 수 있는 모든 직선을 표현함

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24.png"  />

Hough space에서 겹치는 부분이 각 점의 공통 직선을 나타냄

근데 공통 직선이 수직이면 m이 막 무한으로 가버려서 계산하는데 컴퓨터가 힘듦.

그래서 Hough 공간 구할 때 다른 방식을 씀

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40.png" />

공통 직선을 표현하기 위해

hough transform equation라는 걸 쓴다.

직선을 삼각함수를 사용해서 표현하는 것인데 왜 그렇게 되는지 알아내기 힘들었다.

> http://stackoverflow.com/questions/7613955/hough-transform-equation
>
> http://homepages.inf.ed.ac.uk/rbf/HIPR2/hough.htm
>
> http://kin.naver.com/qna/detail.nhn?d1id=11&dirId=1113&docId=248013600&qb=65GQIOygiO2OuCDso7zslrTsoYzsnYQg65WM&enc=utf8&section=kin&rank=1&search_sort=0&spq=0&pid=TnMgwwpySD8ssvdJCbhssssssiR-301489&sid=4H0ekjZUrdpXZ2aGt7qWWg%3D%3D
>
> 을 참고했다.

<img src="https://i.stack.imgur.com/Wg7IU.png" />

여기서

<img  src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2.png"  />

(문송합니다.)

뭐 이렇게 된다.

`theta`와 원점과 직선 사이의 거리만으로 그 직선을 나타낼 수 있다는 것을 알게됐다.

`theta`는 `0~π` 나 `0~2π`이고, `d`는 위 브라질 국기에 경우 `512 * (2**0.5)` 이하이므로 표현하기 한결 쉽다.

`theta 개수 * d 개수` 배열 H를 만들어서

각 모서리(edge)마다 `theta`가 0~180일 때의 `d`를 구하고 배열 `H[theta, d]+=1`씩 해주면

공통 직선의 개수가 검출된다.

여기서 높은 값들만 뽑아내면 직선이 검출됨

```
[accum theta rho] = hough(edge);
```

`theta`는 `theta` 그대로이고, `rho`는 `d`임

accum은 겹치는 값이 들어있는 배열 H.

그래서 이 값들을 표로 나타내고

```
figure, imagesc(accum, 'X', theta, 'Y', rho), title('Hough accumulator');
```

큰 값들, 여기선 직선이 100개 이상 겹친 것들을 뽑아낸 뒤

```
peaks = houghpeaks(accum, 100);
```

표로 나타내면

```
hold on; plot(theta(peaks(:,2)), rho(peaks(:, 1)), 'rs'); hold off;
```

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1.png"  />

여기의 빨간 점들을 원본 그림의 직선으로 나타내면

```
line_segs = houghlines(edge, theta, rho, peaks);

figure, imshow(img), title('Line segments');
```

<img src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/3.png"  />

임계점을 너무 높게 잡아서 안쪽 직선이 안 잡힌것 같지만 여튼 이렇게 된다.
