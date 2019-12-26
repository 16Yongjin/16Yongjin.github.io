---
id: 687
title: Vue.js + Firebase Cloud Message (FCM) 설정
date: 2018-03-04T01:44:21+09:00
author: yongjinsite
categories:
  - Tutorials
tags:
  - Firebase
  - Vue.js

---

Vue.js 프로젝트에 FCM 추가하기

```javascript
import Vue from 'vue'
import { initializeApp, messaging } from 'firebase'

new Vue({
  el: '#app',
  created () {
    initializeApp({
      messagingSenderId: SENDER_ID
    })

    const message = messaging()
    navigator.serviceWorker.register('/static/firebase-messaging-sw.js')
      .then((registration) => {
        console.log('serviceWorker registration')
        return message.useServiceWorker(registration)
      }).then(() => {
        return message.requestPermission()
      })
      .then(() => {
        console.log('Notification permission granted.')
        return message.getToken()
      })
      .then(token => {
        console.log(token)
      })
      .catch(err => {
        console.log('Unable to get permission to notify.', err)
      })

    message.onMessage(({ notification }) => {
      const { title, body } = notification
      console.log('onMessage: ', `${title} ${body}`)
      alert(`${title} ${body}`)
    })
  }
})
```
