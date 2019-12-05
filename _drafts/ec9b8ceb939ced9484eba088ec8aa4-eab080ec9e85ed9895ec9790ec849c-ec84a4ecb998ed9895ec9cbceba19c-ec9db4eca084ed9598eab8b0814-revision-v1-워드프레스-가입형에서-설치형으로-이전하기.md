---
id: 815
title: 워드프레스 가입형에서 설치형으로 이전하기
date: 2019-04-21T15:01:03+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/814-revision-v1/
permalink: /2019/04/21/814-revision-v1/
---
### 서버 세팅하기<figure class="wp-block-embed-wordpress wp-block-embed is-type-wp-embed is-provider-website-for-students">

<div class="wp-block-embed__wrapper">
  <blockquote class="wp-embedded-content" data-secret="wSTudjxBVZ">
    <a href="https://websiteforstudents.com/configure-wordpress-with-nginx-mariadb-php-7-1-and-varnish-proxy-on-ubuntu-16-04-lts/">Configure WordPress with Nginx, MariaDB, PHP 7.1 and Varnish Proxy on Ubuntu 16.04 LTS</a>
  </blockquote>
</div></figure> 

위 링크의 설명을 따라 nginx, mariaDB, php 7.1, wordpress를 서버에 세팅했다.

### 글 옮기기

[내 사이트 &#8211; 설정 &#8211; 아래쪽에 있는 내보내기 &#8211; 콘텐츠 내보내기]를 통해 내보낸 xml 파일을 새 사이트의 [도구 &#8211; 가져오기]에 업로드해서 모든 글을 옮겼다.

### HTTPS 적용

certbot으로 도메인에 인증서를 추가한다.

이미지까지 https를 적용하기 위해

<https://blog.wpbox.kr/changing-wordpress-site-url/>

위 링크의 설명을 따라 search replace db를 설치하고 실행 후 지운다.

그러면 모든 리소스를 https로 가져오게되어 브라우저에 초록색 자물쇠가 생긴다.