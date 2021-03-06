---
id: 850
title: Redux 기초
date: 2019-04-21T15:14:32+09:00
author: yongjin0802
layout: revision
guid: https://yongj.in/2019/04/21/562-revision-v1/
permalink: /2019/04/21/562-revision-v1/
---
<!-- HTML generated using hilite.me -->

<div style="background:#f8f8f8;overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;">
  <pre style="margin:0;line-height:125%;"><span style="color:#008000;font-weight:bold;">const</span> reducer <span style="color:#666666;">=</span> (state <span style="color:#666666;">=</span> [], action) <span style="color:#666666;">=&gt;</span> {
  <span style="color:#008000;font-weight:bold;">switch</span> (action.type){
    <span style="color:#008000;font-weight:bold;">case</span> <span style="color:#ba2121;">'split_string'</span><span style="color:#666666;">:</span>
      <span style="color:#008000;font-weight:bold;">return</span> action.payload.split(<span style="color:#ba2121;">''</span>);
      
    <span style="color:#008000;font-weight:bold;">case</span> <span style="color:#ba2121;">'add_character'</span><span style="color:#666666;">:</span>
      <span style="color:#008000;font-weight:bold;">return</span> [...state, action.payload]
      
      <span style="color:#008000;font-weight:bold;">default</span><span style="color:#666666;">:</span>
      <span style="color:#008000;font-weight:bold;">return</span> state   
  }
  
  
};
<span style="color:#008000;font-weight:bold;">const</span> store <span style="color:#666666;">=</span> Redux.createStore(reducer);

store.getState() <span style="color:#408080;font-style:italic;">// []</span>

<span style="color:#008000;font-weight:bold;">const</span> action <span style="color:#666666;">=</span> { 
  type<span style="color:#666666;">:</span> <span style="color:#ba2121;">'split_string'</span>,
  payload<span style="color:#666666;">:</span> <span style="color:#ba2121;">'asdf'</span> 
};

store.dispatch(action);
store.getState() <span style="color:#408080;font-style:italic;">// ["a","s","d","f"]</span>

<span style="color:#008000;font-weight:bold;">const</span> action2 <span style="color:#666666;">=</span> {
  type<span style="color:#666666;">:</span> <span style="color:#ba2121;">'add_character'</span>,
  payload<span style="color:#666666;">:</span> <span style="color:#ba2121;">'a'</span>
}

store.dispatch(action2)
store.getState() <span style="color:#408080;font-style:italic;">// ["a","s","d","f","a"]</span>
</pre>
</div>

&nbsp;