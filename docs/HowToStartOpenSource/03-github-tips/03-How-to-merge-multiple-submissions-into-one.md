---
title: 如何将多次提交合并为一次
date: 2022-07-18 17:20:41
---

我们作为协同者，可能会修改多次在同一个 PR 上，这个时候项目的 owner 可以选择压缩合并，不过作为协作者，我们应该有这种自觉，在认为代码没问题的时候，主动将多次提交合并为一次。

可以通过 rebase 进行合并，操作步骤如下，比如刚刚那次在协作者 lql95 的视角已经提交了两次，我们现在再进行一次提交：

```sh
$ echo 'test info' > test.txt
$ git add .
$ git commit 'add test file'
$ git push
```

这次提交之后，这个 PR 就有了三次提交，我们自己在本地做如下处理。

首先查看一下提交历史：

```sh
$ git log
commit 55e307a11369a3238d908344fea39b91d32d229f (HEAD -> main, origin/main, origin/HEAD)
Author: lql95 <eryajf@gmail.com>
Date:   Tue May 31 22:21:10 2022 +0800

    add test file

commit 0d61a99c31b2dced4fb9b1e1edfc74585571c909
Author: lql95 <eryajf@gmail.com>
Date:   Tue May 31 21:53:44 2022 +0800

    删除无用内容

commit 5c575c34b0351750510abef7ce6734b8914f951f
Author: lql95 <eryajf@gmail.com>
Date:   Tue May 31 21:44:39 2022 +0800

    以lql95的视角协同维护项目

commit 421212d25e6062dc0d15173304762056dbb3e583
Merge: 85630a4 c2cf945
Author: 二丫讲梵 <Linuxlql@163.com>
Date:   Tue May 31 21:29:58 2022 +0800

    Merge pull request #1 from eryajf/test
```

比如这里要将最新的三次提交合并，可以运行如下命令：

```sh
$ git rebase -i <421212d> # -i后面的参数为最后一个不需要合并的Commit，这里为Commit 1
```

执行之后，将会进入一个交互界面，内容如下：

![image_20220718_172053](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220718_172053.png)

我们把后两个 pick 改成 squash，改后如下：

![image_20220718_172104](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220718_172104.png)

这里两个关键字的含义为：

- pick 表示其他的提交将会合并到这一次提交上
- squash 表示将对应标识的提交合并到 pick 选择的那次 commit 上。

保存之后，进入一个新的交互页面，这个页面是填写提交信息的，可保持默认，然后保存，就合并成功了：

![image_20220718_172112](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220718_172112.png)

通过查看状态，也能看到此时的状态详情：

```sh
* dc38fb2 (HEAD -> main) 以lql95的视角协同维护项目
| * 55e307a (origin/main, origin/HEAD) add test file
| * 0d61a99 删除无用内容
| * 5c575c3 以lql95的视角协同维护项目
|/
*   421212d Merge pull request #1 from eryajf/test
|\
| * c2cf945 test
|/
* 85630a4 Create README.md
```

当然在 vscode 中也能够清晰地看到变化：

![image_20220718_172123](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220718_172123.png)

最后将这次调整 push 到远程即可，因为这次的本地调整，导致本地落后于远程，所以需要进行强推：

```sh
$ git push -f origin main
```

此时再去到 eryajf 主视角看刚刚那次 PR，就可以看到提交次数只有一次了：

![image_20220718_172134](https://cdn.jsdelivr.net/gh/eryajf/tu/img/image_20220718_172134.png)

当然，这里主要是为了体验整个压缩提交的流程，实际上开发过程中，并不需要这步操作，项目的 owner 在处理 PR 的时候可以直接选择压缩合并，也就不会将多次提交合并上去了。
