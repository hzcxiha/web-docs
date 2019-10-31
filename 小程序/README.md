## 前言

从16年微信小程序内测的时候到如今，微信小程序用时间与实践证明了自己的变革与价值，微信小程序的规则也在开发社区的影响下变得更加完善。

对于第三方企业来讲，微信为自己带来了巨大的流量入口和低成本的拉新渠道，如美团、京东、阿里、百度等公司都推出了自己的小程序。

对于小程序开发者来说，小程序的开发生态不断地在完善。到现在，有多种开发微信小程序的方式，主要有原生，[wepy](https://github.com/Tencent/wepy)，[mpvue](https://github.com/Meituan-Dianping/mpvue)，[Taro](https://github.com/NervJS/taro)，[uni-app](https://github.com/dcloudio/uni-app)，[chameleon](https://github.com/didi/chameleon)等

## 框架选型

目前眼花缭乱的小程序框架对于开发者来说，使用哪一种比较好呢，下面我们来对比一下。
#### 1.多端支持度
![image](https://storage.jd.com/taro-resource/duoduan.png)

只从支持端的数量来看，Taro 和 uni-app 以六端略微领先（移动端、H5、微信小程序、百度小程序、支付宝小程序、头条小程序），chameleon 少了头条小程序紧随其后。

但值得一提的是 chameleon 有一套自研多态协议，编写多端代码的体验会好许多，可以说是一个能戳到多端开发痛点的功能。uni-app 则有一套独立的条件编译语法，这套语法能同时作用于 js、样式和模板文件。Taro 可以在业务逻辑中根据环境变量使用条件编译，也可以直接使用条件编译文件（类似 React Native 的方式）。
在移动端方面，uni-app 基于 weex 定制了一套 nvue 方案 弥补 weex API 的不足；Taro 则是暂时基于 expo 达到同样的效果；chameleon 在移动端则有一套 SDK 配合多端协议与原生语言通信。

H5 方面，chameleon 同样是由多态协议实现支持，uni-app 和 Taro 则是都在 H5 实现了一套兼容的组件库和 API。

mpvue 和 WePY 都提供了转换各端小程序的功能，但都没有 h5 和移动端的支持。

所以这一轮对比的结果是：

chameleon > Taro、uni-app > mpvue > WePY

#### 2.组件库/工具库/demo
![image](https://storage.jd.com/taro-resource/component.png)

作为开源时间最长的框架，WePY 不管从 Demo，组件库数量 ，工具库来看都占有一定优势。

uni-app 则有自己的插件市场和 UI 库，如果算上收费的框架和插件比起 WePy 也是完全不遑多让的。

Taro 也有官方维护的跨端 UI 库 taro-ui ，另外在状态管理工具上也有非常丰富的选择（Redux、MobX、dva），但 demo 的数量不如前两个。但 Taro 有一个转换微信小程序代码为 Taro 代码的工具，可以弥补这一问题。

而 mpvue 没有官方维护的 UI 库，chameleon 第三方的 demo 和工具库也还基本没有。

所以这轮的排序是：

WePY > uni-app 、taro > mpvue > chameleon

#### 3.流行度
从目前GitHub上的Star来看
taro > WePY、mpvue > uni-app > chameleon

#### 4.基于公司业务和团队思考
对于公司业务，肯定是要快速迭代开发的，而原生框架对工程化上支持并不友好，可以排除在外。

如果团队是以Vue开发为主的可以考虑mpvue、uni-app，但从多端开发考虑uni-app更优，而且uni-app开发者和案例更多：20万+开发者，50+QQ、微信群，数万案例（[详见](https://uniapp.dcloud.io/case)），被阿里小程序官方工具内置（[详见](https://docs.alipay.com/mini/ide/0.70-stable)）

如果团队以react开发为主，Taro则是必选项。

#### 总结

那说了那么多，到底用哪个呢？

如果不介意尝鲜和学习 DSL 的话，完全可以尝试 WePY 2.0  和 chameleon ，一个是酝酿了很久的 2.0 全新升级，一个是最新发布有专门针对多端开发的多态协议。

uni-app 和 Taro 相比起来就更像是「水桶型」框架，从工具、UI 库，开发体验、多端支持等各方面来看都没有明显的短板。而 mpvue 由于开发一度停滞，现在看来各个方面都不如在小程序端基于它的 uni-app。

## 开发规范

综上所述，目前最优的框架莫过于uni-app和taro，所以我们只介绍这两者。

#### 一、Taro （[详见](https://nervjs.github.io/taro/docs/spec-for-taro.html#docsNav)）

##### 目录结构

```
├── config                 配置目录
|   ├── dev.js             开发时配置
|   ├── index.js           默认配置
|   └── prod.js            打包时配置
├── src                    源码目录
|   ├── components         公共组件目录
|   ├── pages              页面文件目录
|   |   ├── index          index 页面目录
|   |   |   ├── banner     页面 index 私有组件
|   |   |   ├── index.js   index 页面逻辑
|   |   |   └── index.css  index 页面样式
|   ├── utils              公共方法库
|   ├── app.css            项目总通用样式
|   └── app.js             项目入口文件
└── package.json
```
##### 文件命名
Taro 中普通 JS/TS 文件以小写字母命名，多个单词以下划线连接，例如 util.js、util_helper.js

Taro 组件文件命名遵循 Pascal 命名法，例如 ReservationCard.jsx

##### 文件后缀
Taro 中普通 JS/TS 文件以 .js 或者 .ts 作为文件后缀

Taro 组件则以 .jsx 或者 .tsx 作为文件后缀，当然这不是强制约束，只是作为一个实践的建议，组件文件依然可以以 .js 或者 .ts 作为文件后缀
##### JavaScript 书写规范（[详情](https://nervjs.github.io/taro/docs/spec-for-taro.html#javascript-%E4%B9%A6%E5%86%99%E8%A7%84%E8%8C%83)）
##### 组件及 JSX 书写规范（[详情](https://nervjs.github.io/taro/docs/spec-for-taro.html#%E7%BB%84%E4%BB%B6%E5%8F%8A-jsx-%E4%B9%A6%E5%86%99%E8%A7%84%E8%8C%83)）
#### 二、uni-app（[详情](https://uniapp.dcloud.io/frame)）

##### 目录结构

```
┌─components            uni-app组件目录
│  └─comp-a.vue         可复用的a组件
├─hybrid                存放本地网页的目录
├─platforms             存放各平台专用页面的目录
├─pages                 业务页面文件存放的目录
│  ├─index
│  │  └─index.vue       index页面
│  └─list
│     └─list.vue        list页面
├─static                存放应用引用静态资源（如图片、视频等）的目录，注意：静态资源只能存放于此
├─wxcomponents          存放小程序组件的目录
├─main.js               Vue初始化入口文件
├─App.vue               应用配置，用来配置App全局样式以及监听 应用生命周期
├─manifest.json         配置应用名称、appid、logo、版本等打包信息
└─pages.json            配置页面路由、导航条、选项卡等页面类信息
```

##### 开发规范
为了实现多端兼容，综合考虑编译速度、运行性能等因素，uni-app 约定了如下开发规范：

- 页面文件遵循 [Vue 单文件组件 (SFC) 规范](https://vue-loader.vuejs.org/zh/spec.html)
- 组件标签靠近小程序规范，详见[uni-app 组件规范](https://uniapp.dcloud.io/component/README)
- 接口能力（JS API）靠近微信小程序规范，但需将前缀 wx 替换为 uni，详见[uni-app接口规范](https://uniapp.dcloud.io/api/README)
- 数据绑定及事件处理同 Vue.js 规范，同时补充了App及页面的生命周期
- 为兼容多端运行，建议使用flex布局进行开发

## 相关文章：
[跨端开发框架深度横评](https://juejin.im/post/5ca1736af265da30ae314248)