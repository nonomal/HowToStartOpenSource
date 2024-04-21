---
title: 如何给GitHub-Pages绑定自定义域名
date: 2022-07-27 19:54:27
---

现在越来越多的开发者选择基于 GitHub Pages 构建自己的网站，GitHub Pages 的默认访问方式为 `{username}.github.io`，而如果你凑巧，还有一个个人域名，那么其实还可以将自己自定义的域名 CNAME 到 GitHub 默认的访问域名，这样就能实现，基于自己的个性化域名，访问 GitHub Pages 的能力了，或者说得更彻底点，在建个人站点这件事儿上，与 GitHub 的结合，你只需要凑一个域名就能搞定了。

有同学对于如何将个人域名绑定到 GitHub Pages 不太了解，本文就来讲讲，如何操作。

关于如何借助 GitHub Pages 建立个人站点，我的模板项目 [vdoing-template](https://github.com/eryajf/vdoing-template) 已经详细介绍过，就不再赘述。

接下来只需要两步配置就可以完成这个操作。

首先来到 GitHub 当中，在 `Settings` --> `Pages` 中添加`CNAME:`

![image_20220727_200747](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220727_200747.png)

然后在个人的域名解析处，添加一条 CNAME 记录：

![image_20220727_200900](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220727_200900.png)

然后回到 GitHub 配置页面，查看检查是否成功。成功之后，使用 http://pages.eryajf.net 就可以访问网站了。

---

`注意：`目前看来，貌似不支持子路由的配置，比如你无法配置 `test.eryajf.net` 解析到 `eryajf.github.io/test`。
