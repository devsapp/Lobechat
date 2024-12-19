
> 注：当前项目为 Serverless Devs 应用，由于应用中会存在需要初始化才可运行的变量（例如应用部署地区、函数名等等），所以**不推荐**直接 Clone 本仓库到本地进行部署或直接复制 s.yaml 使用，**强烈推荐**通过 `s init ${模版名称}` 的方法或应用中心进行初始化，详情可参考[部署 & 体验](#部署--体验) 。

# lobechat 帮助文档

<description>

本项目快速创建并部署 LobeChat 应用到阿里云云原生应用平台 CAP 。

</description>


## 前期准备

使用该项目，您需要有开通以下服务并拥有对应权限：

<service>



| 服务/业务 |  权限  | 相关文档 |
| --- |  --- | --- |
| 函数计算 |  AliyunFCFullAccess | [帮助文档](https://help.aliyun.com/product/2508973.html) [计费文档](https://help.aliyun.com/document_detail/2512928.html) |
| 云数据库RDS |  AliyunRDSFullAccess | [帮助文档](undefined) [计费文档](undefined) |
| 专有网络 |  AliyunFCServerlessDevsRolePolicy | [帮助文档](https://help.aliyun.com/zh/vpc) [计费文档](https://help.aliyun.com/zh/vpc/product-overview/billing) |

</service>

<remark>



</remark>

<disclaimers>



</disclaimers>

## 部署 & 体验

<appcenter>
   
- :fire: 通过 [云原生应用开发平台 CAP](https://devs.console.aliyun.com/applications/create?template=lobechat) ，[![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://devs.console.aliyun.com/applications/create?template=lobechat) 该应用。
   
</appcenter>
<deploy>
    
   
</deploy>

## 案例介绍

<appdetail id="flushContent">

本项目基于开源 [LobeChat](https://github.com/lobehub/lobe-chat)，简化 LobeChat 应用的初始化搭建过程，快速部署到阿里云云原生应用平台 CAP。

> 说明：当前只支持 LobeChat 的社区版，商业版暂不支持

FastGPT 是一个基于 LLM 大语言模型的知识库问答系统，提供开箱即用的数据处理、模型调用等能力。同时可以通过 Flow 可视化进行工作流编排，从而实现复杂的问答场景！

LobeChat 核心能力：
1. **开源与高性能**：LobeChat 基于开源协议，允许任何人查看、修改和使用其源代码。同时，它采用了高效的架构设计，确保机器人能够快速响应用户请求。
2. **多模态交互**：除了传统的文本交互外，LobeChat 还支持语音合成和语音识别功能，让机器人能够更自然地与人类进行交流。此外，它还支持文本转图像等创意功能，为用户带来全新的交互体验。
3. **可扩展插件系统**：LobeChat 拥有一个庞大的插件市场，用户可以通过安装插件来扩展机器人的功能。无论是学术搜索、游戏娱乐还是日常生活助手，你都能在插件市场中找到合适的选择。
4. **多平台支持**：LobeChat 兼容多家知名AI服务提供商（如OpenAI、Claude、Qwen、Gemini等），使得用户能够轻松接入不同的AI模型和服务。

> **注意**：开源 LobeChat 默认使用 OpenAI 的模型。**在本项目中，将使用 Qwen 模型作为默认模型，在部署前需要准备 Qwen API KEY，需要到百炼控制台创建 & 获取，说明文档：https://help.aliyun.com/zh/model-studio/apikey?spm=a2c4g.11186623.0.i20**


说明：在本项目中，有 Base 和 Database 两个版本可供选择选择，区别如下：
| 版本 |  Base 版本  | Database 版本 |
| --- |  --- | --- |
| 鉴权能力 |  不支持，统一为社区版用户 | 支持三方鉴权，本项目中采用 Auth0 作为三方鉴权平台 |
| 知识库 |  不支持 | 支持 |
| 上传文件 / 文件夹 |  不支持 | 支持 |


## 项目架构图

![](https://img.alicdn.com/imgextra/i2/O1CN01K6LJ1123RTHz5HkJT_!!6000000007252-0-tps-1128-506.jpg
)
## 项目接入点
项目部署成功后，您需要访问 LobeChat 服务的域名地址，就可以打开并使用 LobeChat 了

LobeChat 访问入口：`${resources.lobechat.output.customDomain.domainName}`

</appdetail>

## 使用流程

<usedetail id="flushContent">

### 部署 Database 版本 LobeChat

**一、鉴权准备**：注册并登录 [Auth0](https://manage.auth0.com/dashboard/us/dev-34fdqfx8mrw0s8t2/)平台
  1. 新增Auth0用户：点击左侧导航栏的「Users Management」，进入用户管理界面，可以为你的组织新建用户，用以登录 LobeChat。![](https://img.alicdn.com/imgextra/i4/O1CN01znpbaB1It9HRkcK69_!!6000000000950-0-tps-2021-646.jpg)
  2. 创建应用：点击左侧导航栏的「Applications」，切换到应用管理界面，点击右上角「Create Application」以创建应用。填写你想向组织用户显示的应用名称，可选择任意应用类型，点击「Create」。![](https://img.alicdn.com/imgextra/i4/O1CN014zX5ya1HDdlmiF6jC_!!6000000000724-0-tps-2083-510.jpg)
![](https://img.alicdn.com/imgextra/i2/O1CN01vSHTQy1J3DzgyRCH9_!!6000000000972-0-tps-864-779.jpg)

3. 应用创建成功后，进入应用界面，需要在「Settings」中获取以下鉴权信息：`Domain` `Client ID` `Client Secret` ，用于部署时填写参数![](https://img.alicdn.com/imgextra/i1/O1CN01ENbLVC1unbtK4eOWf_!!6000000006082-0-tps-1245-700.jpg)
 **二、部署项目**：在 LobeChat 项目部署控制台，您需要给 Web 服务（本项目中名为 LobeChat 的服务）配置如下参数：
   1. 步骤一中获取到的鉴权信息 `Domain` `Client ID` `Client Secret` ，以及 `NEXT_AUTH_SECRET`，用于加密 Auth.js 会话令牌的密钥，可以用 
 `openssl rand -base64 32` 命令生成
   2. OSS 的 BucketName 和 Endpoint，如果没有，请到 [OSS](https://oss.console.aliyun.com/overview) 控制台获取
   3. 另外，为了保障数据库等敏感信息不被泄露，您需要填写  `KEY_VAULTS_SECRET` 参数，可以用 `openssl rand -base64 32` 命令生成
   部署完成之后，您可以看到系统返回给您的项目地址
 **四、配置 Auth0 Allowed Callback URLs**：返回 [Auth0 Applications](https://manage.auth0.com/dashboard/us/dev-34fdqfx8mrw0s8t2/applications)，在 「Application Settings」 页签下，找到 「Application URIs」，填写 「Allowed Callback URLs」，格式为 `https://[your-domain]/api/auth/callback/auth0`，其中 `[your-domain]` 部分替换为步骤二中返回项目地址的域名
**五、OSS 跨域配置**：登录 [OSS](https://oss.console.aliyun.com/overview) 控制台，进入目标 Bucket，在 「数据安全」页签下选择「跨域配置」，点击「创建规则」，配置如下参数
    | 参数名 |  说明  | 示例值 |
    | --- |  --- | --- |
    | 来源 |  项目部署成功后返回的项目地址 | https://xxxx.cn-hangzhou.fc.devsapp.net |
    | 允许 Methods |  允许跨域访问的请求方法 |  全选 |
    | 允许 Headers |  允许跨域访问的请求 Header 类型 |  * |

####  参数说明

| 参数名 |  说明  | 示例值 |
| --- |  --- | --- |
| 函数名称 |  只能包含字母、数字和中划线。不能以数字、中划线开头。长度在 1-128 之间。 | lobechat-abcd |
| OSS BucketName |  存储桶名称，到 OSS 控制台获取 | bucket-name |
| OSS Endpoint |  OSS 的地域节点，到 OSS 控制台获取 | oss-cn-hangzhou.aliyuncs.com |
| ACCESS_CODE |  添加访问 LobeChat 服务的密码，你可以设置一个长密码以防被爆破| lobechatxxxxxxxx |
| QWEN_API_KEY |  对应 Qwen 的 API KEY，需要到百炼控制台创建 & 获取，说明文档：https://help.aliyun.com/zh/model-studio/apikey?spm=a2c4g.11186623.0.i20| sk-xxxxxxxx |
| AUTH_AUTH0_ID | Auth0 应用程序的 Client ID，在 Auth0 中创建应用后获取| tAP2xxxxxxxxxok |
| AUTH_AUTH0_ISSUER| Auth0 应用程序的 Issuer URL，在 Auth0 中创建应用后获取| https://dev-34fdxxxxxxxx |
| AUTH_AUTH0_SECRET| Auth0 应用程序的 Client Secret，在 Auth0 中创建应用后获取| KHaxxxxxxxxcap |
| KEY_VAULTS_SECRET| 加密数据库等敏感信息的密钥，您可以使用以下命令生成密钥： openssl rand -base64 32|  wefxxxxxxxxxxxxx= |
| NEXT_AUTH_SECRET| 用于加密 Auth.js 会话令牌的密钥。您可以使用以下命令生成密钥： openssl rand -base64 32|  abcdxxxxxxxxxxxxx= |


### 部署 Base 版本 LobeChat

**部署项目**：在 LobeChat 项目部署控制台，您需要给 Web 服务（本项目中名为 LobeChat 的服务）配置 LobeChat 的访问码和 Qwen API KEY，点击立即部署。部署完成之后，您可以看到系统返回给您的项目地址

####  参数说明

| 参数名 |  说明  | 示例值 |
| --- |  --- | --- |
| 函数名称 |  只能包含字母、数字和中划线。不能以数字、中划线开头。长度在 1-128 之间。 | lobechat-abcd |
| ACCESS_CODE |  添加访问 LobeChat 服务的密码，你可以设置一个长密码以防被爆破| lobechatxxxxxxxx |
| QWEN_API_KEY |  对应 Qwen 的 API KEY，需要到百炼控制台创建 & 获取，说明文档：https://help.aliyun.com/zh/model-studio/apikey?spm=a2c4g.11186623.0.i20| sk-xxxxxxxx |


##  二次开发

具体的使用流程请参考 [LobeChat 快速上手官方教程](https://lobehub.com/zh/docs/usage/start?utm_source=cloud)

Q：如何构建安全的企业级应用呢？

A：推荐使用 LobeChat Databse 版本。如果想更改应用的身份验证方式，请参考 LobeChat 的身份验证文档：https://lobehub.com/zh/docs/usage/features/auth

Q：如何使用其他服务商的模型呢？

A：本项目中，所有模型默认使用通义的模型，如果您想使用其他服务商的模型，可以在名为 lobechat 服务所对应的函数的环境变量中填入对应模型的API KEY即可。具体环境变量写法以及支持的模型服务商请参考：https://lobehub.com/zh/docs/self-hosting/environment-variables/model-provider
> 注意：本项目托管的 LobeChat 当前默认使用 Qwen text-embedding-v3 模型，请确保你的 API Key 可以访问该模型。

Q: 如何使用最新版本的 LobeChat 或者进行更深层次的开发呢？

A: 如果您想做更高层次的二次开发或者想自行更新 LobeChat 版本， 请基于 [LobeChat](https://github.com/lobehub/lobe-chat) 的源码开发，然后打成镜像，将项目中 Web 服务中的镜像修改为您的自定义镜像即可。
> 注意：**在本项目中，LobeChat 的默认模型由 OpenAI 系列模型替换为 Qwen 系列模型**。如果想替换 LobeChat 中的默认模型，需要在 Web 服务（本项目中名为 LobeChat 的服务）的函数环境变量中，新增相应模型的 API KEY 变量，并将 LobeChat 源码中 `src/const/settings` 目录下文件中的默认模型替换成相应的模型 ID。境内的 region 推荐使用默认的 Dashscope 的 Base 地址，模型使用 Qwen 系列模型

</usedetail>

## 注意事项

<matters id="flushContent">
</matters>
