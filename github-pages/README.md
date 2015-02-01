# 发布到 GitHub Pages

除了能够将书籍发布到 GitBook.com 外，还可以将书籍发布到 GitHub Pages，由于没有找到官方文档，所以这里记录的是我自己正在使用的一种方法。

如果读者不了解 GitHub Pages 为何物，简单说就是一个可以托管静态网站的 Git 项目，支持使用 markdown 语法以及 Jekyll 来构建，或者直接使用已经生成好的静态站点。详细可以参考 [GitHub Pages 主页](https://pages.github.com/)。

由于 gitbook 书籍可以通过 `gitbook` 本地构建出 site 格式，所以可以直接将构建好的书籍直接放到 GitHub Pages 中托管，之后，可以通过如下地址访问书籍：

`<username>.github.io/<project>`

例如：这本书中使用的例子 'test' 项目可以通过地址：*chengweiv5.github.io/test* 来访问。

当访问 *chengweiv5.github.io/test* 时，会访问 *chengweiv5/test* 项目的 *gh-pages* 分支的内容，所以需要为项目创建一个 *gh-pages* 分支，并且将静态站点内容放入其中。也就是说，test 项目将有如下两个分支：

- master, 保存书籍的源码
- gh-pages, 保存书籍编译后的 HTML 文件

为了避免复制，这里将两个分支的内容分别保存在本地两个目录中。

## 配置 test master 分支

首先，配置 test 项目 master 分支中的 *book.json*，修改 `gitbook build` 的输出目录为 *../test-gh-pages*，如下：

```diff
$ git diff
diff --git a/book.json b/book.json
index 5ec6de8..e89c441 100644
--- a/book.json
+++ b/book.json
@@ -16,7 +16,7 @@
             "Chengwei's Blog": "http://www.chengweiyang.cn"
         }
     },
-    "output": null,
+    "output": "../test-gh-pages",
     "pdf": {
         "fontSize": 12,
         "footerTemplate": null,
```

注意：*book.json* 中的配置会覆盖命令行参数 `--output`。

## 构建书籍

配置完成后，就可以构建书籍内容了，如下：

```bash
$ gitbook build
Starting build ...
Successfully built!

$ ls ../test-gh-pages/
GLOSSARY.html       chapter1            chapter2            gitbook             glossary_index.json index.html          search_index.json
```

可以看到，书籍内容被放在了 *../test-gh-pages* 目录。

## 上传书籍内容到 GitHub

现在，可以将编译好的书籍内容上传到 GitHub 中 *test* 项目的 *gh-pages* 分支了，虽然这里还没有创建分支，上传和创建会一步完成！

```bash
$ git init .
Initialized empty Git repository in /Users/chengwei/Github/test-gh-pages/.git/

$ git add .

$ git commit -asm "Init book contents"
[master (root-commit) 6c6b0dd] Init book contents
 36 files changed, 2223 insertions(+)
 create mode 100644 GLOSSARY.html
 create mode 100644 chapter1/README.html
 create mode 100644 chapter1/section1.1.html
 create mode 100644 chapter1/section1.2.html
 create mode 100644 chapter2/README.html
 create mode 100644 gitbook/app.js
...
...

$ git remote add github https://github.com/chengweiv5/test.git

$ git push -u github master:gh-pages
Counting objects: 49, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (45/45), done.
Writing objects: 100% (49/49), 1.34 MiB | 131.00 KiB/s, done.
Total 49 (delta 5), reused 0 (delta 0)
To https://github.com/chengweiv5/test.git
 * [new branch]      master -> gh-pages
Branch master set up to track remote branch gh-pages from github.
```

现在，书籍的内容已经上传到 GitHub 上，所以通过访问 *chengweiv5.github.io/test* 就可以阅读 *test* 这本书了！

![gitbook git-pages](../assets/github-pages/gitbook-git-pages.png)

注意：由于我将 *chengweiv5.github.io* 重定向到了个人站点 *www.chengweiyang.cn*，所以可以看到，浏览器中的 URL 自动变成了 *www.chengweiyang.cn/test*，非常 cool! 关于怎样重定向 GitHub Pages 到个人域名，请参考博客：[怎样使用 GitHub Pages 搭建个人站点](http://www.chengweiyang.cn/2014/07/19/Whats-behind-this-site/)。

以后，每次更新了书籍源码，只要编译后，在 *test-gh-pages* 中提交更新，上传到 GitHub 中就可以更新书籍的内容了。
