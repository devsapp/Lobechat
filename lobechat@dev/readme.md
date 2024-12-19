
> 注：当前项目为 Serverless Devs 应用，由于应用中会存在需要初始化才可运行的变量（例如应用部署地区、函数名等等），所以**不推荐**直接 Clone 本仓库到本地进行部署或直接复制 s.yaml 使用，**强烈推荐**通过 `s init ${模版名称}` 的方法或应用中心进行初始化，详情可参考[部署 & 体验](#部署--体验) 。

# FastGPT-CAP 帮助文档

<description>

本案例将 FastGPT 快速创建并部署到阿里云云原生应用平台 CAP 。

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
   
- :fire: 通过 [云原生应用开发平台 CAP](https://devs.console.aliyun.com/applications/create?template=FastGPT-CAP) ，[![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://devs.console.aliyun.com/applications/create?template=FastGPT-CAP) 该应用。
   
</appcenter>
<deploy>
    
   
</deploy>

## 案例介绍

<appdetail id="flushContent">

本案例是基于开源[FastGPT](https://github.com/labring/FastGPT)，简化 FastGPT 应用的初始化搭建过程，并且快速部署到阿里云云原生应用平台 CAP。

FastGPT 是一个基于 LLM 大语言模型的知识库问答系统，提供开箱即用的数据处理、模型调用等能力。同时可以通过 Flow 可视化进行工作流编排，从而实现复杂的问答场景！

FastGPT可以提供：

通过 Serverless 开发平台，您只需要几步，就可以体验 FastGPT，并享受 Serverless 架构带来的降本提效的技术红利。

## 项目架构图

## 项目接入点

</appdetail>

## 使用流程

<usedetail id="flushContent">

- 您需要给 FC 服务（本项目中名为FastGPT的服务）配置 MONGODB 的外网地址和 Dashscope 的 API_KEY，API_KEY 需要到百炼的控制台上去获取，说明文档：https://help.aliyun.com/zh/model-studio/apikey?spm=a2c4g.11186623.0.i20
- 部署完成之后，您可以看到系统返回给您的案例地址
- 直接使用浏览器打开案例地址
- 使用账号名`root`, 密码值为您部署时候填写的 `DEFAULT_ROOT_PSW` 参数值（默认为 123456）
- 之后具体的使用流程请参考[FastGPT快速上手官方教程](https://doc.fastai.site/docs/course/quick-start/)


##  二次开发

<!-- 如果您想要更加安全的部署， 可以 `MONGODB_URI` 和 `PG_URL` 使用内网地址， 并且白名单配置成 mongodb 和 pg 数据库所在的交换机网段， 同时给函数配置 vpcConfig 参数 （vpcId和vSwitchIds需要和数据库相同） -->
如果您想要更加安全的部署， 可以 `MONGODB_URI` 使用内网地址， 并且白名单配置成 mongodb，需要保证 pg 数据库和 mongodb 在同一个 VPC 下，并给函数服务绑定 Mongodb 和 PG 数据库所在的 VPC


如果您想做更高层次的二次开发， 请基于[FastGPT](https://github.com/labring/FastGPT)源码开发，然后将编译后的产物打包如该模版一样的zip包即可。

> 注意使用 `debian10`  `nodejs18` 环境构建

</usedetail>

## 注意事项

<matters id="flushContent">
</matters>
