# 说明书

---

[Site](https://yj1516.top)

Tools：网页寄存服务--[Github Pages](https://pages.github.com/)，静态网站生成器--[Hugo](https://gohugo.io/)，Hugo.Theme--[yj](https://github.com/YHYJ/hugo-yj-theme)(fork from [tranquilpeak](https://github.com/kakawait/hugo-tranquilpeak-theme))

[图片在线压缩](https://www.yasuotu.com/)

本页面基本是[hugo-tranquilpeak-theme/user.md](https://github.com/kakawait/hugo-tranquilpeak-theme/blob/master/docs/user.md)的翻译

---

## hugo-yj-theme

### 功能

#### 基本功能

- 全面响应
- 针对PAD和手机进行了优化（有限）
- 侧边栏可配置
- Tags（标签）、Categories（分类）、Archives（归档）页面
- 自定义背景图
- 支持Open Graph protocol（OG，开放图谱协议）
- 自定义简单（字体、颜色、元素布局、代码着色）
- 支持国际化（i18）

#### 文章功能

- 支持缩略图
- 支持封面
- 自适应视频和图片
- 支持文章分享
- 导航栏
- 使用Github竹图突出显示代码（可自定义）
- 支持图库
- 支持图片标签（FancyBox）、宽图片
- 支持选项卡式代码块
- 支持文本突出显示
- 支持报警（Alerts）
- 目录

#### 综合服务

- Disqus
- Google analytics
- Gravatar
- Facebook Insights

### 缺陷

由于Hugo的限制，以下功能无法使用：

- 按年份归档文章（E.g：`/archives/2019`）
    - 按月份归档文章（E.g：`/archives/2019/01`）

### 安装

1. 进入`hugo new site <name>`创建的<name>文件夹中
2. 执行命令`git submodule add -f https://github.com/YHYJ/hugo-yj-theme.git themes/yj`，这将会把hugo-yj-theme作为子模块下载到*<name>/themes/yj*中

### 配置

#### 配置Hugo使用的主题

![Hugo Theme](https://gitee.com/YJ1516/MyPic/raw/master/picgo/hugo_theme.png)

1. 使用*<name>/yj/exampleSite/config.toml*替换*<name>/config.toml*（以下称为config.toml）
2. 将**theme**字段的值替换为下载到*<name>/themes*中的文件夹的名字

#### 配置界面语言

将config.toml的字段**defaultContentLanguage**替换为以下括号里的值即可设置为对应的语言：

- 中文（`zh-cn`）
- 繁体中文（`zh-tw`）
- 英文（`en-us`）
- 德语（`de-de`）
- 法语`fr-fr`）
- 日语（`ja`)
- 葡萄牙语（`pt-br`)
- 俄语（`ru`)
- 西班牙语（`es`)
- 越南语（`vi`)

如果您的语言不在上述选项中，请按照以下步骤添加（以瑞典语为例）：

1. 将**yj/i18n/en-us.yaml**复制为**yj/i18n/sv-se.yaml**文件
2. 用瑞典语翻译替换所有的**translation**
3. 将**defaultContentLanguage**的值设置为**sv-se**

#### 配置时间格式

该时间格式用于标记文章的发布时间，默认是`yyyy-mm-dd`，像是："2019-1-2"

可以自定义该时间格式：

```toml
[params]
  dateFormat = "2 January 2006"
```

这样时间格式就会变成："2 January 2006"

> **Notes**：时间格式应该遵循go语言包`time`的语法，详见[time](https://golang.org/pkg/time/)
>
> 此外，只有完整的月份英文单词才会翻译成对应的语言，缩写不会翻译

#### 配置全局关键字

可以为搜索引擎定义关键字，这些关键字将被添加到所有的页面上

```toml
[params]
  keywords = ["development", "next-gen"]
```

#### 配置侧边栏

可以根据需求添加多个分组和多个链接

```toml
[[menu.main]]
  weight = 1
  identifier = "home"
  name = "Home" 
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-home\"></i>"
  url = "/"
[[menu.main]]
  weight = 2
  identifier = "github"
  name = "GitHub"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-github\"></i>"
  url = "https://github.com/kakawait"

[[menu.links]]
  weight = 1
  identifier = "categories"
  name = "Categories"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-bookmark\"></i>"
  url = "/categories"
[[menu.links]]
  weight = 2
  identifier = "tags"
  name = "Tags"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-tags\"></i>"
  url = "/tags"
[[menu.links]]
  weight = 3
  identifier = "archives"
  name = "Archives"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-archive\"></i>"
  url = "/archives"

[[menu.misc]]
  weight = 1
  identifier = "rss"
  name = "RSS"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-rss\"></i>"
  url = "/index.xml"
[[menu.misc]]
  weight = 2
  identifier = "about"
  name = "About"
  pre = "<i class=\"sidebar-button-icon fa fa-lg fa-question\"></i>"
  url = "/#about"
```

| 变量       | 描述                               | 类型          |
| ---------- | ---------------------------------- | ------------- |
| weight     | 每组`menu`按照`weight`的值进行排序 | int           |
| identifier | 唯一标识符，用于国际化             | string        |
| name       | 分组下条目的名称                   | string        |
| pre        | 在`name`左侧显示的图标             | template.HTML |
| url        | 分组下条目的URL                    | string        |
| class      | 添加到链接tag的CSS类               | string        |

#### 配置页眉

页眉右边的链接默认显示的是作者的gravatar/头像

```toml
[params.header.rightLink]
  class = ""
  icon = "address-card"
  url = "/#about"
```

| 变量  | 描述                                                         |
| ----- | ------------------------------------------------------------ |
| class | 添加到链接的CSS类                                            |
| icon  | 不带`fa-`的[font-awesome icon](http://fontawesome.io/icons/) class的名称 |
| url   | 跳转到的URL，如果是内部的则不需要域名                        |

#### 配置作者

```toml
[author]
  name = "Firstname Lastname"
  bio = "**Hola**"
  job = "Your job title"
  location = "China"
  gravatarEmail = "XXX@example.com"
  picture = "https://example.com/XXX.png"
  # twitter = "XXXXXX"
  # googlePlus = "XXXXXX"
```

| 变量          | 描述                                                  |
| ------------- | ----------------------------------------------------- |
| name          | 作者名                                                |
| bio           | 个人简介（支持Markdown和HTML格式）                    |
| job           | 工作                                                  |
| location      | 所在地                                                |
| gravatarEmail | 优先使用gravatar image作为头像                        |
| picture       | 使用一个图片作为头像，当gravatarEmail为空是使用该图片 |
| twitter       | Twitter用户名（不加@，E.g：yj），默认不使用           |
| googlePlus    | google plus ID，E.g：+yj 或者 012346789012467890      |

### 定制化

#### 文章格式

> **Notes**：并不是所有的定制化内容都会在这个文档记录，详情查看[example config.toml](https://github.com/YHYJ/hugo-yj-theme/blob/master/exampleSite/config.toml)

```toml
[params]
  syntaxHighlighter = "highlight.js"
  clearReading = true
  hierarchicalCategories = true
  description = "Hola"
  sidebarBehavior = 2
  coverImage = "images/cover.jpg"
  imageGallery = true
  thumbnailImage = true
  thumbnailImagePosition = "left"
  autoThumbnailImage = true
  favicon = "/favicon.png"
  swapPaginator = true              # "上一篇"和"下一篇"按钮的相对位置，为'true'则"上一篇"在左，否则在右
```

| 变量                   | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| syntaxHighlighter      | 设置代码高亮，可选`highlight.js`和`prism.js`两种方式         |
| clearReading           | 当阅读文章的时候隐藏侧边栏，即所谓“阅读模式”。（当`sidebarBehavior`的值是3或者4的时候该变量无效） |
| hierarchicalCategories | 设置是否在"archives"之间建立层级关系，当为`true`时，`categories = ["foo", "bar"]`将把"bar"作为"foo"的子类别 |
| description            | 站点描述                                                     |
| sidebarBehavior        | 定义标题和侧边栏的行为：`1`-自适应，尽量最宽；`2`-自适应，宽窄适中；`3`-自适应，尽量最窄；`4`-折叠式，尽量最宽；`5`-折叠式，宽窄适中；`6`-折叠式，尽量最窄 |
| coverImage             | 博客封面图片，可以使用本地文件或者URL，使用本地文件要放到*yj/static/images*下 |
| imageGallery           | 设置是否启用图库，启用后会在文章末尾显示包含有photos变量的图片库 |
| thumbnailImage         | 设置是否在索引页面显示文章的缩略图                           |
| thumbnailImagePosition | 设置缩略图和文章标题的相对位置                               |
| autoThumbnailImage     | 设置当没有指定缩略图时是否自动选择封面或者从图库选择一张图片作为缩略图 |
| favicon                | 网站图标，文件名必须是`favicon`                              |
| swapPaginator          | “上一篇”和“下一篇”按钮的相对位置，`true`是“上一篇”  “下一篇”；`false`是“下一篇”  “上一篇” |

当`hierarchicalCategories = true`时，'archives'页面如图：

![True](https://gitee.com/YJ1516/MyPic/raw/master/picgo/with_hierarchical_categories.png)

当`hierarchicalCategories = false`时，'archives'页面如图：

![False](https://gitee.com/YJ1516/MyPic/raw/master/picgo/without_hierarchical_categories.png)

#### 代码高亮

自带的代码高亮支持很少，可以自定义添加JS来完善：

```toml
[params]
  [[params.customJS]]
    src = "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/languages/dockerfile.min.js"
    crossorigin = "anonymous"
    async = true
    defer = true
```

