<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->
<div align="right"><strong>🇨🇳中文</a></strong>  | <strong><a href="./README.md">🇬🇧English</strong></div>
<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->

# K6 性能测试快速启动项目

一个关于使用 K6 进行性能测试的快速启动介绍性文档。

- [K6 性能测试快速启动项目](#k6-性能测试快速启动项目)
  - [什么是 K6](#什么是-k6)
  - [官方网站及文档](#官方网站及文档)
  - [安装](#安装)
    - [Mac 系统安装](#mac-系统安装)
    - [Windows 系统安装](#windows-系统安装)
    - [Docker 安装](#docker-安装)
    - [其他系统安装](#其他系统安装)
    - [确认 K6 安装成功](#确认-k6-安装成功)
  - [第一个 K6 测试脚本](#第一个-k6-测试脚本)
    - [编写第一个测试脚本](#编写第一个测试脚本)
      - [新建一个 K6 性能测试项目目录并进入](#新建一个-k6-性能测试项目目录并进入)
      - [创建一个名为 `demo.js` 的文件，用于编写测试脚本](#创建一个名为-demojs-的文件用于编写测试脚本)
      - [编辑测试脚本](#编辑测试脚本)
      - [运行测试脚本](#运行测试脚本)
      - [查看测试结果](#查看测试结果)
      - [解析 demo 测试脚本](#解析-demo-测试脚本)
  - [K6 常用功能](#k6-常用功能)
    - [HTTP Requests](#http-requests)
      - [GET 请求例子](#get-请求例子)
      - [POST 请求例子](#post-请求例子)
      - [支持的 HTTP 方法](#支持的-http-方法)
      - [HTTP 请求标签](#http-请求标签)
    - [Metrics 指标](#metrics-指标)
      - [K6 内置指标](#k6-内置指标)
        - [标准内置指标](#标准内置指标)
        - [HTTP 特定的内置指标](#http-特定的内置指标)
        - [其他内置指标](#其他内置指标)
      - [自定义指标](#自定义指标)
        - [自定义指标 demo 示例](#自定义指标-demo-示例)
          - [1.从导入 k6/metrics 模块引入 Trend 构造函数](#1从导入-k6metrics-模块引入-trend-构造函数)
          - [2.在 init 上下文中构造一个新的自定义度量 Trend 对象](#2在-init-上下文中构造一个新的自定义度量-trend-对象)
          - [3.在脚本中使用 add 方法记录指标测量值](#3在脚本中使用-add-方法记录指标测量值)
          - [4.demo\_custom\_metrics.js 自定义指标完整代码](#4demo_custom_metricsjs-自定义指标完整代码)
          - [5.运行 demo\_custom\_metrics.js 并查看自动化趋势指标](#5运行-demo_custom_metricsjs-并查看自动化趋势指标)
    - [Checks 检查](#checks-检查)
      - [1.检查 HTTP 响应状态](#1检查-http-响应状态)
      - [2.检查 HTTP 响应体](#2检查-http-响应体)
      - [3.添加多个检查](#3添加多个检查)
    - [Thresholds 阈值](#thresholds-阈值)
      - [什么是阈值](#什么是阈值)
      - [HTTP 错误和响应持续时间的阈值示例](#http-错误和响应持续时间的阈值示例)
      - [阈值语法](#阈值语法)
        - [阈值表达式语法](#阈值表达式语法)
        - [按类型划分的聚合方法](#按类型划分的聚合方法)
      - [常用的阈值示例](#常用的阈值示例)
        - [1.在指定持续时间内完成的请求百分比](#1在指定持续时间内完成的请求百分比)
        - [2.错误率低于 1%](#2错误率低于-1)
        - [3.单个指标的多个阈值](#3单个指标的多个阈值)
        - [4.持续时间组的阈值](#4持续时间组的阈值)
      - [超过阈值时中止测试](#超过阈值时中止测试)
    - [Test lifecycle 测试生命周期](#test-lifecycle-测试生命周期)
      - [生命周期阶段概述](#生命周期阶段概述)
      - [init 初始化阶段](#init-初始化阶段)
      - [VU 阶段](#vu-阶段)
      - [Setup 测试前置准备配置阶段 和 teardown 测试后置退出阶段](#setup-测试前置准备配置阶段-和-teardown-测试后置退出阶段)
    - [Scenarios 测试场景](#scenarios-测试场景)
      - [测试场景配置](#测试场景配置)
      - [测试场景执行器](#测试场景执行器)
      - [测试场景配置选项](#测试场景配置选项)
      - [测试场景示例](#测试场景示例)
  - [如何快速编写 K6 性能测试脚本](#如何快速编写-k6-性能测试脚本)
    - [使用 K6 提供的 Test builder 测试生成器工具来编写脚本](#使用-k6-提供的-test-builder-测试生成器工具来编写脚本)
      - [安装 Test builder 测试生成器](#安装-test-builder-测试生成器)
      - [如何使用 Test builder 测试生成器](#如何使用-test-builder-测试生成器)
      - [获取 Test builder 测试生成器生成的脚本](#获取-test-builder-测试生成器生成的脚本)
      - [运行 Test builder 测试生成器生成的脚本](#运行-test-builder-测试生成器生成的脚本)
      - [其他 Test builder 测试生成器的功能](#其他-test-builder-测试生成器的功能)
    - [使用 K6 Recorder 录制器录制脚本](#使用-k6-recorder-录制器录制脚本)
      - [安装 K6 Recorder 录制器](#安装-k6-recorder-录制器)
      - [如何使用 K6 Recorder 录制器](#如何使用-k6-recorder-录制器)
    - [使用浏览器开发者工具和 har-to-k6 工具生成 K6 脚本](#使用浏览器开发者工具和-har-to-k6-工具生成-k6-脚本)
      - [可以获取 HAR 文件的浏览器和工具](#可以获取-har-文件的浏览器和工具)
      - [如何使用浏览器开发者工具获取 HAR 文件](#如何使用浏览器开发者工具获取-har-文件)
      - [使用 har-to-k6 进行转换 HAR 文件](#使用-har-to-k6-进行转换-har-文件)
  - [进阶](#进阶)
    - [输出 html 报告](#输出-html-报告)
    - [持续集成](#持续集成)
      - [接入 github action](#接入-github-action)
    - [Options 配置选项](#options-配置选项)
      - [如何使用配置选项](#如何使用配置选项)
  - [参考资料](#参考资料)

## 什么是 K6

k6 是一款用于性能测试和负载测试的开源工具，主要用于评估和验证应用程序的性能和稳定性。以下是关于 k6 的一些主要特点和信息：

1. **开源性：** k6 是一款完全开源的性能测试工具，代码存储在 GitHub 上。这意味着用户可以自由访问、使用和修改工具的源代码。

2. **JavaScript 编写脚本：** k6 使用 JavaScript 语言编写测试脚本，这使得编写测试用例相对简单，并且对于开发人员而言更加友好。脚本可以包含 HTTP 请求、WebSocket 连接、脚本执行逻辑等。

3. **支持多种协议：** k6 支持多种常见的协议，包括 HTTP、WebSocket、Socket.IO、gRPC 等，使其可以广泛应用于各种类型的应用程序。

4. **分布式测试：** k6 具有分布式测试的能力，允许在多个节点上运行测试，从而模拟更真实的生产环境负载。

5. **实时结果和报告：** k6 提供实时结果，包括请求响应时间、吞吐量等，并能够生成详细的 HTML 报告，帮助用户更好地理解应用程序的性能状况。

6. **容器化支持：** k6 适应容器化环境，可以轻松集成到 CI/CD 流水线中，并与常见的容器编排工具（如 Kubernetes）配合使用。

7. **插件生态系统：** k6 支持插件，用户可以通过插件扩展其功能，满足特定需求。

8. **活跃的社区：** 由于 k6 是一个开源项目，拥有一个积极的社区，提供支持、文档和示例，使用户更容易上手和解决问题。

总体而言，k6 是一个灵活、强大且易于使用的性能测试工具，适用于各种规模的应用程序和系统。

## 官方网站及文档

- [官方网站](https://k6.io/)
- [官方文档](https://k6.io/docs/)

## 安装

### Mac 系统安装

Mac 系统可以通过 Homebrew 安装 k6：

```bash
brew install k6
```

### Windows 系统安装

Windows 系统可以通过 Chocolatey 安装 k6：

```bash
choco install k6
```

或者通过 winget 安装 k6：

```bash
winget install k6
```

### Docker 安装

k6 也可以通过 Docker 安装：

```bash
docker pull grafana/k6
```

### 其他系统安装

K6 除了支持上述系统外，还支持 Linux（Debian/Ubuntu/Fedora/CentOS），也支持下载 K6 二进制文件和 K6 扩展进行安装，具体安装方式请参考[官方文档](https://k6.io/docs/get-started/installation)。

### 确认 K6 安装成功

安装完成后，可以通过以下命令确认 k6 是否安装成功：

```bash
k6 version
```

如果安装成功，会显示 k6 的版本信息：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/QR8wKb.png)

## 第一个 K6 测试脚本

### 编写第一个测试脚本

#### 新建一个 K6 性能测试项目目录并进入

```bash
mkdir k6-demo
cd k6-demo
```

#### 创建一个名为 `demo.js` 的文件，用于编写测试脚本

- 可以通过 `k6 new` 命令创建一个测试脚本文件：

```bash
k6 new demo.js
```

- 也可以直接创建一个名为 demo.js 的测试脚本文件

```bash
touch demo.js
```

#### 编辑测试脚本

如果是通过 `k6 new` 命令创建的测试脚本文件，会自动生成一个简单的测试脚本，如下所示：

```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  // A number specifying the number of VUs to run concurrently.
  vus: 10,
  // A string specifying the total duration of the test run.
  duration: '30s',

  // The following section contains configuration options for execution of this
  // test script in Grafana Cloud.
  //
  // See https://grafana.com/docs/grafana-cloud/k6/get-started/run-cloud-tests-from-the-cli/
  // to learn about authoring and running k6 test scripts in Grafana k6 Cloud.
  //
  // ext: {
  //   loadimpact: {
  //     // The ID of the project to which the test is assigned in the k6 Cloud UI.
  //     // By default tests are executed in default project.
  //     projectID: "",
  //     // The name of the test in the k6 Cloud UI.
  //     // Test runs with the same name will be grouped.
  //     name: "demo.js"
  //   }
  // },

  // Uncomment this section to enable the use of Browser API in your tests.
  //
  // See https://grafana.com/docs/k6/latest/using-k6-browser/running-browser-tests/ to learn more
  // about using Browser API in your test scripts.
  //
  // scenarios: {
  //   // The scenario name appears in the result summary, tags, and so on.
  //   // You can give the scenario any name, as long as each name in the script is unique.
  //   ui: {
  //     // Executor is a mandatory parameter for browser-based tests.
  //     // Shared iterations in this case tells k6 to reuse VUs to execute iterations.
  //     //
  //     // See https://grafana.com/docs/k6/latest/using-k6/scenarios/executors/ for other executor types.
  //     executor: 'shared-iterations',
  //     options: {
  //       browser: {
  //         // This is a mandatory parameter that instructs k6 to launch and
  //         // connect to a chromium-based browser, and use it to run UI-based
  //         // tests.
  //         type: 'chromium',
  //       },
  //     },
  //   },
  // }
};

// The function that defines VU logic.
//
// See https://grafana.com/docs/k6/latest/examples/get-started-with-k6/ to learn more
// about authoring k6 scripts.
//
export default function() {
  http.get('https://test.k6.io');
  sleep(1);
}
```

如果是直接创建的测试脚本文件，可以将上述内容复制到 `demo.js` 文件中。

#### 运行测试脚本

在 `demo.js` 文件所在目录下，运行以下命令：

```bash
k6 run demo.js
```

#### 查看测试结果

如果一切正常，会看到类似如下的输出：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/a4vK69.png)

包含以下信息：

- **execution:** 执行信息，包括开始时间、结束时间、持续时间、VU 数量、迭代次数等。
- **scenarios:** 场景信息，包括场景名称、VU 数量、迭代次数、持续时间、平均响应时间、吞吐量等。
- **http_reqs:** HTTP 请求信息，包括请求名称、请求数量、失败数量、平均响应时间、吞吐量等。

#### 解析 demo 测试脚本

- `import http from 'k6/http';`：导入 k6 的 HTTP 模块，用于发送 HTTP 请求。

- `import { sleep } from 'k6';`：导入 k6 的 sleep 方法，用于执行脚本等待。

- `export const options = { ... }`：定义测试脚本的配置项，包括 VU 数量、持续时间等。

- `vus: 10,`：定义 VU 数量为 10（指定并发运行的 VU 数量）。

- `duration: '30s',`：定义持续时间为 30 秒（指定测试运行总持续时间）。

- `export default function() { ... }`：定义测试脚本的逻辑，包括发送 HTTP 请求、执行等待等。

- `http.get('https://test.k6.io');`：发送一个 GET 请求到 `https://test.k6.io`。

- `sleep(1);`：执行等待 1 秒。

> 其他注释内容可以忽略，这些内容是关于 k6 的一些高级功能，后续会介绍。

## K6 常用功能

### HTTP Requests

使用 K6 进行性能测试的第一步就是定义要测试的 HTTP 请求。

#### GET 请求例子

使用 `k6 new` 命令创建的 demo 测试脚本中，已经包含了一个简单的 GET 方法 HTTP 请求：

```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export default function() {
  http.get('https://test.k6.io');
  sleep(1);
}
```

#### POST 请求例子

这个 POST 请求例子展示一些复杂的场景的应用（带有电子邮件/密码身份验证负载的 POST 请求）

```javascript
import http from 'k6/http';

export default function () {
  const url = 'http://test.k6.io/login';
  const payload = JSON.stringify({
    email: 'aaa',
    password: 'bbb',
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
    },
  };

  http.post(url, payload, params);
}

```

> 以上内容参考自 [K6 官方文档](https://k6.io/docs/using-k6/http-requests)

#### 支持的 HTTP 方法

K6 提供的 HTTP 模块能处理各种 HTTP 请求和方法。以下是支持的 HTTP 方法列表：

| 方法 | 作用 |
| ------- | ------- |
| batch()| 并行发出多个 HTTP 请求（例如浏览器往往会这样做）。|
| del() | 发出 HTTP DELETE 请求。|
| get() | 发出 HTTP GET 请求。|
| head() | 发出 HTTP HEAD 请求。|
| options() | 发出 HTTP OPTIONS 请求。|
| patch() | 发出 HTTP PATCH 请求。|
| post() | 发出 HTTP POST 请求。|
| put() | 发出 HTTP PUT 请求。|
| request() | 发出任何类型的 HTTP 请求。|

#### HTTP 请求标签

K6 允许为每个 HTTP 请求添加标签，结合标签和分组，可以很方便的在测试结果中更好地组织，分组请求和过滤结果组织分析。

以下为支持的标签列表：

| 标签 | 作用 |
| ------- | ------- |
| name | 请求名称。默认为请求的 URL|
| method | 请求方法（GET、POST、PUT 等）|
| url | 默认为请求的 URL。|
| expected_response | 默认情况下，200 到 399 之间的响应状态为 true。使用 setResponseCallback 更改默认行为。|
| group | 当请求在组内运行时，标记值是组名称。默认为空。|
| scenario | 当请求在场景内运行时，标记值是场景名称。默认为 default。|
| status | 响应状态|

HTTP 请求使用 tag 和 group 标签的例子会在后续的 demo 中展示。

大家也可以参考官方的例子：[https://grafana.com/docs/k6/latest/using-k6/http-requests/](https://grafana.com/docs/k6/latest/using-k6/http-requests/)

### Metrics 指标

指标用于衡量系统在测试条件下的性能。默认情况下，k6 会自动收集内置指标。除了内置指标，您还可以创建自定义指标。

指标一般分为四大类：

1. 计数器（Counters）：对值求和。
2. 计量器（Gauges）：跟踪最小、最大和最新的值。
3. 比率（Rates）：跟踪非零值发生的频率。
4. 趋势（Trends）：计算多个值的统计信息（如均值、模式或百分位数）。

要使测试断言符合需求标准，可以根据性能测试要求的指标条件编写阈值（表达式的具体内容取决于指标类型）。

为了后续进行筛选指标，可以使用标签和分组，这样可以更好地组织测试结果。

> 测试结果输出文件可以以各种摘要和细粒度格式导出指标，具体信息请参阅结果输出文档。（后面测试结果输出文档会详细介绍这一部分）

#### K6 内置指标

每个 k6 测试执行都会发出内置和自定义指标。每个支持的协议也有其特定的指标。

##### 标准内置指标

无论测试使用什么协议，k6 始终收集以下指标：

| 指标名称 | 指标分类 | 指标描述 |
| ------- | ------- | -------|
| vus| Gauge |当前活跃虚拟用户数 |
| vus_max | Gauge | 最大可能虚拟用户数（VU 资源已预先分配，以避免扩大负载时影响性能）|
|iterations 迭代|Counter |VU 执行 JS 脚本（default 函数）的总次数。|
|iteration_duration|Trend|完成一次完整迭代的时间，包括在 setup 和 teardown 中花费的时间。要计算特定场景的迭代函数的持续时间，请尝试此解决方法|
|dropped_iterations|Counter|由于缺少 VU（对于到达率执行程序）或时间不足（基于迭代的执行程序中的 maxDuration 已过期）而未启动的迭代次数。关于删除迭代|
|data_received|Counter|接收到的数据量。此示例介绍如何跟踪单个 URL 的数据。|
|data_sent |Counter|发送的数据量。跟踪单个 URL 的数据以跟踪单个 URL 的数据。|
|checks|Rate|设置的检查成功率。|

> 指标分类分别为：计数器（Counter）、计量器（Gauges）、比率（Rates）、趋势（Trends）

##### HTTP 特定的内置指标

HTTP 特定的内置指标是仅在 HTTP 请求期间才会生成和收集的指标。其他类型的请求（例如 WebSocket）不会生成这些指标。

> 注意：对于所有 http_req_* 指标，时间戳在请求结束时发出。换句话说，时间戳发生在 k6 收到响应正文末尾或请求超时时。

下表列出了 HTTP 特定的内置指标：

| 指标名称 | 指标分类 | 指标描述 |
| ------- | ------- | -------|
|http_reqs|Counter|k6 总共生成了多少个 HTTP 请求。|
|http_req_blocked|Trend|在发起请求之前阻塞（等待空闲 TCP 连接槽）所花费的时间。`float`类型|
|http_req_connecting|Trend |与远程主机建立 TCP 连接所花费的时间。`float`类型|
|http_req_tls_handshaking|Trend|与远程主机握手 TLS 会话所花费的时间|
|http_req_sending|Trend|向远程主机发送数据所花费的时间。`float`类型|
|http_req_waiting|Trend|等待远程主机响应所花费的时间（也称为“第一个字节的时间”或“TTFB”）。`float`类型|
|http_req_receiving|Trend|从远程主机接收响应数据所花费的时间。`float`类型|
|http_req_duration|Trend|请求的总时间。它等于 http_req_sending + http_req_waiting + http_req_receiving（即远程服务器处理请求和响应所需的时间，没有初始 DNS 查找/连接时间）。`float`类型|
|http_req_failed|Rate|根据 setResponseCallback 的失败请求率。|

> 指标分类分别为：计数器（Counter）、计量器（Gauges）、比率（Rates）、趋势（Trends）

##### 其他内置指标

K6 内置指标除了标准内置指标和 HTTP 特定的内置指标外，还有其他内置指标：

- Browser metrics 浏览器指标：<https://grafana.com/docs/k6/latest/using-k6/metrics/reference/#browser>
- Built-in WebSocket metrics 内置 WebSocket 指标：<https://grafana.com/docs/k6/latest/using-k6/metrics/reference/#websockets>
- Built-in gRPC metrics 内置 gRPC 指标：<https://grafana.com/docs/k6/latest/using-k6/metrics/reference/#grpc>

#### 自定义指标

除了系统内建的指标之外，您还可以创建自定义指标。例如，您可以计算与业务逻辑相关的指标，或者利用 Response.timings 对象为特定的一组端点创建指标。

每种指标类型都有一个构造函数，用于生成自定义指标。该构造函数会生成一个声明类型的指标对象。每种类型都有一个 add 方法，用于记录指标测量值。

> 注意：必须在 init 上下文中创建自定义指标。这会限制内存并确保 K6 可以验证所有阈值是否评估了定义的指标。

##### 自定义指标 demo 示例

以下示例演示如何创建等待时间的自定义趋势指标：

> 项目文件中的 demo_custom_metrics.js 文件已经包含了这个 demo 示例，可以直接运行查看结果。

###### 1.从导入 k6/metrics 模块引入 Trend 构造函数

```javascript
import { Trend } from 'k6/metrics';
```

> 等待时间趋势指标属于趋势（Trends）指标，所以需要从 k6/metrics 模块引入 Trend 构造函数。

###### 2.在 init 上下文中构造一个新的自定义度量 Trend 对象

```javascript
const myTrend = new Trend('waiting_time');
```

> 在 init 上下文中构造一个新的自定义度量 Trend 对象，脚本中的对象为 myTrend，其指标在结果输出中显示为 `waiting_time`。

###### 3.在脚本中使用 add 方法记录指标测量值

```javascript
export default function() {
  const res = http.get('https://test.k6.io');
  myTrend.add(res.timings.waiting);
}
```

> 在脚本中使用 add 方法记录指标测量值，这里使用了 `res.timings.waiting`，即等待时间。

###### 4.demo_custom_metrics.js 自定义指标完整代码

```javascript
import http from 'k6/http';
import { Trend } from 'k6/metrics';

const myTrend = new Trend('waiting_time');

export default function () {
  const res = http.get('https://httpbin.test.k6.io');
  myTrend.add(res.timings.waiting);
  console.log(myTrend.name); // waiting_time
}
```

###### 5.运行 demo_custom_metrics.js 并查看自动化趋势指标

```bash
k6 run demo_custom_metrics.js
```

运行结果如下：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/4tbqVc.png)

> 可以看到，自定义指标 `waiting_time` 已经在结果输出中显示出来了。

更多关于自定义指标的内容，请参考官方文档：[https://k6.io/docs/using-k6/metrics/#custom-metrics](https://k6.io/docs/using-k6/metrics/#custom-metrics)

### Checks 检查

> 这里也可以理解为断言，即对测试结果进行验证。

检查用来检验不同测试中的具体测试条件是否正确相应，和我们常规在做其他类型测试时也会对测试结果进行验证，以确保系统是否以期望的内容作出响应。

例如，一个验证可以确保 POST 请求的响应状态为 201，或者响应体的大小是否符合预期。

检查类似于许多测试框架中称为断言的概念，但是**K6 在验证失败并不会中止测试或以失败状态结束。相反，k6 会在测试继续运行时追踪失败验证的比率**。

> 每个检查都创建一个速率指标。要使检查中止或导致测试失败，可以将其与阈值结合使用。

下面会介绍如何使用不同类型的检查，以及如何在测试结果中查看检查结果。

#### 1.检查 HTTP 响应状态

K6 的检查非常适用于与 HTTP 请求相关的响应断言。

示例，以下代码片段来检查 HTTP 响应代码为 200：

```javascript
import { check } from 'k6';
import http from 'k6/http';


export default function () {
  const res = http.get('https://httpbin.test.k6.io');
  check(res, {
    'HTTP response code is status 200': (r) => r.status === 200,
  });
}
```

运行该脚本，可以看到如下结果：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/aTXnpy.png)

> 当脚本包含检查时，摘要报告会显示通过了多少测试检查。

在此示例中，请注意检查“HTTP response code is status 200”在调用时是 100% 成功的。

#### 2.检查 HTTP 响应体

除了检查 HTTP 响应状态外，还可以检查 HTTP 响应体。

示例，以下代码片段来检查 HTTP 响应体大小为 9591 bytes：

```javascript
import { check } from 'k6';
import http from 'k6/http';


export default function () {
  const res = http.get('https://httpbin.test.k6.io');
  check(res, {
    'HTTP response body size is 9591 bytes': (r) => r.body.length == 9591,
  });
}
```

运行该脚本，可以看到如下结果：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/AmbL0E.png)

> 当脚本包含检查时，摘要报告会显示通过了多少测试检查。

在此示例中，请注意检查“HTTP response body size is 9591 bytes”在调用时是 100% 成功的。

#### 3.添加多个检查

有时候我们在一个测试脚本中需要添加多个检查，那可以直接在单​​个 check() 语句中添加多个检查，如下面脚本所示：

```javascript
import { check } from 'k6';
import http from 'k6/http';


export default function () {
  const res = http.get('https://httpbin.test.k6.io');
  check(res, {
    'HTTP response code is status 200': (r) => r.status === 200,
    'HTTP response body size is 9591 bytes': (r) => r.body.length == 9591,
  });
}
```

运行该脚本，可以看到如下结果：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/5yJyBw.png)

在此示例中，两个检查都是正常通过的（调用是 100% 成功的）。

> 注意：当检查失败时，脚本将继续成功执行，并且不会返回“失败”退出状态。如果您需要根据检查结果使整个测试失败，则必须将检查与阈值结合起来。这在特定环境中特别有用，例如将 k6 集成到 CI 管道中或在安排性能测试时接收警报。

### Thresholds 阈值

#### 什么是阈值

阈值一般是我们为测试指标定义的通过/失败标准。对于 K6 来说，如果被测系统的性能不满足阈值条件，**测试将以失败状态结束**。

> 前面提到的检查（check）是用来验证测试结果是否符合预期，check 不通过，测试还会继续，而阈值（threshold）是用来验证测试结果是否符合性能要求。如果不符合，测试将以失败状态结束。

通常情况下，我们进行性能测试时会使用阈值来编写不同服务或接口的 SLOs(服务级别目标 Service Level Objectives)。

下面为一些阈值的例子：

- 不到 1% 的请求返回错误。
- 95% 的请求响应时间低于 200 毫秒。
- 99% 的请求响应时间低于 400 毫秒。
- 特定端点始终在 300 毫秒内响应。
- 自定义指标（等待时间趋势）的任何条件（大于 300 毫秒）。

如果后续会写性能自动化测试脚本，那么阈值就是必不可少的。

- 给你的测试一个阈值。
- 自动化执行
- 设置测试失败警报。

#### HTTP 错误和响应持续时间的阈值示例

以下示例演示如何使用阈值来设置并评估 HTTP 错误率（http_req_failed 指标）和评估 95% 的请求响应是否在特定持续时间内发生（http_req_duration 指标）：

```javascript
import http from 'k6/http';

export const options = {
  thresholds: {
    http_req_failed: ['rate<0.01'], // HTTP 错误率应该低于 1%
    http_req_duration: ['p(95)<200'], // 95% 的请求响应应该低于 200ms
  },
};

export default function () {
  http.get('https://test-api.k6.io/public/crocodiles/1/');
}
```

上述的示例中，我们设置了两个阈值：

- HTTP 错误率应该低于 1%。（用到了 http_req_failed 指标）
- 95% 的请求响应应该低于 200ms。（用到了 http_req_duration 指标）

对于上面代码设置的阈值，如果运行的时候，HTTP 错误率低于 1% 和 95% 的请求响应低于 200ms，那么测试就会以成功状态结束，否则任一阈值不满足，测试就将以失败状态结束。

运行该脚本，可以看到如下结果：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/EiPBZ9.png)

结果中显示，http_req_failed 阈值通过了，http_req_duration 阈值没有通过，整体测试以失败状态结束。

> 如果任何阈值失败，则阈值名称（http_req_failed、http_req_duration）旁边的绿色小复选标记 ✓ 将是 ✗ 并且 k6 将以非零值退出退出代码。

#### 阈值语法

阈值语法是一个字符串，由以下部分组成：

- 指标名称（例如 http_req_duration）。
- 一个或多个条件，用逗号分隔。
- 每个条件都由一个运算符和一个值组成。
- 运算符可以是以下之一：>、>=、<、<=、==、!=、=~、!~。
- 值可以是数字或百分比。
- 百分比值必须在 0 到 100 之间。

想要在测试脚本中使用阈值，步骤如下：

1.在 options 对象中添加 thresholds 属性，如下所示：

```javascript
export const options = {
  thresholds: {
    /* ... */
  },
};
```

2.在 thresholds 对象中定义阈值表达式（至少一个，可以多个），如下所示：

```javascript
export const options = {
  thresholds: {
    //短格式
    METRIC_NAME1: ['THRESHOLD_EXPRESSION', `...`],
    //长格式
    METRIC_NAME2: [
      {
        threshold: 'THRESHOLD_EXPRESSION',
        abortOnFail: true, // boolean
        delayAbortEval: '10s', // string
      },
    ], // full format
  },
};
```

- 阈值表达式支持短格式和长格式，短格式将所有阈值表达式作为字符串放入数组中。长格式将每个阈值放入一个对象中，并具有在失败时中止的额外属性。
- 上面示例代码中的 METRIC_NAME1 和 THRESHOLD_EXPRESSION 是占位符。正常情况下必须是指标名称和阈值表达式。
- 示例代码声明配置指标 metric_name1 和 metric_name2 的两个阈值。通过评估阈值后的'threshold_expression'来确定阈值是通过还是失败，.

##### 阈值表达式语法

阈值表达式的计算结果为 `true` 或 `false` 。阈值表达式必须采用以下格式：

``` javascript
<aggregation_method> <operator> <value>
```

- `<aggregation_method>`：聚合方法，用于计算指标的值。例如，p(95) 表示 95% 百分位数，而 avg 表示平均值。
- `<operator>`：运算符，用于比较指标的值与阈值表达式中的值。例如，> 表示大于，< 表示小于，== 表示等于。
- `<value>`：阈值表达式中的值。例如，200 表示 200 毫秒，95 表示 95%。

阈值表达式的一些示例如下：

- avg < 200 // 平均持续时间必须小于 200 毫秒
- count >= 500 // 计数必须大于或等于 500
- p(90) < 300 // 90% 的样本必须低于 300

##### 按类型划分的聚合方法

k6 根据类型聚合指标。这些聚合方法构成阈值表达式的一部分。

以下是按类型划分的聚合方法列表：

| 指标类型  | 聚合方法 |
| ------- | ------- |
｜Counter | count 计数 和 rate 比率 |
｜Gauge | value 具体的值 |
｜Rate | rate 比率 |
｜Trend | avg 平均值、min 最小值、max 最大值、med 和 p(N) 其中 N 指定阈值百分位值，表示为 0.0 到 100 之间的数字。p(99.99) 表示第 99.99 个百分位。这些值以毫秒为单位。｜

一个复杂的聚合方法示例：

```javascript
import http from 'k6/http';
import { Trend, Rate, Counter, Gauge } from 'k6/metrics';
import { sleep } from 'k6';

export const TrendRTT = new Trend('RTT');
export const RateContentOK = new Rate('Content OK');
export const GaugeContentSize = new Gauge('ContentSize');
export const CounterErrors = new Counter('Errors');
export const options = {
  thresholds: {
    // 计数：不允许超过 99 次返回错误的内容。
    'Errors': ['count<100'],
    // 计量：返回的内容必须控制在 4000 字节以下。
    'ContentSize': ['value<4000'],
    // 比率：内容必须在 95 次以上达到“OK”。
    'Content OK': ['rate>0.95'],
    // 趋势：百分位数、平均值、中位数和最小值必须保持在指定的毫秒范围内。
    'RTT': ['p(99)<300', 'p(70)<250', 'avg<200', 'med<150', 'min<100'],
  },
};

export default function () {
  const res = http.get('https://test-api.k6.io/public/crocodiles/1/');
  const contentOK = res.json('name') === 'Bert';

  TrendRTT.add(res.timings.duration);
  RateContentOK.add(contentOK);
  GaugeContentSize.add(res.body.length);
  CounterErrors.add(!contentOK);

  sleep(1);
}
```

注意：不要通过重复相同的对象键来为同一指标指定多个阈值。

> 由于阈值被定义为 JavaScript 对象的属性，因此您不能指定多个具有相同属性名称的阈值。如果要为一个指标设置多个阈值，请使用同一键的数组指定它们。

#### 常用的阈值示例

使用阈值的最快方法是先使用内置指标。以下是一些常用的复制示例

##### 1.在指定持续时间内完成的请求百分比

```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  thresholds: {
    // 90% 的请求必须在 400 毫秒内完成。
    http_req_duration: ['p(90) < 400'],
  },
};

export default function () {
  http.get('https://test-api.k6.io/public/crocodiles/1/');
  sleep(1);
}
```

##### 2.错误率低于 1%
  
```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  thresholds: {
    // 在整个测试执行过程中，错误率必须低于 1％。
    http_req_failed: ['rate<0.01'],
  },
};

export default function () {
  http.get('https://test-api.k6.io/public/crocodiles/1/');
  sleep(1);
}
```

##### 3.单个指标的多个阈值

我们也可以为一项指标应用多个阈值。该阈值对于不同的请求百分位数有不同的持续时间要求。

```javascript
import http from 'k6/http';
import { sleep } from 'k6';

export const options = {
  thresholds: {
    // 90％的请求必须在 400 毫秒内完成，95％在 800 毫秒内完成，99.9％在 2 秒内完成。
    http_req_duration: ['p(90) < 400', 'p(95) < 800', 'p(99.9) < 2000'],
  },
};

export default function () {
  const res1 = http.get('https://test-api.k6.io/public/crocodiles/1/');
  sleep(1);
}
```

##### 4.持续时间组的阈值

我们也可以为每个组设置阈值。此代码具有针对单独请求和批量请求的组。对于每个组，都有不同的阈值。

```javascript
import http from 'k6/http';
import { group, sleep } from 'k6';

export const options = {
  thresholds: {
    'group_duration{group:::individualRequests}': ['avg < 400'],
    'group_duration{group:::batchRequests}': ['avg < 200'],
  },
  vus: 1,
  duration: '10s',
};

export default function () {
  group('individualRequests', function () {
    http.get('https://test-api.k6.io/public/crocodiles/1/');
    http.get('https://test-api.k6.io/public/crocodiles/2/');
    http.get('https://test-api.k6.io/public/crocodiles/3/');
  });

  group('batchRequests', function () {
    http.batch([
      ['GET', `https://test-api.k6.io/public/crocodiles/1/`],
      ['GET', `https://test-api.k6.io/public/crocodiles/2/`],
      ['GET', `https://test-api.k6.io/public/crocodiles/3/`],
    ]);
  });

  sleep(1);
}
```

#### 超过阈值时中止测试

如果在测试过程中，我们想要在阈值不满足时中止测试，那么可以使用 `abortOnFail` 属性。

将 abortOnFail 属性设置为 true。当您设置 abortOnFail 时，一旦阈值失败，测试运行就会停止。

> 这里也会有一种特殊情况，测试可能会因为这个阈值的设定导致在测试生成重要数据之前中止。为了防止这些情况，我们可以使用 delayAbortEval 延迟 abortOnFail。在此脚本中，abortOnFail 延迟了十秒。十秒后，如果未达到 p(99) < 10 阈值，测试将中止。

```javascript
export const options = {
  thresholds: {
    metric_name: [
      {
        threshold: 'p(99) < 10', // string
        abortOnFail: true, // boolean
        delayAbortEval: '10s', // string
        /*...*/
      },
    ],
  },
};
```

更多阈值的内容，请参考官方文档：[https://k6.io/docs/using-k6/thresholds/](https://k6.io/docs/using-k6/thresholds/)

### Test lifecycle 测试生命周期

K6 框架中的测试的生命周期，测试脚本始终都以下面的相同顺序进行执行：

- `init` 初始化阶段：上下文中的代码准备脚本、加载文件、导入模块并定义测试`生命周期函数`。必需的。
- `setup` 前置准备设置阶段：设置测试环境并生成数据。可选的。
- `VU` UV 阶段：代码在 default 或场景函数中运行，运行时间和次数与 options 定义的一样长。必需的。
- `teardown` 后置测试退出阶段：对数据进行后处理并关闭测试环境。可选的。

> 生命周期函数：除了初始化代码之外，每个阶段都在生命周期函数中发生，这是在 k6 运行时按照特定顺序调用的函数。

下面是一个完整的测试生命周期示例：

```javascript
// 1. 配置 init 阶段（必需的）

export function setup() {
  // 2. 配置 setup 阶段（可选的）
}

export default function (data) {
  // 3. 配置 VU 阶段（必需的）
}

export function teardown(data) {
  // 4. 配置 teardown  阶段（可选的）
}
```

#### 生命周期阶段概述

| 测试阶段    |目的  | 示例             | 请求次数 |
| -------------- | ------ | ---------------- | ------ |
| init 初始化阶段 | 加载本地文件、导入模块、声明生命周期函数 | 打开 JSON 文件，导入模块 | 每个 VU 一次* |
| Setup 前置准备配置阶段 | 设置要处理的数据，在 VU 之间共享数据 | 调用 API 启动测试环境 | 一次 |
| VU code VU 代码阶段 | 运行测试函数，通常是 default| 发出 https 请求，验证响应 | 每次迭代一次，根据测试选项的需要进行多次 |
| Teardown 测试后置退出阶段 | 设置代码的处理结果，停止测试环境 | 验证设置是否有一定的结果，发送 webhook 通知测试已完成 | 一次 **|

> `*` 在云脚本中，init 代码可能会被更频繁地调用。`**` 如果 Setup 函数异常结束（例如抛出错误），则不会调用 teardown() 函数。考虑向 setup() 函数添加逻辑以处理错误并确保正确清理。

#### init 初始化阶段

K6 测试的必要阶段。这个阶段用来在测试之前准备测试环境和初始化测试条件

> init 上下文中的代码每个 VU 都会运行一次。

一般在`init` 阶段可能会做的事情：

- 导入模块
- 从本地文件系统加载文件
- 为所有 options 配置测试
- 为 VU、setup 和 teardown 阶段（以及自定义或 handleSummary() 函数）定义生命周期函数。

> init 上下文中的代码始终首先执行

#### VU 阶段

VU 阶段是测试的核心。在这个阶段，代码在 default 或场景函数中运行，运行时间和次数与 options 定义的一样长。

关于 UV 阶段的 Q&A：

- 1.为什么有 VU 阶段？

  - VU 阶段是测试的核心，脚本必须至少包含一个定义 VU 逻辑的场景函数。该函数内部的代码是 VU 代码。
  - VU 阶段是真正的测试代码，所以 VU 阶段的代码会被多次执行，执行次数由 options 定义的一样长。
- 2.为什么把 init 阶段和 VU 阶段分开
  - 将 init 阶段与 VU 阶段分离，可以消除 VU 代码中不相关的计算，从而提高 k6 性能并使测试结果更加可靠。init 代码的一个限制是它无法发出 HTTP 请求。此限制确保 init 阶段在测试中可重现（协议请求的响应是动态且不可预测的）
  - 将 init 阶段与 VU 阶段分离，可以使 VU 阶段的代码更加简洁，更加专注于测试逻辑。
- 3.UV 阶段的默认函数生命周期的理解
  - VU 从头到尾依次执行 default() 函数。一旦 VU 到达函数末尾，它就会循环回到开头并重新执行代码
  - 作为此“重新启动”过程的一部分，k6 会重置 VU。Cookie 被清除，TCP 连接可能被断开（取决于我们的测试配置选项）。

#### Setup 测试前置准备配置阶段 和 teardown 测试后置退出阶段

Setup 和 teardown 阶段是可选的。这两个阶段都是在 VU 阶段之前和之后运行的。

与 default 一样，setup 和 teardown 函数必须是导出函数。但与 default 函数不同，k6 每次测试仅调用 setup 和 teardown 一次。

- setup 在测试开始时调用，在 init 阶段之后但在 VU 阶段之前。
- teardown 在测试结束时、VU 阶段（default 函数）之后调用。
- 与 init 阶段不同，您可以在设置和拆卸阶段调用完整的 k6 API

更多 K6 测试生命周期的内容，请参考官方文档：[https://k6.io/docs/using-k6/test-life-cycle/](https://k6.io/docs/using-k6/test-life-cycle/)

### Scenarios 测试场景

在 K6 的测试脚本中，可以定义多个测试场景，每个场景都可以有自己的配置项，例如 VU 数量、持续时间等。

测试场景可以详细配置 VU 和迭代计划的方式。通过测试场景配置，我们可以在性能测试中对不同的工作负载或流量模式进行更好的根据业务进行自定义。

使用测试场景配置的好处：

- 更简便、更灵活的测试组织方式。您可以在同一个脚本中定义多个测试场景，每个场景可以独立执行不同的 JavaScript 函数。
- 模拟更真实的流量情况。每个测试场景都可以使用不同的虚拟用户（VU）和迭代调度模式，由专门设计的执行器提供支持。
- 并行或顺序工作负载。各个场景相互独立并行运行，尽管可以通过仔细设置每个场景的 startTime 属性使它们看起来像是按顺序运行的。
- 细致入微的结果分析。可以为每个场景设置不同的环境变量和指标标签。

#### 测试场景配置

我们可以使用代码中的 options 对象中的 scenarios 键值来配置具体场景方案。也可以为场景指定任意名称，只要脚本中的每个场景名称都是唯一的即可。

场景配置示例：

```javascript
export const options = {
  scenarios: {
    example_scenario: {
      // 使用的执行器名称
      executor: 'shared-iterations',

      // 常规的场景配置
      startTime: '10s',
      gracefulStop: '5s',
      env: { EXAMPLEVAR: 'testing' },
      tags: { example_tag: 'testing' },

      // 与执行器相关的特殊配置
      vus: 10,
      iterations: 200,
      maxDuration: '10s',
    },
    another_scenario: {
      /*...*/
    },
  },
};
```

#### 测试场景执行器

对于每个 k6 场景，VU（虚拟用户）的工作负载由执行器进行调度。执行器配置测试运行的持续时间、流量是否保持恒定或变化，以及工作负载是由 VU 还是到达率（即开放或关闭模型）建模的。

我们设置的测试场景对象必须定义 executor 属性，并选择其中一个预定义的执行器名称。您选择的执行器将决定 k6 如何对负载进行建模。可选项包括：

- 按迭代次数。
  - shared-iterations 在 VU 之间共享迭代。
  - per-vu-iterations 让每个 VU 运行配置的迭代。

- 按 VU 数量。
  - constant-VUs 以恒定数量发送 VU。
  - ramping-vus 根据您配置的阶段增加 VU 数量。

- 按迭代率。
  - constant-arrival-rate 以恒定速率开始迭代。
  - ramping-arrival-rate 根据您配置的阶段提高迭代率。

除了这些通用场景选项之外，每个执行程序对象还具有特定于其工作负载的其他选项，可以点击[执行者](https://grafana.com/docs/k6/latest/using-k6/scenarios/executors)获取更多

#### 测试场景配置选项

| 选项名称       | 类型   | 描述             | 默认值 |
| -------------- | ------ | ---------------- | ------ |
| executor(必填) | string | 唯一的执行者名称 | -     |
| startTime |  string |  自测试开始以来的时间偏移，此时该场景应开始执行。| "0s"|  
| gracefulStop |  string|  在强行停止迭代之前等待迭代完成执行的时间。要了解更多信息，请阅读优雅停止。|  "30s"|  
|  exec |  string |  要执行的导出 JS 函数的名称。|  "default"|  
|  env |  object|  此场景特定的环境变量。| {}|  
|  tags |  object |  特定于此场景的标签。| {}|  

#### 测试场景示例

测试场景的 demo 脚本 会结合两种场景并按顺序执行：

- shared_iter_scenario 立即启动。10 个 VU 尝试尽快使用 100 次迭代（某些 VU 可能比其他 VU 使用更多迭代）。
- per_vu_scenario 在 10 秒后开始。在这种情况下，十个 VU 每个运行十次迭代。

示例代码如下：

```javascript
import http from 'k6/http';

export const options = {
  scenarios: {
    shared_iter_scenario: {
      executor: 'shared-iterations',
      vus: 10,
      iterations: 100,
      startTime: '0s',
    },
    per_vu_scenario: {
      executor: 'per-vu-iterations',
      vus: 10,
      iterations: 10,
      startTime: '10s',
    },
  },
};

export default function () {
  http.get('https://test.k6.io/');
}
```

运行场景 demo 脚本，可以看到如下结果：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/zLDexk.png)

观看测试结果，你会发现配置了场景的测试结果中，除了常规的测试结果外，k6 输出将包含有关 demo 场景的 详细结果信息 (shared_iter_scenario 场景和 per_vu_scenario 场景的很详细的指标信息)。

更多关于测试场景的内容，请参考官方文档：[https://k6.io/docs/using-k6/scenarios/](https://k6.io/docs/using-k6/scenarios/)

## 如何快速编写 K6 性能测试脚本

我们除了可以使用 JavaScript 编写 K6 性能测试脚本外，K6 还提供了多种快捷的方式来编写性能测试脚本。

- 1.使用 K6 提供的 Test builder 测试生成器工具来编写脚本
- 2.使用 K6 Recorder 录制器录制脚本
- 3.使用 浏览器开发者工具获取 HAR 文件后使用 har-to-k6 工具将 HAR 文件转换为 K6 脚本

下面将分别介绍这三种方式。

### 使用 K6 提供的 Test builder 测试生成器工具来编写脚本

k6 的 Test builder 测试生成器提供了一个图形界面，可根据您的输入生成 k6 测试脚本。然后，您可以复制测试脚本并从 CLI 运行测试。

> Test builder 测试生成器目前还是一个实验性的功能，可能会在未来的版本中发生变化。大家可以查看官方文档：[https://k6.io/docs/using-k6/test-builder/](https://k6.io/docs/using-k6/test-builder/)获取更多信息

#### 安装 Test builder 测试生成器

Test builder 不需要安装，它是 Grafana Cloud k6 提供的一个功能，可以在浏览器中使用。

需要注册一个 Grafana Cloud k6 账号，然后登录 Grafana Cloud。

如何进入 Test builder 测试生成器界面：

- 登录进入 Grafana Cloud 首页

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/66TXQ3.png)

- 依次点击左侧菜单栏上的 Testing & synthetics--->Performance--->Projects
- 然后选择 default project 或者新建一个 project，进入到项目的详情页面
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/Ynx49y.png)
- 点击页面上的 Start testing 按钮，然后再选择页面下的 Test builder，进入到 Test builder 测试生成器界面
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/GgzyK7.png)

> 提醒：由于 Test builder 测试生成器是 Grafana Cloud 上登录进行使用，可能 Grafana Cloud 存储一些敏感数据，所以建议大家不要在生产环境中使用 Test builder 测试生成器。

#### 如何使用 Test builder 测试生成器

- 1.在 Test builder 测试生成器界面，点击 Scenario_1 下的 Options 按钮进入到配置页面，配置测试场景的基本信息，如下图所示：
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/JvABl9.png)

> 可以看到场景配置页面提供了多种配置选项，可以根据自己的需求进行配置场景名称，执行器类型和不同的 UV 配置。

- 2.在 Test builder 测试生成器界面，点击 Scenario_1 下的 Requests 按钮进入到 Requests 管理页面，如下图所示：
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/ohtOQD.png)

- 3.点击页面下的 Request 按钮进入添加请求页面，如下图所示：
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/BFSEME.png)

- 4.在添加请求页面，输入请求的 URL 地址，再根据实际情况添加请求的 headers 或请求的 body 或检查点等参数，然后点击页面上的 Create 按钮，完成性能场景的配置，如下图所示：
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/inCNCz.png)

#### 获取 Test builder 测试生成器生成的脚本

在 Test builder 测试生成器界面，点击页面上的 Script 按钮，页面就会展示出 Test builder 测试生成器生成的脚本，如下图所示：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/rh3Qfr.png)

> 可以看到 Test builder 测试生成器生成的脚本，是一个完整的 K6 测试脚本，可以直接复制到本地，然后使用 k6 运行该脚本。

#### 运行 Test builder 测试生成器生成的脚本

在 Test builder 测试生成器界面，点击页面上的 Run Test 按钮，页面就会展示出 Test builder 测试生成器生成的脚本的运行结果，如下图所示：

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/yFuEyu.png)

> 可以看到 Test builder 测试生成器生成的脚本运行的很详细的测试结果信息。

#### 其他 Test builder 测试生成器的功能

- 也支持导入 HAR 文件生成测试脚本
- 也支持多个 scenario 场景的配置和一个 scenario 场景的多个请求的配置

更多关于 Test builder 测试生成器的内容，请参考官方文档：[https://grafana.com/docs/grafana-cloud/k6/author-run/test-builder/](https://grafana.com/docs/grafana-cloud/k6/author-run/test-builder/)

### 使用 K6 Recorder 录制器录制脚本

K6 Recorder 录制器是 K6 提供的一个浏览器扩展程序，可以在浏览器中录制用户与 Web 应用程序的交互，并将其转换为 k6 测试脚本。

#### 安装 K6 Recorder 录制器

K6 Recorder 录制器是一个浏览器扩展程序，可以在 Chrome 或 Firefox 中使用。您可以从 Chrome Web Store 或 Firefox Add-ons 页面安装它。

- Chrome Web Store 安装地址：[https://chrome.google.com/webstore/detail/grafana-k6-browser-record/fbanjfonbcedhifbgikmjelkkckhhidl](https://chrome.google.com/webstore/detail/grafana-k6-browser-record/fbanjfonbcedhifbgikmjelkkckhhidl)

- Firefox Add-ons 安装地址：[https://addons.mozilla.org/en-US/firefox/addon/grafana-k6-browser-recorder/](https://addons.mozilla.org/en-US/firefox/addon/grafana-k6-browser-recorder/)

安装完成后，就可以在浏览器中使用 K6 Recorder 录制器了。

#### 如何使用 K6 Recorder 录制器

- 1. 在浏览器上点击打开 k6 Recorder 录制器扩展。
- 2. 选择保存自动生成的脚本的位置。
  - 要将其保存在本地计算机上，请选择"我不想在云中保存测试"(后面的例子我选择的这个选项)。
  - 要将其保存到任何 Grafana Cloud k6 项目中，请选择“登录”。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/yj75Ef.png)
- 3. 选择保存脚本位置后，在当前浏览器选项卡输入测试网站地址，点击选择开始录制按钮以开始录制当前浏览器选项卡。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/6NjHGS.png)

![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/KFMDWX.png)

> 图中我打开了谷歌的首页并点击了搜索框，输入了 123，然后点击了搜索按钮，

- 4. 点击了 k6 Recorder 录制器的停止录制按钮停止录制。
- 5. 将录制的文件取名保存在本地（我这里取名为 record-demo.har）。
- 6. 使用 har-to-k6 工具将 HAR 文件转换为 K6 脚本。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/2nRtpW.png)

> har-to-k6 工具是一个命令行工具，可以将 HAR 文件转换为 k6 脚本。需要先通过 `npm install -g har-to-k6`安装 har-to-k6 工具，然后通过 `har-to-k6 record-demo.har -O record-demo.js`命令将 HAR 文件转换为 K6 脚本。

- 7. 转换后的 K6 脚本部分截图如下所示：
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/ldC2kl.png)

- 8. 大家可以根据自己的需求对转换后的 K6 脚本进行修改，然后使用 k6 运行该脚本。
- 9. 使用 k6 运行转换后的 K6 脚本，查看运行结果。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/jUpYWj.png)

更多关于 K6 Recorder 录制器的内容，请参考官方文档：[https://grafana.com/docs/k6/latest/using-k6/test-authoring/create-tests-from-recordings/using-the-browser-recorder/](https://grafana.com/docs/k6/latest/using-k6/test-authoring/create-tests-from-recordings/using-the-browser-recorder/)

### 使用浏览器开发者工具和 har-to-k6 工具生成 K6 脚本

除了我们可以使用 K6 Recorder 录制器来录制脚本外，我们还可以使用浏览器开发者工具获取测试请求的 HAR 文件，然后使用 har-to-k6 工具转换 HAR 文件来生成 K6 脚本。

#### 可以获取 HAR 文件的浏览器和工具

我们可以根据实际情况选择一个工具来记录 HAR 文件。市面上的很多浏览器和工具可以以 HAR 格式导出 HTTP 流量。大家常用的是：

- Chrome 浏览器
- Firefox 浏览器
- Microsoft Edge 浏览器
- Charles 代理抓包工具 (HTTP proxy/recorder)
- Fiddler 代理抓包工具 (HTTP proxy/recorder)

#### 如何使用浏览器开发者工具获取 HAR 文件

下面是使用 Chrome 浏览器开发者工具获取测试请求 HAR 文件例子：

- 在 Chrome 中打开新的隐身窗口。 （可以排除登录 cookies 等干扰信息）。
- 打开 Chrome 开发者工具（按 F12）。
- 选择网络选项卡 Network。
- 检查和确认录音按钮（圆形按钮）是否已激活（红色）。
- 如果想要记录多个连续的页面加载，请选中“保留日志”复选框。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/1RDeqJ.png)

- 输入测试网站的 URL（如 <https://www.google.com/>），然后开始执行和后续模拟用户执行的操作（如输入 123 进行搜索）。

- 完成后，在 Chrome 开发人员工具中，右键单击 URL 并选择“将内容另存为 HAR”。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/WBsOXl.png)

- 选择保存 HAR 文件的位置并重命名（如 har-demo），然后点击保存按钮，完成 HAR 文件的保存。

#### 使用 har-to-k6 进行转换 HAR 文件

- 1. 安装 har-to-k6 工具

  - 通过 `npm install -g har-to-k6`命令安装 har-to-k6 工具。

- 2. 使用 har-to-k6 工具将 HAR 文件转换为 K6 脚本

  - 通过 `har-to-k6 har-demo.har -O har-demo.js`命令将 HAR 文件转换为 K6 脚本。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/UIKobM.png)

- 3. 转换后的 K6 脚本部分截图如下所示：
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/1OWWG0.png)

- 4. 大家可以根据自己的需求对转换后的 K6 脚本进行修改，然后使用 k6 运行该脚本。
- 5. 使用 k6 运行转换后的 K6 脚本，查看运行结果。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/9BLD7D.png)

更多关于 HAR 文件的内容，请参考官方文档：[https://grafana.com/docs/k6/latest/using-k6/test-authoring/create-tests-from-recordings/using-the-har-converter/](https://grafana.com/docs/k6/latest/using-k6/test-authoring/create-tests-from-recordings/using-the-har-converter/)

## 进阶

### 输出 html 报告

通过之前的 K6 的默认测试报告来看，K6 本身只能输出命令行的报告，没有图形化界面的测试报告。

如果我们想要生成图形化界面的测试报告，可以使用第三方提供的 K6 HTML Report Exporter v2 插件来生成 html 报告。

下面是使用 K6 HTML Report Exporter v2 插件来生成 html 报告的步骤：

- 1. 在测试脚本中引入 K6 HTML Report Exporter v2 插件

```javascript
import { htmlReport } from "https://raw.githubusercontent.com/benc-uk/k6-reporter/main/dist/bundle.js";
```

- 2. 在测试脚本中配置 K6 HTML Report Exporter v2 插件

```javascript
export function handleSummary(data) {
  return {
    "summary.html": htmlReport(data),
  };
}
```

- 3. 完整的测试脚本示例

```javascript
import { check } from 'k6';
import http from 'k6/http';
import { htmlReport } from "https://raw.githubusercontent.com/benc-uk/k6-reporter/main/dist/bundle.js";


export default function () {
  const res = http.get('https://httpbin.test.k6.io');
  check(res, {
    'HTTP response code is status 200': (r) => r.status === 200,
  });
}

export function handleSummary(data) {
  return {
    "summary.html": htmlReport(data),
  };
}
```

- 4. 使用 k6 运行测试脚本即可在项目根目录生成名称为 summary.html 的 html 报告

- 5. 打开 summary.html 报告即可查看 html 报告。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/tty2Zs.png)

更多关于 K6 HTML Report Exporter v2 插件的用法，请参考官方文档 https://github.com/benc-uk/k6-reporter[https://github.com/benc-uk/k6-reporter]

### 持续集成

#### 接入 github action

以 github action 为例，其他 CI 工具类似

- 创建.github/workflows 目录：在你的 GitHub 仓库中，创建一个名为 .github/workflows 的目录。这将是存放 GitHub Actions 工作流程文件的地方。

- 创建工作流程文件：在.github/workflows 目录中创建一个 YAML 格式的工作流程文件，例如 k6.yml。

- 编辑 k6.yml 文件：将以下内容复制到文件中

```yml
name: K6 Performance Test
on: [push]
jobs:
  build:
    name: Run k6 test
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Run k6 local test
        uses: grafana/k6-action@v0.3.1
        with:
          filename: demo.js
          flags: --vus 50 --duration 10s
```

- 提交代码：将 k6.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 K6 Performance Test 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/NlOiHp.png)

- 我们也通过 github action 输出 html 报告，先调整一下 k6.yml 文件

```yml
name: K6 Performance Test
on: [push]
jobs:
  build:
    name: Run k6 performance test
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Run k6 local test
        uses: grafana/k6-action@v0.3.1
        with:
          filename: demo.js
          flags: --vus 50 --duration 10s
      - name: Archive K6 performance test report
        uses: actions/upload-artifact@v3
        with:
          name: K6-performance-test-report
          path: summary.html
      - name: Upload K6 performance test report to GitHub
        uses: actions/upload-artifact@v3
        with:
          name: K6-performance-test-report
          path: summary.html
```

- 提交代码：将 k6.yml 文件添加到仓库中并提交。
- 查看测试报告：在 GitHub 中，导航到你的仓库。单击上方的 Actions 选项卡，然后单击左侧的 K6 Performance Test 工作流。你应该会看到工作流正在运行，等待执行完成，就可以查看结果和测试报告附件。
![ ](https://cdn.jsdelivr.net/gh/naodeng/blogimg@master/uPic/sFCarY.png)

### Options 配置选项

K6 的选项配置是来通过不同选项来配置测试运行行为。例如，选项是如何定义测试标签、阈值、用户代理以及虚拟用户和迭代的数量。

#### 如何使用配置选项

## 参考资料

- [K6 官方文档：https://k6.io/docs/](https://k6.io/docs/)
- [官方网站：https://k6.io/](https://k6.io/)
