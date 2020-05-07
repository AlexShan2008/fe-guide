# 热云官网需求开发及上线部署流程

## 需求评审，项目排期

- 可行性研究
- 工期确定

## 代码开发

- 功能开发需要新建`feat-*` 分支进行开发，如只是静态资源或者文案的更改可以在dev分支直接开发
- 开发完成后提交`merge request` 到`dev`分支
- 经他人review后，合并到dev分支
- 本地打包后测试，本地打包测试通过后，将打包的代码提交到运维相关人员

- 本地测试流程：(本地开启静态服务器)

```shell
cd root 
yarn export 
cd out

http-server --port 3000

```

## 发布

- 发布到测试环境 webtest.reyun.com
- 发布上线邮件到运维相关人员(刘诏旭 liuzhaoxu@reyun.com，抄送相关产品经理及shantong@reyun.com)，并钉钉通知运维及产品。
- 测试环境通过后发布到正式环境。

> Tips:

1. 由于官网生产环境有`CDN`加速，所以代码更新后有大概两个小时的延迟时间。
2. 可以访问 http://www.reyun.com.s3-website.cn-north-1.amazonaws.com.cn/
进行需求验证。
