---
id: 843
title: Vue.js + Firebase Cloud Message (FCM) 설정
date: 2019-04-21T15:12:43+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/687-revision-v1/
permalink: /2019/04/21/687-revision-v1/
---
<pre style="background:#fff;color:#000;"><span style="color:#00f;font-weight:bold;">import</span> Vue from <span style="color:#036a07;">'vue'</span>
<span style="color:#00f;font-weight:bold;">import</span> { initializeApp, messaging } from <span style="color:#036a07;">'firebase'</span>

<span style="color:#00f;font-weight:bold;">new</span> <span style="text-decoration:underline;">Vue</span>({
  el: <span style="color:#036a07;">'#app'</span>,
  created () {
    initializeApp({
      messagingSenderId: SENDER_ID
    })

    <span style="color:#00f;font-weight:bold;">const</span> message <span style="color:#687687;">=</span> messaging()
    <span style="color:#6d79de;font-weight:bold;">navigator</span>.serviceWorker.register(<span style="color:#036a07;">'/static/firebase-messaging-sw.js'</span>)
      .then((registration) <span style="color:#687687;">=</span><span style="color:#687687;">&gt;</span> {
        <span style="text-decoration:underline;">console</span><span style="color:#3c4c72;font-weight:bold;">.log</span>(<span style="color:#036a07;">'serviceWorker registration'</span>)
        <span style="color:#00f;font-weight:bold;">return</span> message.useServiceWorker(registration)
      }).then(() <span style="color:#687687;">=</span><span style="color:#687687;">&gt;</span> {
        <span style="color:#00f;font-weight:bold;">return</span> message.requestPermission()
      })
      .then(() <span style="color:#687687;">=</span><span style="color:#687687;">&gt;</span> {
        <span style="text-decoration:underline;">console</span><span style="color:#3c4c72;font-weight:bold;">.log</span>(<span style="color:#036a07;">'Notification permission granted.'</span>)
        <span style="color:#00f;font-weight:bold;">return</span> message.getToken()
      })
      .then(token <span style="color:#687687;">=</span><span style="color:#687687;">&gt;</span> {
        <span style="text-decoration:underline;">console</span><span style="color:#3c4c72;font-weight:bold;">.log</span>(token)
      })
      .<span style="color:#00f;font-weight:bold;">catch</span>(err <span style="color:#687687;">=</span><span style="color:#687687;">&gt;</span> {
        <span style="text-decoration:underline;">console</span><span style="color:#3c4c72;font-weight:bold;">.log</span>(<span style="color:#036a07;">'Unable to get permission to notify.'</span>, err)
      })

    message.onMessage(({ notification }) <span style="color:#687687;">=</span><span style="color:#687687;">&gt;</span> {
      <span style="color:#00f;font-weight:bold;">const</span> { title, body } <span style="color:#687687;">=</span> notification
      <span style="text-decoration:underline;">console</span><span style="color:#3c4c72;font-weight:bold;">.log</span>(<span style="color:#036a07;">'onMessage: '</span>, `<span style="color:#687687;">$</span>{title} <span style="color:#687687;">$</span>{body}`)
      <span style="color:#3c4c72;font-weight:bold;">alert</span>(`<span style="color:#687687;">$</span>{title} <span style="color:#687687;">$</span>{body}`)
    })
  }
})
</pre>

&nbsp;