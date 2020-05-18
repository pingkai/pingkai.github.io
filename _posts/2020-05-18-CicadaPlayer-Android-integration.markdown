---
layout: post
title: "Android使用系列"
data: 2020-05-18 11:35:10 +0800
categories: jekyll update
---
# 01.CicadaPlayer在Android中的集成
<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY3Njg1MzE3Ng=="  frameborder="0" scrolling="no" allowfullscreen></iframe>

**视频中遗漏了一点：在surfaceDestroyed()方法中，需要调用setSurface(null)。TextureView同样。**

```java
@Override
public void surfaceDestroyed(SurfaceHolder holder) {
     mCicadaPlayer.setSurface(null);
}
```
