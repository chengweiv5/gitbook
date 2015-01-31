# multipart

[multipart](https://www.npmjs.com/package/gitbook-plugin-multipart) 插件可以将书籍分成几个部分，例如：

- GitBook Basic
- GitBook Advanced

对有非常多章节的书籍非常有用，分成两部分后，各个部分的章节都从 1 开始编号。

## 安装及配置

和安装其它插件一样，执行以下命令：

```bash
$ npm install gitbook-plugin-multipart -g
```

然后编辑 `book.json` 添加 multipart 到 plugins 中：

```json
    "plugins": [
        "multipart"
    ],
```
