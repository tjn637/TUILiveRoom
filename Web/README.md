## 前言
如果您正在为直播活动寻找一个推拉流的应用，如果您想要办一场讲座且在讲课的同时满足分享 PPT 的需求，如果您想要满足不同延迟度要求的直播场景，如果您需要在直播的过程中和在线观众进行互动，那么腾讯云快速推拉流场景化解决方案就是为解决您的需求而准备。

借鉴市场中推拉流场景的常见解决方案，我们提供了包含 UI 的推拉流解决方案 [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) 和 [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer) 供您使用和参考。TUIPusher 及 TUIPlayer 功能演示请观看以下视频。同时，为了您更加快速的体验 TUIPusher & TUIPlayer 的功能，我们结合用户管理系统和房间管理系统提供了 [TUIPusher 体验链接](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html) 及 [TUIPlayer 体验链接](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html)。

<img width="1280" src="liveroom_pusher.gif"/>
<img width="1280" src="liveroom_player.gif"/>

## 功能介绍
### TUIPusher 推流组件
- 支持采集麦克风和扬声器的流并推流
  - 可根据需求设置视频参数（帧率，分辨率，码率）
  - 支持开启美颜并设置视频美颜参数
- 支持采集屏幕分享流并推流
- 支持推流到腾讯云实时音视频后台，推流到腾讯云 CDN
- 支持在线聊天室，和在线观众进行聊天互动
- 支持获取观众列表，对在线观众进行禁言操作

### TUIPlayer 拉流组件
- 支持同时播放音视频流和屏幕分享流
- 支持在线聊天室，和在线观众进行聊天互动
- 支持超低延时直播（300ms 延时）, 快直播（1000ms 以内延时）以及标准直播（支持超高并发观看）三种拉流线路


## 接入方式
[](id:step1)
### 步骤1：账号准备
TUIPusher & TUIPlayer 基于腾讯云实时音视频和即时通讯服务进行开发。
1. [注册腾讯云账号](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327) 并开通 [实时音视频](https://console.cloud.tencent.com/trtc) 和 [即时通讯](https://console.cloud.tencent.com/im) 服务。
2. 在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 单击 **应用管理 > 创建应用** 创建新应用。
![创建应用](https://main.qcloudimg.com/raw/34f87b8c0a817d8d3e49baac5b82a1fa.png)
2. 在 **应用管理 > 应用信息** 中获取 SDKAppID 信息。
![](https://qcloudimg.tencent-cloud.cn/raw/f7915fbbeb48518c2b25a413960f3432.png)
3. 在 **应用管理 > 快速上手** 中获取应用的 secretKey 信息。
![](https://qcloudimg.tencent-cloud.cn/raw/06d38bbdbaf43e1f2b444edae00019fa.png)

>!
>- 首次创建实时音视频应用的腾讯云账号，可获赠一个10000分钟的音视频资源免费试用包。
>- 创建实时音视频应用之后会自动创建一个 SDKAppID 相同的即时通信 IM 应用，可在 [即时通讯控制台](https://console.cloud.tencent.com/im) 配置该应用的套餐信息。

[](id:step2)
### 步骤2：项目准备
1. 在 [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web) 下载 TUIPusher & TUIPlayer 代码。
2. 为 TUIPusher & TUIPlayer 安装依赖。
```bash
cd Web/TUIPusher
npm install

cd Web/TUIPlayer
npm install
```
3. 将 sdkAppId 和  secretKey 填入 `TUIPusher/src/config/basic-info-config.js` 及 `TUIPlayer/src/config/basic-info-config.js` 配置文件中。
![](https://qcloudimg.tencent-cloud.cn/raw/9286fcb781fa37179f84e4bdcd85bfae.png)
4. 本地开发环境运行 TUIPusher & TUIPlayer。
```bash
cd Web/TUIPusher
npm run serve

cd Web/TUIPlayer
npm run serve
```
5. 可打开 `http://localhost:8080` 和 `http://localhost:8081` 体验 TUIPusher 和 TUIPlayer 功能。
6. 可更改 `TUIPusher/src/config/basic-info-config.js` 及 `TUIPlayer/src/config/basic-info-config.js` 配置文件中的房间，主播及观众等信息，**注意保持 TUIPusher 和 TUIPlayer 的房间信息，主播信息一致**。

>! 完成以上配置，您可以使用 TUIPusher & TUIPlayer 进行超低延时直播，如您需要支持快直播和标准直播，请继续阅读 [步骤3：旁路直播](#step3)。
>

[](id:step3)

### 步骤3：旁路直播

TUIPusher & TUIPlayer 实现的快直播和标准直播依托于腾讯云的云直播服务，因此支持快直播和标准直播线路需要您开启旁路推流功能。

1. 在 [**实时音视频控制台**](https://console.cloud.tencent.com/trtc) 中为您正在使用的应用开启旁路推流配置，可按需开启指定流旁路或全局自动旁路。
![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
2. 请在 [**域名管理**](https://console.cloud.tencent.com/live/domainmanage) 页面添加自有播放域名，具体请参见 [添加自有域名](https://cloud.tencent.com/document/product/267/20381)。
3. 在 `TUIPlayer/src/config/basic-info-config.js` 配置文件中配置播放域名。

完成以上配置，您可以体验 TUIPusher & TUIPlayer 支持超低延时直播，快直播以及标准直播的所有功能。

[](id:step4)

### 步骤4：生产环境应用
当您将 TUIPusher & TUIPlayer 用于生产应用时，在接入 TUIPusher & TUIPlayer 之外，您需要：
- 创建用户管理系统，用于管理产品用户信息，包括但不限于用户 ID,  用户名，用户头像等。
- 创建房间管理系统，用于管理产品直播间信息，包括但不限于直播间 ID、直播间名称，直播间主播信息等。
- 服务端生成  UserSig。
> !
> - 本文使用生成 UserSig 的方式，是在客户端根据您填入的 sdkAppId 及 secretKey 生成 userSig，该方式的 secretKey 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TUIPusher & TUIPlayer 进行功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的应用向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275#Server)。
- 参考 `TUIPusher/src/pusher.vue` 及 `TUIPlayer/src/player.vue` 文件，将用户信息、直播间信息、SDKAppId 及 UserSig 等账号信息提交到 vuex 的 store 进行全局存储，您就可以跑通推拉流两个客户端的所有功能。详细业务流程参见下图：
![](https://qcloudimg.tencent-cloud.cn/raw/d2cafd2e0f029908859f7498e9d92297.png)

## 注意事项
###  平台支持

| 操作系统 | 浏览器类型 | 浏览器最低版本要求 | TUIPlayer | TUIPusher | TUIPusher 屏幕分享 |
| ------- | ------- | ------- | ------- | ------- | ------- |
| Mac OS | 桌面版 Safari 浏览器 | 11+ | 支持 | 支持 | 支持（需要 Safari13+ 版本）  |
| Mac OS   | 桌面版 Chrome 浏览器 | 56+ | 支持 | 支持 | 支持（需要 Chrome72+ 版本）  |
| Mac OS   | 桌面版 Firefox 浏览器 | 56+ | 支持 | 支持 | 支持（需要 Firefox66+ 版本） |
| Mac OS   | 桌面版 Edge 浏览器 | 80+ | 支持 | 支持 | 支持 |
| Mac OS   | 桌面版微信内嵌网页 | - | 支持      | 不支持    | 不支持 |
| Mac OS   | 桌面版企业微信内嵌网页 | - | 支持 | 不支持    | 不支持 |
| Windows  | 桌面版 Chrome 浏览器 | 56+ | 支持 | 支持 | 支持（需要 Chrome72+ 版本）  |
| Windows  | 桌面版 QQ 浏览器（极速内核） | 10.4+ | 支持 | 支持 | 不支持 |
| Windows  | 桌面版 Firefox 浏览器 | 56+ | 支持 | 支持 | 支持（需要 Firefox66+ 版本） |
| Windows  | 桌面版 Edge 浏览器 | 80+ | 支持 | 支持 | 支持 |
| Windows  | 桌面版微信内嵌网页 | - | 支持 | 不支持 | 不支持 |
| Windows  | 桌面版企业微信内嵌网页 | - | 支持 | 不支持 | 不支持 |

### 域名要求
出于对用户安全、隐私等问题的考虑，浏览器限制网页在 HTTPS 协议下才能正常使用 TUIPusher & TUIPlayer 的全部功能。为确保生产环境用户顺畅接入和体验 TUIPusher & TUIPlayer 的全部功能，请使用 HTTPS 协议访问音视频应用页面。
>! 本地开发可以通过 `http://localhost` 协议进行访问。

URL 域名及协议支持情况请参考如下表格：

| 应用场景 | 协议 | TUIPlayer | TUIPusher | TUIPusher 屏幕分享 | 备注 |
| ------- | ------- | ------- | ------- | ------- | ------- |
| 生产环境 | HTTPS 协议 | 支持 | 支持 | 支持 | 推荐 |
| 生产环境     | HTTP 协议 | 支持      | 不支持    | 不支持 | - |
| 本地开发环境 | `http://localhost` | 支持 | 支持 | 支持 | 推荐 |
| 本地开发环境 | `http://127.0.0.1`| 支持 | 支持 | 支持 | - |
| 本地开发环境 | `http://[本机IP]` | 支持 | 不支持 | 不支持 | - |

### 防火墙限制
TUIPusher & TUIPlayer 依赖以下端口进行数据传输，请将其加入防火墙白名单。
- TCP 端口：8687
- UDP 端口：8000，8080，8800，843，443，16285
- 域名：qcloud.rtc.qq.com

## 结语
TUIPusher 和 TUIPlayer 组件在持续优化中，未来将推出互动连麦，弹幕等功能。您的支持和反馈是我们不断进步的动力，欢迎加入QQ群（群号：592465424）进行技术交流和问题反馈。

![image-20210622142449407](https://main.qcloudimg.com/raw/1ea3ab1ff36d37c889f4140499585a4a.png)