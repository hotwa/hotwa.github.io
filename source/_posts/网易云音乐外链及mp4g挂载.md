---

title: 网易云音乐外链及mp3挂载
categories: 部署
date: 2021-02-24 16:16:15
tags:
 - hexo
 - html
 - markdown
---



# markdown挂载网易云音乐

## 非自动播放效果

### 使用video标签

```html5
<video width="480" height="400" controls>     <source src="http://music.163.com/song/media/outer/url?id=472045959.mp3" type="audio/mp3"> </video>
```

> 将分享id http://music.163.com/song/media/outer/url?id=472045959.mp3 修改即可
>
> 备选链接（使用iframe标签自动播放）：http://link.hhtjim.com/163/472045959.mp3

#### 效果如下

##### type="audio/mp3"

<video width="720" height="50" controls>
    <source src="http://music.163.com/song/media/outer/url?id=472045959.mp3" type="audio/mp3">
</video>

##### type=type="video/mp4"

<video width="720" height="50" controls>
    <source src="http://music.163.com/song/media/outer/url?id=472045959.mp3" type="video/mp4">
</video>



### 使用audio标签

```html5
<audio controls height="100" width="100">
    <source src="http://music.163.com/song/media/outer/url?id=472045959.mp3" type="audio/mpeg">
    <embed height="50" width="100" src="http://music.163.com/song/media/outer/url?id=472045959.mp3">
</audio>
```

#### 效果如下

<audio controls height="100" width="100">
    <source src="http://music.163.com/song/media/outer/url?id=472045959.mp3" type="audio/mpeg">
    <embed height="50" width="100" src="http://music.163.com/song/media/outer/url?id=472045959.mp3">
</audio>

## 自动播放效果

### 使用iframe标签

```html5
<iframe name="music" src="http://link.hhtjim.com/163/472045959.mp3" marginwidth="0px" marginheight="0px" width=100% height="80px" frameborder=1 scrolling="yes">
</iframe>
```

# markdown挂载视频

```html5
<video width="480" height="400" controls>
    <source src="http://pic.jmsu.top/sunnerd.mp4" type="video/mp4">
</video>
```

```html5
<iframe height=498 width=510 src="https://v5-dy-f.ixigua.com/6f72a74d86b160e7c66db5ba75db769a/6036665c/video/tos/cn/tos-cn-ve-15/1cb550e737244e5ebbc66b762be742dd/" frameborder=0 allowfullscreen></iframe>
```

```html5
<video width="480" height="400" controls>
    <source src="https://v5-dy-f.ixigua.com/6f72a74d86b160e7c66db5ba75db769a/6036665c/video/tos/cn/tos-cn-ve-15/1cb550e737244e5ebbc66b762be742dd/" type="video/mp4">
</video>
```

#### 效果如下(markdown正常显示)

<video width="480" height="400" controls>
    <source src="http://pic.jmsu.top/sunnerd.mp4" type="video/mp4">
</video>


<a rel="noreferrer" target="_blank" src="http://v5-dy-f.ixigua.com/6f72a74d86b160e7c66db5ba75db769a/6036665c/video/tos/cn/tos-cn-ve-15/1cb550e737244e5ebbc66b762be742dd/"></a>



