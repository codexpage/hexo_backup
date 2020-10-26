---
title: Example
date: 2018-10-02 20:42:34
tags:
---
{% raw %}
<canvas id="myCanvas" width="" height=""></canvas>		
<script type="text/javascript">
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);
ctx.stroke();		
</script>
{% endraw %}




<!-- 两种插入图片的方式 -->
<!-- {% img [test] /images/diluvion-cover.png '"title" "atl"' %}
![](/images/diluvion-cover.png) -->

<!-- <iframe> 不会被解析，但是<script>会被解析成text 需要加 raw标签-->
<!-- <iframe frameborder="0" scrolling="no" src="index2.html" width="100%" height="500px"></iframe> -->


