# Disqus

[Disqus](https://disqus.com) 是一个非常流行的为网站集成评论系统的工具，同样，gitbook 也可以集成 disqus 以便可以和读者交流。

首先，需要在 disqus 上注册一个账号，然后添加一个 website，这会获得一个关键字，然后在集成时配置这个关键字即可。

## 安装 disqus 插件

可以参考 [插件项目主页](https://github.com/GitbookIO/plugin-disqus) 来安装，命令如下：

```bash
$ npm install gitbook-plugin-disqus -g
```

然后，修改 `book.json` 配置文件，添加插件的配置内容：

```json
{
    "plugins": ["disqus"],
    "pluginsConfig": {
        "disqus": {
            "shortName": "introducetogitbook"
        }
    }  
}
```

注意：上面的 `shortName` 的值就是你在 disqus 上创建的 website 获得的唯一关键字。

效果如下图所示：

![disqus](../../assets/plugins/disqus.png)
