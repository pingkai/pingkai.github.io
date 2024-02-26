---
layout: post
title: "CicadaPlayer项目简介视频"
data: 2020-05-07 16:35:10 +0800
categories: jekyll update
---
# 01.CicadaPlayer项目简介-莫企
<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY2NDc3OTMwNA=="  frameborder="0" scrolling="no" allowfullscreen></iframe>

**关于默认分支的说明是不对的，现在默认分支以改成master**

## 自我介绍

1. 个人简单经历
2. 在项目中主要工作

## github页面介绍

1. 项目背景
2. license
3. 语言
4. 图标
5. README
6. wiki
7. 目前状况
8. pullrequest

---

# 02.CicadaPlayer Travis CI及单元测试初探
<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY2NDc4NjU2MA==" frameborder="0" allowfullscreen></iframe>

1. 持续集成
2. 代码覆盖率
3. pull request检查
4. 内存检查
5. IDE简介
6. Debug ffmpeg debug
7. Travis单元测试的流程
8. 项目的入手点

---

# 03. CicadaPlayer DataSource以及原型模式

<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY2NDc5OTA2NA==" frameborder="0" allowfullscreen></iframe>

1. 使用原型模式的初衷和plugin
1. DataSource的原型模式的注册和创建
2. 其他组件的原型模式的创建简介
3. DataSource接口介绍
4. http DataSource的实现
5. 其他DataSource的实现
6. BiDataSource
7. **更正原型模式代码说明（最后两分钟）**

---
# 04.Active Object模式和ActiveDecoder的应用

<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY2OTYyNTE4NA==" frameborder="0" allowfullscreen></iframe>
1. 主动对象简单介绍
2. 用播放器实现seek preview举例说明选择主动对象的想法
2. 播放器编排层线程模型简介（简单方案，timedEventQueue）
3. ActiveDecoder介绍
4. demuxer和render 主动对象介绍

[active object 说明](https://www.dre.vanderbilt.edu/~schmidt/PDF/Active-Objects.pdf)

---
# 05.基本媒体数据类型及其内存管理
<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY2OTY1MTA0NA==" frameborder="0" allowfullscreen></iframe>
1. 数据和meta分离的结构
2. clone方法
3. AVAFPacket和AVAFFrame的实现
4. 其他硬解码frame的实现
5. subTitlePacket 已经不再使用。
6. unique_ptr和shared_ptr的选择。

     shared_ptr
               优点:简单，通用，可以共享
               缺点:数据安全，滥用，传染性/(不可转换性)
              
     unique_ptr
               优点：安全，自由，无传染性
               缺点：使用稍复杂，无拷贝构造，通用性稍差，不可共享
                
7. 数据在模块间的传递

---

# 06.CicadaPlayer中对ffmpeg的使用(1)

<iframe height="498" width="510" src="https://player.youku.com/embed/XNDY2OTY1OTAzMg==" frameborder="0" allowfullscreen></iframe>
1. DataSource ffmpegDataSource
2. demuxer avFormatDemuxer avFormatSubtitleDemuxer
3. bsf AVBSF AFAVBSF

---

# 07.CicadaPlayer中对ffmpeg的使用(2)
1. muxer
2. decoder avcodecDecoder
3. ffmpegAudioFilter
4. 其他utils aes md5

