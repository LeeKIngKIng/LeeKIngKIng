---
title: 年终总结
date: 2018-01-16 10:18:49
tags: "summary"
---

{% asset_img pic1.gif %}

<!-- more -->

## 魂斗罗独立项目：
{% asset_img qrcode.png %}

该项目包含两个video和多个audio，通过多个交互按钮和css3动画进行衔接，中间还有一个寻找物品的小游戏交互。

### 音频播放
ios系统的微信中实现音频自动播放，只需加入以下代码：
```
var audioAutoPlay=function(id){
    var audio = document.getElementById(id);
    audio.play();
    document.addEventListener("WeixinJSBridgeReady", function () {
        audio.play();
    }, true);
}
audioAutoPlay('startBgm'); 
```
若想把音频放在setTimeout中延迟执行播放，由于ios系统的安全机制，则也得事先点击触发音频播放。因此需要在setTimeout前的某一个点击事件中播放音频然后立即暂停。


### H5视频交互
在iPhone下面，不需要全屏播放，可以在一个区域中播放,这样交互视频可以出现在普通图形对象的下面了，话不多说，直接上代码。
```
<!--html部分-->
<div class="videoPlayer">
  <video class="IIV" id="video" src="data/test.mp4" width="100%" autoplay="" x-webkit-airplay="true" webkit-playsinline="" playsinline=""></video>
</div>
```
```
//less部分
.IIV::-webkit-media-controls-play-button,
.IIV::-webkit-media-controls-start-playback-button {
  width: 0;
  opacity: 0;
  pointer-events: none;
}

.videoPlayer{
  z-index: 1;
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 0;
  &.show{
    width: 100%;
    height: 100%;
  }
  video{
    position: absolute;
    top: 50%;
    left: 50%;
    .transform(translate(-50%, -50%));
    &.no{
      background:transparent;
    }
  }
}
```
如果想支持ios9，则需另外引入[iphone-inline-video.min.js](https://www.npmjs.com/package/iphone-inline-video)（自行下载），添加js代码：
```
var inBrowser = typeof window !== 'undefined';
var UA = inBrowser && window.navigator.userAgent.toLowerCase();
var isIOS = UA && /iphone|ipad|ipod|ios/.test(UA);
$video = $("#video")[0]
if (isIOS) {
    enableInlineVideo($video);
}
```

由于video的poster属性有兼容性问题，视频封面需改成一div覆盖在上面，利用video的currenttime属性判断视频是否开始。
代码如下：
```
var curTime,isEnd1=true;
$('#video').on('timeupdate',function(){
    curTime=$video.currentTime;
    if(curTime>0){
        $('.poster').css('background','none');
    }
    if(curTime>9.2){
        $('.poster').hide()
        $('.btn_goIn').show().addClass('fadeIn');
        if(isEnd1){
            PTTSendClick('btn','video1End','视频1结束');
            isEnd1=false;
        }
        $video.pause();
    }
})
```
还能利用currenttime控制交互按钮和css3动画出现的时机，值得注意的是android的currenttime相比ios会有误差，需要另外调试视频以实际数据为准。

最后一个视频由于需要在某一时间段内循环播放，而ios9是不支持视频静音的，所以需要把音频提取出来放进一个audio标签中跟视频同步播放。

### 小游戏交互
开始是使用陀螺仪控制画面左右移动的，会更有趣味。后来客户需要更简单的交互，就改成滑动了。
```
var width=parseInt($('.bg').width());
var distanceX=0;
var delta;

$('#main').on('touchstart',function(e){
    delta = e.targetTouches[0].pageX - distanceX;
});
var action=function(e){
    var newDistanceX =  e.targetTouches[0].pageX - delta;
    //判断滑动的方向以及背景画面的边界
    if((newDistanceX>0 && newDistanceX<width/2-20) || (newDistanceX<0&& newDistanceX>-width/2/3*2+20)){
    	//记录上次位移
        distanceX = newDistanceX;
    }
}
$('#main').on('touchmove',action)

var requestFrame = window.requestAnimationFrame ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame    ||
    window.oRequestAnimationFrame      ||
    window.msRequestAnimationFrame     ||
    function(callback) {
        window.setTimeout(callback, 1000 / 60);
    };
var step=function(){
    $('.bg').css('-webkit-transform','translate('+distanceX+'px,0)');
    animationFrameId=requestFrame(step);
    if(enough.length===5){
        $('#main').off('touchmove',action);
        cancelAnimationFrame(animationFrameId)
        $('.bg').css('-webkit-transform','translate(0,0)');
        $('.finalFrame').show();
    }
}
requestFrame(step);
```

## 过往项目中遇到的一些问题：
1.注意返回结果是字符串还是数值，减法运算可以正常运行，而加法就变成合并字符串了。
2.ios上的body的overflow：hidden无效，还是会滚动。解决方法是加上position：fixed，可是这个会造成页面跳到顶端。
3.移动嵌套直播使用iframe,用video需要m3u8格式。
4.网易组件galleryv2的slidesPerView设置个数与元素个数相等时会出现bug，元素个数会变成double。
5.元素display属性为none时，会导致swiper初始化出现问题。
6.宽高的rem值为奇数时有些机型可能会相差1像素导致缺了一边框。
7.$(document).on('click',function(){}) 在iphone上不触发事件。解决方法是给document元素添加css :cursor:pointer;或者改为touch事件。
8.注意ie7、8的性能问题，有时代码执行需设在setTimeout中。
9.position设置定位才能触发z-index。





