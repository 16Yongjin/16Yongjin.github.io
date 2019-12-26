---
id: 124
title: matlab으로 Hough 직선 찾기
date: 2017-04-17T02:05:23+09:00
author: yongjinsite
categories:
  - Computer Vision
tags:
  - Hough
  - MatLab
---

Udacity의 Intoduction to Computer Vision에서 퍼옴.

<img class="alignnone size-full wp-image-126" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/brazil.png" alt="Brazil.png" width="512" height="512" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/brazil.png 512w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/brazil-150x150.png 150w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/brazil-300x300.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/brazil-85x85.png 85w" sizes="(max-width: 512px) 100vw, 512px" /> 

이렇게 생긴 이미지에서 선을 검출하기

img = imread(&#8216;Brazil.png&#8217;);

이미지를 불러와서

g = rgb2gray(img);

흑백사진으로 만든 다음에

edge = edge(g, &#8216;canny&#8217;);

모서리들을 뽑아낸다.

<img class="alignnone size-full wp-image-132" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/2.png" alt="2.png" width="746" height="650" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/2.png 746w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/2-300x261.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/2-344x300.png 344w" sizes="(max-width: 746px) 100vw, 746px" /> 

이제

모서리 점들을 hough 공간에다가 배치시킴

예를 들어 점 x0, y0이 있으면

이를 y0 = m*x0 + b 로 표현할 수 있는데

위 매개변수 인 m과 b로 된 2차원 공간으로 점 x0, y0을 옮길 수 있음.

즉 한 점이 나타낼 수 있는 모든 직선을 표현함

<img class="alignnone size-full wp-image-150" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24.png" alt="스크린샷 2017-04-16 오후 8.19.24.png" width="2560" height="1600" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24.png 2560w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24-300x188.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24-768x480.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24-1024x640.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24-1000x625.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-19-24-480x300.png 480w" sizes="(max-width: 2560px) 100vw, 2560px" /> 

Hough space에서 겹치는 부분이 각 점의 공통 직선을 나타냄

근데 공통 직선이 수직이면 m이 막 무한으로 가버려서 계산하는데 컴퓨터가 힘듦.

그래서 Hough 공간 구할 때 다른 방식을 씀

<img class="alignnone size-full wp-image-164" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40.png" alt="스크린샷 2017-04-16 오후 8.27.40.png" width="2560" height="1600" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40.png 2560w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40-300x188.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40-768x480.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40-1024x640.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40-1000x625.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/ec8aa4ed81aceba6b0ec83b7-2017-04-16-ec98a4ed9b84-8-27-40-480x300.png 480w" sizes="(max-width: 2560px) 100vw, 2560px" /> 

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

<img style="max-width:100%;" src="https://i.stack.imgur.com/Wg7IU.png" /> 

여기서

<img class="alignnone size-full wp-image-196" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2.png" alt="hough.png" width="1600" height="1200" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2.png 1600w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2-300x225.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2-768x576.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2-1024x768.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2-1000x750.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/hough2-400x300.png 400w" sizes="(max-width: 1600px) 100vw, 1600px" /> 

(문송합니다.)

뭐 이렇게 된다.

theta와 원점과 직선 사이의 거리만으로 그 직선을 나타낼 수 있다는 것을 알게됐다.

theta는 0~π 나 0~2π이고, d는 위 브라질 국기에 경우 512 \* (2\**0.5) 이하이므로 표현하기 한결 쉽다.

theta개수*d개수 배열 H를 만들어서

각 모서리(edge)마다 theta가 0~180일 때의 d를 구하고 배열 H[theta, d]+=1씩 해주면

공통 직선의 개수가 검출된다.

여기서 높은 값들만 뽑아내면 직선이 검출됨

[accum theta rho] = hough(edge);

theta는 theta 그대로이고, rho는 d임

accum은 겹치는 값이 들어있는 배열 H.

그래서 이 값들을 표로 나타내고

figure, imagesc(accum, &#8216;X&#8217;, theta, &#8216;Y&#8217;, rho), title(&#8216;Hough accumulator&#8217;);

큰 값들, 여기선 직선이 100개 이상 겹친 것들을 뽑아낸 뒤

peaks = houghpeaks(accum, 100);

표로 나타내면

hold on; plot(theta(peaks(:,2)), rho(peaks(:, 1)), &#8216;rs&#8217;); hold off;

<img class="alignnone size-full wp-image-224" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1.png" alt="1.png" width="1120" height="840" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1.png 1120w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1-300x225.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1-768x576.png 768w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1-1024x768.png 1024w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1-1000x750.png 1000w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/1-400x300.png 400w" sizes="(max-width: 1120px) 100vw, 1120px" /> 

여기의 빨간 점들을 원본 그림의 직선으로 나타내면

line_segs = houghlines(edge, theta, rho, peaks);

figure, imshow(img), title(&#8216;Line segments&#8217;);

<img class="alignnone size-full wp-image-230" src="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/3.png" alt="3.png" width="746" height="650" srcset="https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/3.png 746w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/3-300x261.png 300w, https://raw.githubusercontent.com/16Yongjin/16Yongjin.github.io/master/wp-content/uploads/2017/04/3-344x300.png 344w" sizes="(max-width: 746px) 100vw, 746px" /> 

임계점을 너무 높게 잡아서 안쪽 직선이 안 잡힌것 같지만 여튼 이렇게 된다.