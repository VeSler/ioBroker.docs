---
translatedFrom: en
translatedWarning: 如果您想编辑此文档，请删除“translatedFrom”字段，否则此文档将再次自动翻译
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/zh-cn/adapterref/iobroker.alpha-ess/README.md
title: ioBroker.alpha-ess
hash: V4ISnss7tsahkwLRKntb/ZHb75ptTvTUQp4w13zChfY=
---
![标识](../../../en/adapterref/iobroker.alpha-ess/admin/alpha-ess.png)

![安装数量（最新）](http://iobroker.live/badges/alpha-ess-installed.svg)
![安装数量（稳定）](http://iobroker.live/badges/alpha-ess-stable.svg)
![NPM 版本](http://img.shields.io/npm/v/iobroker.alpha-ess.svg)
![下载](https://img.shields.io/npm/dm/iobroker.alpha-ess.svg)
![已知漏洞](https://snyk.io/test/github/Gaspode69/ioBroker.alpha-ess/badge.svg)

# IoBroker.alpha-ess
## IoBroker 的 alpha-ess 适配器
此适配器登录到 [阿尔法ESS](https://www.alphaess.com/) 的 Web API 并检索您的 Alpha ESS 设备的信息。\根据您的 Alpha ESS 产品，可以获得设备的实时数据和配置数据。 API 返回哪些数据点取决于您的 Alpha ESS 设备。

此适配器支持两个 API，内部的 Alpha ESS Web API（Alpha ESS 可以随时更改）和 Alpha ESS Open API（功能较少，但在 Alpha ESS 设备的官方文档 API 上）。

目前，此适配器为每个受支持的数据点创建一个状态，该状态希望具有自我解释的名称。\所有其他数据点都将被忽略。在适配器启动期间，这些数据点被记录为调试消息。

从 1.0.0-alpha.5 版本开始，每个状态的质量属性根据其状态进行设置：

|质量 |意思 |
|:--------|:--------------------------------------------------|
|0x00 |好的并且是最新的|
|0x01 |由于未知原因，值未更新，请参阅日志 |
|0x02 |此数据点的在线连接有问题|
|0x12 |适配器断开连接或停止|
|0x44 |API 返回错误或内部错误，见日志 |

## 设置：
**使用的 API：** 在非官方“封闭”API 和官方“开放”API（开发中）之间进行选择 根据所选的 API，有不同的可用设置。

**关闭API设置：**

- **用户名：**您的 Alpha ESS 帐户的用户名
- **密码：**您的 Alpha ESS 帐户的密码
- **Alpha ESS 系统 ID：**您的 Alpha ESS 设备的系统标识符
- **读取实时数据的时间间隔：** 单位：秒。
- **读取能量数据的时间间隔：** 单位：分钟。
- **读取设置数据的间隔：** 单位：分钟。
- **读取当天统计数据的时间间隔：** 单位：分钟。
- **读取汇总数据的时间间隔：** 单位：分钟。

可以使用 Alpha ESS 提供的模拟账户。凭据（用户名、系统 ID）在适配器中设置为默认值。
密码以加密方式存储，因此必须手动输入：demo

**打开 API 设置：**

为了能够使用新的 Open API，您必须在 https://open.alphaess.com 下注册您的 Alpha-ESS 设备。注册后，您将获得一个开发者 ID 和一个开发者密钥（称为“秘密”）。您需要这些才能访问 Open API。目前我不知道这是否会在未来改变。

- **个人申请ID：**申请ID（见上文）
- **个人申请秘密：**申请秘密（见上文）
- **Alpha ESS 系统 ID：**您的 Alpha ESS 设备的系统标识符
- **读取实时数据的时间间隔：** 单位：秒。
- **读取能量数据的时间间隔：** 单位：分钟。
- **读取充电设置的间隔：** 单位：分钟。
- **读取放电设置的间隔：** 单位：分钟。
- **读取汇总数据的时间间隔：** 单位：分钟。

##免责声明
**所有产品和公司名称或徽标均为其各自所有者的商标™ 或注册® 商标。使用它们并不意味着与它们或任何相关子公司有任何从属关系或认可！这个个人项目是在业余时间维护的，没有业务目标。**

## Changelog

### **WORK IN PROGRESS**

-   (Gaspode) Support also the new official OpenAPI provided by Alpha-ESS
-   (Gaspode) Set state quality accordingly to status of data
-   (Gaspode) Writing charging and discharging settings implemented for 'Closed API' and OpenAPI
-   (Gaspode) Remove no more supported states at startup automatically

### 0.4.0 (2023-02-16)

-   (Gaspode) Optimized deletion of group states
-   (Gaspode) Added new Realtime state for pmeter_dc

### 0.3.0 (2023-02-11)

-   (Gaspode) Read selected statistical data
-   (Gaspode) Added Summary data
-   (Gaspode) Refactored complete implementation
-   (Gaspode) Changed the unit of settings for all intervals, except of realtime data, to minutes (Caution: settings are reset to defaults)
-   (Gaspode) Remove disabled states at adapter startup
-   (Gaspode) Removed no more supported value 'createtime' (state ID Realtime.Last_update).
-   (Gaspode) Optimized rounding for selected values
-   (Gaspode) Added states EV1_power, EV2_power, EV3_power and EV4_power to Realtime folder

### 0.1.0 (2023-01-15)

-   (Gaspode) First release for Latest repository
-   (Gaspode) Corrected typo in state ID Battery_SOC
-   (Gaspode) Implemented improvements as suggested in code review
-   (Gaspode) Slow down requests in case of permanent errors
-   (Gaspode) Changed adapter type from metering to energy
-   (Gaspode) Correction for NPM
-   (Gaspode) Enable NPM

### 0.0.5

-   (Gaspode) Use meaningful state names
-   (Gaspode) Use suitable state roles
-   (Gaspode) Added new state for Alpha ESS settings parameter 'upsReserve'

### 0.0.4

-   (Gaspode) use axios to perform Alpha ESS API calls instead of deprecated request
-   (Gaspode) New option "Update unchanged states" added

### 0.0.3

-   (Gaspode) refactored API calls, added daily energy values

### 0.0.2

-   (Gaspode) corrected api call for realtime data

### 0.0.1

-   (Gaspode) initial release

## License

MIT License

Copyright (c) 2023 Gaspode <gaspode69@online.de>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.