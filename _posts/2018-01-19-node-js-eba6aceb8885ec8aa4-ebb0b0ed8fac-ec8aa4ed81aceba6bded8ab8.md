---
id: 671
title: Node.js 리눅스 배포 스크립트
date: 2018-01-19T21:58:25+09:00
author: yongjinsite

guid: https://yongjinsite.wordpress.com/?p=671
permalink: '/2018/01/19/node-js-%eb%a6%ac%eb%88%85%ec%8a%a4-%eb%b0%b0%ed%8f%ac-%ec%8a%a4%ed%81%ac%eb%a6%bd%ed%8a%b8/'
timeline_notification:
  - "1516366708"
categories:
  - Development
tags:
  - Linux
  - Node.js
---
서버는 sudo npm i -g pm2 실행 후  
[code language=&#8221;shell&#8221;]  
\# 맥에서  
$ vim deploy.sh  
```bash
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

ESC, :wq, ENTER

$ chmod +x deploy.sh  
$ ./deploy.sh  
```


<div>
</div>

> <div>
>   참고
> </div>
> 
> <div>
>   https://www.youtube.com/watch?v=AQClj-lLqRs
> </div>

 