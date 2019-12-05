---
id: 816
title: Node.js 리눅스 배포 스크립트
date: 2019-04-21T15:03:40+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/671-revision-v1/
permalink: /2019/04/21/671-revision-v1/
---
서버는 sudo npm i -g pm2 실행 후  
[code language=&#8221;shell&#8221;]  
\# 맥에서  
$ vim deploy.sh  
~~~~~  
#!/bin/bash  
APP_NAME=&#8217;앱이름&#8217;  
tar -czf $APP_NAME.tar.gz app.js package.json  
scp -i ~/.ssh/rsa $APP\_NAME.tar.gz user@server\_address:~  
rm $APP_NAME.tar.gz

ssh -i ~/.ssh/rsa user@server_address <<&#8216;ENDSSH&#8217;

APP_NAME=&#8217;앱이름&#8217;  
echo &#8216;stop&#8217; $APP_NAME  
pm2 stop $APP_NAME  
echo &#8216;remove&#8217; $APP_NAME  
rm -rf $APP_NAME  
mkdir $APP_NAME  
tar -xf $APP\_NAME.tar.gz -C $APP\_NAME  
rm $APP_NAME.tar.gz  
cd $APP_NAME  
npm install  
pm2 start app.js &#8211;name $APP_NAME

ENDSSH  
~~~~  
ESC, :wq, ENTER

$ chmod +x deploy.sh  
$ ./deploy.sh  
[/code]

<div>
</div>

> <div>
>   참고
> </div>
> 
> <div>
>   https://www.youtube.com/watch?v=AQClj-lLqRs
> </div>

 