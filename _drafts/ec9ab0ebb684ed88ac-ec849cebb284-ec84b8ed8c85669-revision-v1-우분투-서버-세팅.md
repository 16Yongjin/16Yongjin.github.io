---
id: 846
title: 우분투 서버 세팅
date: 2019-04-21T15:13:23+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/669-revision-v1/
permalink: /2019/04/21/669-revision-v1/
---
1. 비밀번호 설정

<pre>$ sudo passwd root
  sudo: unable to resolve host XXXXXXXX-123
  Enter new UNIX password: 
  Retype new UNIX password: 
  passwd: password updated successfully
</pre>

2. sudo: unable to resolve host XXXXXXXX-123 메시지 없애기

<pre>$ sudo vim /etc/hostname # 호스트 이름 바꾸기

  $ sudo vi /etc/hosts 
  127.0.0.1 호스트_이름 # 호스트 추가하기

  $ sudo reboot # 재부팅
  또는
  $ sudo /etc/init.d/networking restart
  
</pre>

3. 계정 추가하기

<pre>$ sudo adduser [계정이름]
</pre>

4. ssh 설정

<pre># 맥에서
  $ ssh-keygen -t rsa # 암호키 생성
  $ scp ~/.ssh/rsa.pub user@server_address:rsa.pub # 공개키 서버로 옮기기

  # 서버에서
  $ mkdir ~/.ssh
  $ cat ~/rsa.pub &gt;&gt; ~/.ssh/authorized_keys

  $ ssh -i ~/rsa server_address # 이제 이렇게 해서 비밀번호 입력 없이 접속 가능

  # ssh 비밀번호 접속 막기
  
  $ vim /etc/ssh/sshd_config 에서

  ChallengeResponseAuthentication no
  PasswordAuthentication no
  UsePAM no 
  로 설정

  $ sudo /etc/init.d/ssh restart # 설정 적용
</pre>

5. Nginx 와 Node.js 설치

<pre>$ sudo apt-get install nginx
    
  $ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
  $ apt-get install nodejs
</pre>

<div>
</div>

> 참고
> 
> 2번
> 
> <blockquote class="wp-embedded-content" data-secret="RyKexUtlbm">
>   <p>
>     <a href="http://sarghis.com/blog/831/">우분투(Ubuntu) 호스트 이름 변경</a>
>   </p>
> </blockquote>
> 
>  
> 4번  
> https://opentutorials.org/module/432/3742  
> http://support.hostgator.com/articles/specialized-help/technical/how-to-disable-password-authentication-for-ssh  
> 5번  
> https://zetawiki.com/wiki/우분투\_node.js\_설치  
> https://twpower.github.io/linux/2017/04/08/39(Ubuntu에서-apt-get을-통해-nginx-설치하기-및-간단한-정리).html