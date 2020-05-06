---
layout: post
title: "欢迎来到CicadaPlayer"
data: 2020-05-06 16:35:10 +0800
categories: jekyll update
---
CicadaPlayer官方发布地址

[https://github.com/alibaba/CicadaPlayer](https://github.com/alibaba/CicadaPlayer)


CicadaPlayer是一个跨平台的多媒体播放器，目前支持Android， iOS ，Mac， Linux，Windows和webAssembly平台，它是由[阿里云播放SDK](https://help.aliyun.com/document_detail/125579.html?spm=a2c4g.11186623.6.1070.13794c07tqHY4M)的播放器核心部分代码重构而来，未来阿里云播放SDK发布的新版本5.x开始将直接使用CicadaPlayer作为其播放器核心，目前5.1版本已经开始灰度发布，不久将正式替换目前的4.7.4版本。

下面就来简单介绍下该项目

## 1. CicadaPlayer的目标

1.  降低视频App开发难度，使用宽松的MIT license，提供简单易用的sdk接口，并提供比较丰富的场景demo。
2.  做一款跨平台的播放器，不限于目前支持的平台，未来还会支持更多平台。
3.  将插件化和可定制化设计贯穿整个架构的设计，开发者可以只编译自己想要的功能，不但播放器本身的功能可以定制和裁剪，其中的ffmpeg等开源库也可以定制裁剪；并且开发者可以通过开发自己的插件扩展或者替换现有的插件，开发的插件不会受到任何限制，可以用于商业目的。
4.  国际化，向国际标准靠拢，逐步支持国际流行的协议，codec等。

## 2. CicadaPlayer的特点

### 2.1 现代流媒体的支持

从十几年前苹果发布http live streaming到现在，网络流媒体发生了一些变化，向码率自适应，多语言，多字幕的方向靠拢，大大提高了网络视频的观看体验，可是目前一些历史比较久的跨平台开源多媒体项目并没有很好的支持这种特性，如果ffmpeg中只能比较简单的播放hls流，在4.2版本才加入dash的支持，并且也无法支持多码率等特性，那么那些直接使用ffmpeg作为demuxer的播放器也就无法很好的支持这些特性。CicadaPlayer通过自研方式支持了目前国内流行的HLS协议的多码率，多语言，多字幕的播放，目前可以比较完善的实现这些特性，并且多码率切换已经实现无缝切换。dash的支持也在计划之内，wildwine drm也会很快支持。

### 2.2 友好的跨平台解决方案

CicadaPlayer诞生的时候就考虑了跨平台开发的问题，目前做到了下载一套代码，可以完成所有平台的编译，你不必再专门为某个平台单独clone任何代码，比如在Android的开发环境修改一个bug或者开发一个功能，你修改了代码，担心在其他平台编译不过，或者有功能问题，那么这时候你直接打开其他平台的IDE编译运行就可以了，不需要手动merge你的改动到其他平台再测试。

CicadaPlayer使用了CMake作为编译系统，CMake可以生成目前绝大部分IDE的工程，你没必要为自己不熟悉XCode或者vs的工程配置而烦恼，你熟悉CMake就够了，由于使用统一的CMake工程文件，不管你在哪个平台开发，头文件和库等的路径的设置都是一致的，你不必担心因为不同编译系统里面设置的头文件或者路径不一样，导致include的头文件在这个平台可以编译过，换个平台就编译不过了的问题，况且维护多个编译系统的这些路径都一致，本身就是很烦恼的事情。

CicadaPlayer还在本机开发环境中提供了command line 程序，可以用支持CMake的跨平台IDE(如clion)，畅游各个平台的开发，不必去单独熟悉vs 或者xcode之类的东西，甚至在Linux平台上都能得到和Mac Windows一样的体验。

播放器中只有硬解码和渲染个别模块可能和平台相关，其他绝大部分的功能模块都可以是跨平台的，所以当你在开发一个核平台无关的功能时，完全可以在本机环境下开发，并可利用现有的单元测试框架运行和调试。比如你开发一个网络协议时，你没必要使用AndroidStudio去连接一个手机，再把某些代码写死去测试你刚刚写的代码，而是写一个简单的单元测试文件直接在开发机环境就跑了，debug，dump数据之类都会变得超级简单，并且这个单元测试代码也不会白写，以后每次修改代码后都可以再跑这个单元测试。

### 2.3 稳定性保证

对于阿里云来说，稳定压倒一切。CicadaPlayer在稳定性方面做了如下工作：

#### 2.3.1 单元测试和覆盖率

单元测试我认为对于一个软件来说是至关重要的，尤其对于其稳定性，是一切的基石，目前CicadaPlayer中对于每个独立的模块都有其相关的单元测试代码，整个播放器也有单元测试代码，支持[覆盖率统计](https://codecov.io/gh/alibaba/CicadaPlayer/branch/develop)，目前整体在70%左右。

cmdline的CicadaPlayer还支持从网络发消息进行测试，你可以写个脚本或者利用现有脚本进行你自己想要测试的流程，或者自动疯狂测试。

#### 2.3.2 持续集成

目前CicadaPlayer的github项目已经和著名的持续集成工具Travis和覆盖率统计工具codecov完成了对接，每次提交代码都会自动触发Travis自动编译->单元测试->覆盖率统计->结果回传的逻辑，这个流程中任何环节出问题都能马上发现，并且单元测试的过程中开启了clang的AddressSanitizer工具，在发现问题的时候会崩溃，保证每次提交的质量，并且目前Travis我们选择的是Linux平台，Linux下的Address Sanitizer是可以发现内存泄漏的。

#### 2.3.3 clang编译器中的Sanitizer工具的使用

目前所有平台的编译都使用clang编译器（引用的开源库编译除外），目前支持使用AddressSanitizer， ThreadSanitizer， MemorySanitizer(Linux下AddressSanitizer包含)，UndefinedBehaviorSanitizer，每次发版前都使用单元测试或者cmdline tool跑这些工具（AddressSanitizer 每次提交都跑），及时修改掉相关问题。

#### 2.3.4 Coverity Scan工具支持

[Coverity Scan](https://scan.coverity.com/projects/alibaba-cicadaplayer)也已经被集成，并且有单独的分支coverity_scan，每次发版前可以触发扫描，及时改掉相关问题

## 3. 未来规划

CicadaPlayer将会一直随着阿里云官网的播放器SDK更新，提供无限期的更新支持，已经支持的feature可以参见[项目主页](https://github.com/alibaba/CicadaPlayer#features)

未来将加入DASH DRM HDR 等支持，完善字幕的支持，还将提供一些智能ai插件，如自动字幕翻译，自动语言识别等。更欢迎大家PR。

## 4. 联系

可进入CicadaPlayer官方钉钉群，扫二维码或者点击二维码图片，群里会不定时分享一些使用和代码原理的视频，并且可以回看。

[![](https://oscimg.oschina.net/oscnet/up-230fc6ed24bee5246a6931b923b0324ad89.png)](https://h5.dingtalk.com/invite-page/index.html?bizSource=____source____&corpId=ding42c495ce0dcfdb7f35c2f4657eb6378f&inviterUid=B8D63ADF200A8E9DFF4BBDCA828801C7&encodeDeptId=FE36B0936DFD1AC591E7FE61FE0552A6)
