---
title: '开源翻译软件bob使用'
date: 2022-03-24 12:51:27
tags: [Mac软件]
published: true
hideInList: false
feature: /post-images/kai-fa-fan-yi-ruan-jian-bob-shi-yong.png
isTop: false
---


# 介绍

Bob 是一款 Mac 端翻译软件，支持**划词翻译**、**截图翻译**以及手动输入翻译。

- [x] 划词翻译
- [x] 截图翻译
- [x] 输入翻译
- [x] 翻译多开
- [x] 自定义插件
- [x] 自动识别语种
- [x] 驼峰拆分、蛇形拆分
- [x] AppleScript 调用
- [x] PopClip 调用

# 官网地址 [https://ripperhe.gitee.io/bob/#/](https://ripperhe.gitee.io/bob/#/)

# 安装

### 系统要求

| 版本 | 系统要求 |
| --- | --- |
| 0.1.0 - 0.4.0 | macOS 10.12+ |
| 0.5.0+ | macOS 10.13+ |

### Homebrew Cask 安装（技术人员使用）

```bash
brew install --cask bob
```

### 手动安装（普适）

| 渠道 | 建议 | 下载 |
| --- | --- | --- |
| 从 [GitHub release](https://github.com/ripperhe/Bob/releases) 下载 | 国外从这里下载更快 | [点此下载 ⬇](https://github.com/ripperhe/Bob/releases/latest/download/Bob.zip) |
| 从 [Gitee release](https://gitee.com/ripperhe/Bob/releases) 下载 | 国内从这里下载更快 | [点此下载 ⬇](https://gitee.com/ripperhe/Bob/attach_files/980744/download/Bob.zip) |

下载完成之后，解压并拖拽到**应用程序**文件夹即可

# 如何使用

## 软件介绍

打开bob 偏好设置

![偏好设置](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071904916.png)

软件页面如下图，主要用到以下两个功能。其中`偏好设置`是设置常用快捷键以及用户偏好的，`服务`重点是翻译功能以及截图识别并翻译功能。

![软件页面](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071906587.png)

点击`文本翻译`tab下的“+”号添加一种API，常用的有百度翻译，腾讯翻译，阿里翻译等。其中软件默认提供了一种百度翻译的，不过百度翻译的秘钥是作者免费提供的，不稳定，可以添加完服务以后自己申请对应平台的秘钥，使用自己的秘钥进行翻译。

![文本翻译](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071906502.png)

![添加秘钥](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071907135.png)

其中`简明英汉词典`和`金山词霸`是内置的，可以添加上去。如果使用`简明英汉词典`别忘记下载开源的词典数据库，可以使翻译更精确。

![内置](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071908179.png)

在`文本识别`翻译中，建议使用内置的`离线文本识别`，这个使用的是Mac系统内置的文字识别服务，可免费使用。当前如果感觉系统文字识别效果不好，也可用点击“+”号添加下面的平台服务，自己去申请秘钥添加。

![文本识别](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071909727.png)

在`语音合成`中，同样建议使用系统的`离线语音合成`，调用Mac系统原生的读屏幕功能。同样可以点击“+”号单独申请各个平台独立的秘钥使用。

![语音合成](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071909716.png)

## plugin的介绍。

插件是软件提供的第三方集成服务，可拓展此软件功能。使用方法是，先下载插件，然后双击即可安装。安装过的插件，会在点击“+”号时显示可用状态。

[插件使用教程](https://ripperhe.gitee.io/bob/#/general/quickstart/plugin)

![plugin](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071910199.png)

插件下载过程，首先打开链接[https://github.com/topics/bobplugin](https://github.com/topics/bobplugin)，打开页面如图

![plugin-list](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071911971.jpeg)

然后选择你需要的插件，本例以第一个`bobplugin-google-translate`谷歌翻译插件为例。点击第一个进入页面:

![bobplugin-google-translate](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071912926.jpeg)

点击箭头所指的地方，即Release下面的版本号，点击后进入最新版本的发布页面：

![bobplugin-google-translate release](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071912568.jpeg)

点击箭头所示的，以`.bobplugin`为后缀的文件，会自动下载。下载后的文件，直接双击进行安装：

![install plugin](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071913327.jpeg)

安装后可在全部插件里看到此插件：

![all plugins](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071913315.png)

可以在`服务`里的`文本翻译`的“+”号里添加使用。

![文本翻译添加插件](https://raw.githubusercontent.com/wangyingbo/PrivateImages/master/2022/202206071914167.png)

**插件推荐**

这是 Bob 的一个 google 语法检查插件, 基于 Bob google 翻译插件修改而来。插件会先将输入的文本使用 google 翻译一遍，再把翻译结果用 google 翻译回输入语言，适用于书写英文时查看 Google 翻译推荐的写法，也许可以帮你纠正时态、补充定语、推荐更准确的单词等。
[https://github.com/tankxu/bobplugin-google-translate-grammar-checker](https://github.com/tankxu/bobplugin-google-translate-grammar-checker)
Bob 的一个Google 翻译插件。使用Google翻译进行翻译，无需翻墙即可使用。
[https://github.com/roojay520/bobplugin-google-translate](https://github.com/roojay520/bobplugin-google-translate)
能不能好好好说话。互联网缩写词、潮流词查询等。
[https://github.com/roojay520/bobplug-nbnhhsh](https://github.com/roojay520/bobplug-nbnhhsh)
一个 Bob 插件，支持简繁互转，汉字>拼音，汉字>火星文转换。
[https://github.com/roojay520/bobplug-pinyin](https://github.com/roojay520/bobplug-pinyin)
Google tts文字转语音插件。
[https://github.com/roojay520/bobplug-google-tts](https://github.com/roojay520/bobplug-google-tts)


----


# 各个服务平台的申请教程和平台对比

请参考链接  [服务教程与各平台对比](https://ripperhe.gitee.io/bob/#/general/quickstart/service)

Bob 的翻译功能是由几种的服务配合完成的，如下所示：

| 服务 | 使用场景 |
| :-- | :-- |
| 文本翻译 | 用于翻译文本，**每次翻译都会调用** |
| 文本识别 | 用于获取图片中的文本，**截图翻译时会调用** |
| 语音合成 | 用于合成音频，点击翻译页面播放按钮时会调用 |

每种服务我都接入了多家服务商的服务，你可以根据自己的喜好自由选择。

**Bob 本身是不收费的，但使用某些服务可能需要给服务商支付一定的费用，这和 Bob 无关**。

所以你现在有三个选择：

1. 使用 Bob 内置的服务
    * 这些服务可以直接添加使用，无需额外配置
    * 这些服务要么本来就是免费的，要么就是填的我的秘钥，然后我共享给大家使用了
    * 我的秘钥每月的总额度和每秒并发请求数都是有限的，**随着使用人数的增多，一定会出现调用缓慢甚至完全无法使用的情况**
2. 自行申请私人秘钥
    * 稳定可靠，申请一次可持续使用
    * **许多服务都有大量免费额度，私人使用足够了**
    * 需要自行申请，可能略显繁琐
3. 自定义插件
    * 可以利用 `JavaScript` 自定义 API
    * 可以用于接入一些你需要，但是 Bob 没有接入的服务
    * 需要一定的编码能力，不过也可以使用他人写好的 Bob 插件

### 已接入的服务

下方列出了 Bob 已接入的所有服务，同时也展示的各大服务商的大致收费情况，**数据仅供参考**。每个服务商的计费规则复杂多样，随着时间推移可能有一定变化。

?> 我针对每个可以申请私人秘钥的服务都写了一篇申请教程，跟随教程应该很快就能申请完成。 💪

文本翻译：

| 服务 | 免费额度 | 超出免费额度 | 并发请求数 | 申请教程 |
| :-- | :-- | :-- | :-- | :-- |
| 百度翻译试用版 | - | - | - | 内置服务，无需申请，不保证稳定性 |
| 金山词霸 | - | - | - | 内置服务，无需申请，不保证稳定性 |
| 简明英汉词典增强版 | - | - | - | 内置服务，无需申请，不保证稳定性 |
| 腾讯翻译君 | 每月500万字符 👍 | 58元/100万字符 | 5次/秒 | [点此跳转](service/translate/tencent.md) |
| 百度翻译 | 完全免费，无限使用 👍 | | 1次/秒 | [点此跳转](service/translate/baidu.md) |
| 阿里翻译| 每月100万字符 👍 | 50元/100万字符 | 50次/秒 | [点此跳转](service/translate/ali.md) |
| 有道翻译 | 无 | 48元/100万字符 | 无相关说明 | [点此跳转](service/translate/youdao.md) |
| 搜狗翻译（即将下线） | 无 | 40元/100万字符 | 50次/秒 | [点此跳转](service/translate/sougou.md) |
| 彩云小译 | 每月100万字符 👍 | 20元/100万字符 | 无相关说明 | [点此跳转](service/translate/caiyun.md) |
| 小牛翻译 | 无 | 500元/1000万字符 | 50次/秒 | [点此跳转](service/translate/niu.md) |
| Google 翻译 | 每月50万字符 | 20美元/100万字符 | 无相关说明 | [点此跳转](service/translate/google.md) |

文本识别：

| 服务 | 免费额度 | 超出免费额度 | 并发请求数 | 申请教程 |
| :-- | :-- | :-- | :-- | :-- |
| 离线文本识别 | - | - | - | 内置服务，macOS 11 以上可用，可离线使用 |
| 百度智能云通用 OCR 试用版 | - | - | - | 内置服务，无需申请，不保证稳定性 |
| 百度智能云通用 OCR | 每月1000次 👍 | 0.0050元/次 | 2次/秒 | [点此跳转](service/ocr/baidu.md) |
| 腾讯云通用 OCR | 每月1000次 👍 | 0.15元/次 | 无相关说明 | [点此跳转](service/ocr/tencent.md) |
| 腾讯云图片翻译 | 每月10000次 👍 | 0.045元/次 | 1次/秒 | [点此跳转](service/ocr/tencentimagetranslate.md) |
| 有道智云通用 OCR | 无 | 0.01元/次 | 无相关说明 | [点此跳转](service/ocr/youdao.md) |
| 搜狗深智 OCR（即将下线） | 无 | 0.006元/次 | 无相关说明 | [点此跳转](service/ocr/sougou.md) |
| Google OCR | 每月1000次 👍 | 1.5美元/1000次 | 1800次/分钟 | [点此跳转](service/ocr/google.md) |

语音合成：

| 服务 | 免费额度 | 超出免费额度 | 并发请求数 | 申请教程 |
| :-- | :-- | :-- | :-- | :-- |
| 离线语音合成 | - | - | - | 内置服务，macOS 10.15 以上可用，可离线使用 |
| 腾讯云语音合成 | 新用户可领取800万字符，3月内有效 | 0.2元/万字符 | 20次/秒（免费试用为3次/秒） | [点此跳转](service/tts/tencent.md) |
| Google 语音合成 | 每月400万字符 👍 | 4美元/100万字符 | 无相关说明 | [点此跳转](service/tts/google.md) |

## 通过插件接入服务

考虑到部分用户希望自定义 API，Bob 支持以插件的形式自行实现各种服务。将开发完成的插件安装到 Bob，即可像其他普通的服务一样使用。详情见 [使用插件](general/quickstart/plugin.md) 相关文章。

## 如何添加和启用服务?

在 Bob 中打开 「偏好设置-翻译-服务」，这里我以「文本翻译」服务为例

1. 选中「文本翻译」tab 栏
2. 点击页面下方的 <b><font color=red>+</font></b> 号
3. 在弹出的菜单中选中自己想要添加的服务
4. 如果添加的是需要输入秘钥的服务，请将申请的秘钥填到服务详情的对应位置（可以点击 `验证` 按钮测试秘钥是否有效）
5. 确保自己刚刚创建的服务的开关是<b><font color=red>开启状态</font></b>
6. 点击页面右下角<b><font color=red>「保存」</font></b>按钮❗️❗️❗️

