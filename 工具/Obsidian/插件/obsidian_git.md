
通过这个插件的名称就可以猜到此插件和 Git 有关，事实确实如此。这个插件可以实现笔记的版本控制，并且让 Git 的操作图形化，更加简单，更加高效地实现 Git 的命令。当然我使用 Git 最重要的原因不是版本控制，而是实现同步。

在 Obsidian 中，所有的操作都是在本地进行的，一定程度上保护了用户的隐私，但是也造成了一个老大难的问题，即我在我笔记本上面记录的内容无法在别的地方查看。虽然 Obsidian 提供了同步的方案，但是要钱。奈何囊中羞涩，只好找寻他法。

作为一个经常写代码的，第一反应就是 GitHub，一个免费托管代码的平台。其实之前我就把我的笔记托管到 GitHub 平台上面过，所以自然而然就想到了它。上一次折腾 GitHub 是在我在社区里面买 L0 课程的时候，跟着教程成功地把自己的代码提交到了 Github 上面，后面就没怎么遇到问题了，也就没有继续去探索 Github，所以一开始我也不确定能否行得通。上周先把 GitHub 上的仓库克隆到了公司的电脑上，至少是可行的，今天又折腾了一番，把这个流程走通了，实现了在公司的电脑上拉取仓库的内容，并把修改提交到 GitHub 上。所以这篇笔记的重点不是 obsidian git 这个插件本身，而是如何配置 Git 及 GitHub，实现同步的目的。

## 基本流程

### 注册 Github 账号

在 GitHub 上注册账号，并创建仓库；

### 配置 Git 用户名和邮箱

下载 Git，配置用户名和邮箱；

### 生成 ssh key

在 Git 执行生成 ssh key 的命令，这一步是比较关键的，因为在 2021 年 8 月之后，Github 就不支持在 Git 中通过 Github 的账号和密码登录 Github。

生成 ssh key 的命令如下：

```bash
ssh-keygen -t rsa -C "your github email"
```

例如我的 GitHub 邮箱是 1815265375@qq.com，那么生成 ssh key 的命令则是：

```bash
ssh-keygen -t rsa -C "1815265375@qq.com"
```

生成的秘钥可以通过以下命令来查看：

```
cd ~/.ssh
ls -alh
cat id_rsa.pub
```

如下图所示：

![](Snipaste_2023-11-16_23-22-53.png)

### 在 Github 上添加公钥

在 Github 添加公钥，把生成的 ssh key 复制粘贴到 Github 上对应位置，即 Settings -> SSH and GPG keys -> New SSH key

![](add_ssh_key.png)

需要注意的是，**一个 Github 账号可以添加多个公钥**，这也是能够实现在多台电脑上实现协同工作的基础。

### 验证 ssh key 是否设置成功

在 Git 中执行以下命令：

```bash
ssh -T git@github.com
```

当结果如下图所显示的类似时，说明已经设置成功了：

![](Snipaste_2023-11-16_23-30-55.png)

设置成功后，就不再需要密码 clone 和 push 代码。

### 测试

测试推送或拉取代码，可以随便写点内容并提交到远程仓库，检验整个流程是否走通。

### 参考资料

1. [Github配置ssh key的步骤（大白话+包含原理解释）_github生成ssh key_风中一匹狼v的博客-CSDN博客](https://blog.csdn.net/weixin_42310154/article/details/118340458)
2. [远程仓库 - 廖雪峰的官方网站 (liaoxuefeng.com)](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)
3. [如何使用git（同一账号）在多台电脑协同做工 - 南瓜不南瓜 - 博客园 (cnblogs.com)](https://www.cnblogs.com/Ye-zixiao/p/12233193.html)

### 坑

今天主要主要踩的坑就是我已经在 Github 上成功地配置了公钥，但是当我执行

```bash
git push origin master
```

还会弹出一个输入 token 的对话框，一开始我还以为要填写生成的 ssh key，但是复制粘贴提交后，提示失败。不过在网上找到了 [破解为何添加了ssh keys还是无法git push - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/406922505) 这篇文章，并跟着这篇文章的步骤操作后，成功解决了这个问题，把笔记推送到了远程仓库上。

问题所在：

> 由于之前并没有单独使用ssh keys的习惯，在 git clone 的时候很多时候都是按照 git init repo 上的指示，采用了 https 协议，而非 git 协议。

拿 Obsidian 这个远程仓库举例，如果是 https 协议，克隆的地址是 `https://github.com/Moonshadow2333/Obsidian.git`，而如果是用 ssh key 来克隆项目，则地址是 `git@github.com:Moonshadow2333/Obsidian.git`。

查看 remote 地址：

```bash
git config --get remote.origin.url
```

如果发现不是 ssh key 的克隆地址，则可以使用以下命令来修改：

```bash
git remote set-url origin git@github.com:Moonshadow2333/Obsidian.git
```

最后再执行 `git push origin master` 命令来验证是否成功。