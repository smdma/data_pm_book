





gitbook插件可以解决一些网站不太方便的地方，如侧边栏导航不能收缩，自带搜索不支持中文等。

插件安装、使用方法：

> 1、 在`book.json`的plugins参数中添加插件名。
> 2、终端使用`gitbook install`来安装插件，或使用NPM命令来单独安装：`npm install gitbook-plugin-插件名`。
> 3、重启服务或者重新打包就能看见效果。
> 4、如果使用`gitbook install`安装的很慢，建议使用`npm init`初始化一个package.json文件，然后每个包通过npm命令安装，以后就可以通过`npm install`一键快速安装依赖包了。

**注意：**
1、插件一定先要在`book.json`文件里面plugins中才能生效，如果只是安装了插件，而没配置的话是不会生效的。
2、gitbook命令安装慢，而且是全部插件都安装一遍，如果只安装一个插件的话建议使用NPM命令安装。



Gitbook 的插件：

- 数学公式： `mathjax`
- 目录列表折叠：`collapsible-menu`、`toggle-chapters`
- 返回顶部：`back-to-top-button`
- 更改标题色彩：`theme-comscore`
- 自由调节侧边栏宽度：`splitter`



## 2. 高频常用插件

### 2.1 search-pro 高级搜索（支持中文）

search-pro支持中文搜索，在使用此插件之前，需要将默认的search和lunr 插件去掉。
在`book.json`的plugins参数中添加插件名：

```markdown
{
    "plugins": [
         "-lunr", "-search", "search-pro"
    ]
}
```

其中"-search"中的`-`符号代表去除默认自带的插件。
然后使用`npm install gitbook-plugin-search-pro --registry=https://registry.npm.taobao.org/`

### 2.2 左侧目录可折叠

#### 2.2.1 chapter-fold

支持多层目录，点击导航栏的标题名就可以实现折叠扩展。
在`book.json`的plugins参数中添加插件名：

```markdown
{
    "plugins": ["chapter-fold"]
}
```

然后使用`npm install gitbook-plugin-chapter-fold`命令安装插件。
使用效果如下图:

![clipboard.png](https://segmentfault.com/img/bVbvv9Z?w=700&h=322)

**注意：**要想目录折叠，`SUMMARY.md`目录应该如下：

```markdown
* [项目介绍](README.md)

* [tcp说明](doc/http/tcp/tcp说明.md)
    * [udp说明](doc/http/tcp/udp/udp说明.md)
* [html](doc/html/readme.md)
    * [HTML5-特性说明](doc/html/HTML5-特性说明.md)
```

如下写法会产生bug，导致CSS是收缩的，不能展开，效果如上面的动图：

```markdown
* CSS 
    * [说明](doc/css/readme.md)
```

#### 2.2.2 expandable-chapters

这个插件也是左侧目录折叠的插件，不同的是可以解决`chapter-fold`插件的bug，怎么写都会折叠目录
在`book.json`的plugins参数中添加插件名：

```markdown
{
    "plugins": [
         "expandable-chapters"
    ]
}
```

安装命令：`npm install gitbook-plugin-expandable-chapters`
**注意：**这个插件也有问题，就是如下写法的，需要点击箭头才能展开收缩菜单：

```markdown
* [tcp说明](doc/http/tcp/tcp说明.md)
    * [udp说明](doc/http/tcp/udp/udp说明.md)
```

解决的办法是和`chapter-fold`插件一起用，互补一下各自的问题就完美解决了：

```markdown
"plugins": [
    "expandable-chapters",
    "chapter-fold",
]
```

注意还有一个`expandable-chapters-small`插件也是折叠菜单的，但是这个插件跟`chapter-fold`有一样的bug，这里就不讲了，用上面两个插件就完美解决问题了。

### 2.3 splitter 侧边栏宽度可调节

在`book.json`的plugins参数中添加插件名：

```markdown
{
    "plugins": ["splitter"]
}
```

然后使用`npm install gitbook-plugin-splitter`命令安装插件。
使用效果如下图:
![clipboard.png](https://segmentfault.com/img/bVbu86E?w=540&h=233)

### 2.4 生成页内目录

#### 2.4.1 page-treeview 在页面顶部显示目录

不需要插入标签，能支持到6级目录，在页面顶部显示。
在`book.json`的plugins参数中添加插件名：

```
{
    "plugins": ["page-treeview"],
    "pluginsConfig": {
        "page-treeview": {
            "copyright": "Copyright &#169; aleen42",
            "minHeaderCount": "2",
            "minHeaderDeep": "2"
        }
    }
}
```

插件的配置项可以不填。
然后使用`npm install gitbook-plugin-page-treeview`命令安装插件。
使用效果如下图:
![clipboard.png](https://segmentfault.com/img/bVbu9bp?w=899&h=334)
目录线面一行版权的信息，如果想要删除，需要在插件目录中打开：`/node_modules/gitbook-plugin-page-treeview/lib/index.js`。
大约43行，在`generateContent`方法定义中，该方法的返回值

```markdown
return renderContent ? `<div class="treeview__container">${copyRight + renderContent}</div>` : '';
// 改成：
return renderContent;
```

然后重启服务或重新打包。

**注意：**
1、此方法适用于`3.0.1`版本的，其他版本如果没有请搜索`renderContent`,`options.copyright`,`>Treeview<`尝试。
2、如果你重新安装了这个插件，那么就需要从新修改插件文件。

#### 2.4.2 悬浮按钮目录

anchor-navigation-ex

```
{
    "plugins" : [ 
        "anchor-navigation-ex"
    ],
    "pluginsConfig": {
        "anchor-navigation-ex": {
            "showLevel": false, //标题是否显示层级序号.页面标题和导航中的标题都会加上层级显示。
            "showGoTop": false // 是否显示返回顶部按钮
        },
    }
}
```

npm install gitbook-plugin-anchor-navigation-ex
`anchor-navigation-ex`页面右上角生成一个灰色的按钮，鼠标移入后会显示灰色的目录。

更多配置介绍：[https://github.com/zq99299/gi...](https://github.com/zq99299/gitbook-plugin-anchor-navigation-ex/blob/master/doc/config.md)

下面的插件也能生成悬浮页内目录，但是页面只有二级、三级、标题是不会显示，这里仅供参考
page-toc-button、ancre-navigation

```
{
    "plugins" : [ 
        "page-toc-button",
        "ancre-navigation"
    ],
    "pluginsConfig": {
        "page-toc-button": {
            "maxTocDepth": 2,  // 标题的最大深度（2 = h1 + h2 + h3）。不支持值> 2。
            "minTocSize": 2    // 显示toc按钮的最小toc条目数。
           }
    }
}
```

安装：

```
npm install gitbook-plugin-page-toc-button
npm install gitbook-plugin-ancre-navigation
```

`page-toc-button`插件在页面右上角生成一个黑色的按钮，鼠标移入后会显示黑色的目录。
`ancre-navigation`插件页面右上角生成一个白色的按钮，页面右下角生成一个返回顶部的按钮。

### 2.5 回到顶部按钮

在`book.json`的plugins参数中添加插件名和配置信息：

```
{
    "plugins": [
        "back-to-top-button"
    ],
}
```

使用`npm install gitbook-plugin-back-to-top-button`命令安装插件。

## 3. 其他插件

### 3.1 折叠模块(页面内容可折叠)

#### 3.1.1 accordion

这个插件名叫手风琴，可以实现将内容隐藏起来，外部显示模块标题和显示箭头，点击箭头可显示里面的内容。

在`book.json`的plugins参数中添加插件名：

```
{
    "plugins": ["accordion"]
}
```

然后使用`npm install gitbook-plugin-accordion`命令安装插件。
md文件的写法：

```
%accordion%模块标题%accordion%
内容部分
%/accordion%
```

使用效果([https://artalar.github.io/git...](https://artalar.github.io/gitbook-plugin-accordion/))：
![clipboard.png](https://segmentfault.com/img/bVbvgSv?w=912&h=257)

#### 3.1.2 sectionx

在`book.json`的plugins参数中添加插件名：

```
{
    "plugins": ["sectionx"],
    "pluginsConfig": {
        "sectionx": {
          "tag": "b"       // 设置标题的标签，可选值：h1, h2, h3, h4, h5, h6, b
        }
     }
}
```

标签的 tag 最好是使用 b 标签，如果使用 h1-h6 可能会和其他插件冲突。

然后使用`npm install gitbook-plugin-sectionx`命令安装插件。

在MD文件中的用法：

```
<!--sec data-title="这里写标题" data-id="section0" data-show=true ces-->
这里是内容   
dsadsa    
dadsa
<!--endsec-->
```

最终效果：
![clipboard.png](https://segmentfault.com/img/bVbvgTj?w=908&h=167)
在线例子：[https://ymcatar.gitbooks.io/g...](https://ymcatar.gitbooks.io/gitbook-test/content/testing_sectionx.html)

其中参数的作用：

> data-title：收缩模块的标题，大小在插件参数配置里面配置，注意：HTML中实体字符要转义
> data-id：收缩模块的id，用于插件的控制按钮，下面讲解
> data-show：模式默认是收缩还是展开的，true：展开，false：隐藏

sectionx还可以设置按钮来显示或隐藏代码折叠模块，md写法如下：

```
<button class="section" target="showCode" show="显示文案" hide="隐藏文案"></button>
<!--sec data-title="这里写标题" data-id="showCode" data-show=true ces-->
这里是内容   
dsadsa     
dadsa
<!--endsec-->
```

效果如下图：

![clipboard.png](https://segmentfault.com/img/bVbvmAD?w=955&h=323)
其中参数的作用：

> class：类名必须是`section`
> target：需要影藏的模块名，名字与`data-id`一致
> show：模块隐藏时，按钮显示的文案
> hide：模块显示时，按钮显示的文案

### 3.2 右上角添加github图标

在`book.json`的plugins参数中添加插件名和配置信息：

```
{
    "plugins": [ 
        "github" 
    ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/zhangjikai"
        }
    }
}

```

然后使用`npm install gitbook-plugin-github`命令安装插件。
**注意：**
如果使用npm命令安装后报错`GitBook doesn't satisfy the requirements of this plugin: >=4.0.0-alpha.0`.
请使用`gitbook install`来安装.
或者`npm uninstall gitbook-plugin-github`卸载后，使用`npm i gitbook-plugin-github@2.0.0`安装，然后查看是否还报错。

### 3.3 edit-link在线编辑文件

`book.json`中插件名和配置信息：

```
{
    "plugins": ["edit-link"],
    "pluginsConfig": {
      "edit-link": {
            "base": "//github.com/yulilong/book/edit/master",
            "label": "编辑此页面"
       }
    }
}
```

使用`npm i gitbook-plugin-edit-link`命令安装插件。
下过如下图：

![clipboard.png](https://segmentfault.com/img/bVbvzyh?w=745&h=236)
点击编辑按钮，即可跳转到github仓库在线编辑这个文件。

### 3.4 修改网站的favicon.ico

github地址：[https://github.com/menduo/git...](https://github.com/menduo/gitbook-plugin-favicon)
`book.json`中插件名和配置信息：

```
{
    "plugins": ["favicon"],
    "pluginsConfig": {
      "favicon": {
            "shortcut": "asset/img/favicon.ico",
            "bookmark": "asset/img/favicon.ico",
            "appleTouch": "asset/img/favicon.ico",
            "appleTouchMore": {
                "120x120": "asset/img/favicon.ico",
                "180x180": "asset/img/favicon.ico"
            }
        }
    }
}
```

使用`npm install gitbook-plugin-favicon`命令安装插件。
下过如下图：

![clipboard.png](https://segmentfault.com/img/bVbvwc3?w=1197&h=326)

**注意：**
1、图标的格式一定要是`.ico`的，直接修改图片的后缀为`.ico`是无效的。
2、图标的分辨率要是32*32的。
3、可在线把图片转成图标：http://www.bitbug.net/

### 3.5 查看图片

#### 3.5.1 popup打开新的页面查看图片

在`book.json`的plugins参数中添加插件名：

```
{
    "plugins": [
        "popup"
    ],
}
```

使用`npm install gitbook-plugin-popup`命令安装插件。

#### 3.5.2 lightbox页面弹窗显示图片

在`book.json`的plugins参数中添加插件名：

```
{
    "plugins": [
        "lightbox"
    ],
}
```

使用`npm install gitbook-plugin-lightbox`命令安装插件。

### 3.6 prism代码块颜色插件

插件地址：[https://github.com/gaearon/gi...](https://github.com/gaearon/gitbook-plugin-prism)
此插件需要禁用gitbook自带的`highlight`插件。
`book.json`中插件名和配置信息：

```
{
    "plugins": ["prism", "-highlight"],
    "pluginsConfig": {
      "prism": {
        "css": [
          "prismjs/themes/prism-okaidia.css"
        ]
      }
    }
}
```

使用`npm install gitbook-plugin-prism`命令安装插件。
效果如下图：
![clipboard.png](https://segmentfault.com/img/bVbvpGH?w=1014&h=231)

更多的颜色参考：[https://github.com/gaearon/gi...](https://github.com/gaearon/gitbook-plugin-prism)

### 3.7 Gitalk评论插件

Gitalk插件的使用教程:[https://segmentfault.com/a/11...](https://segmentfault.com/a/1190000018072952)

这个插件是需要在`MD`文件中写入代码的，在需要评论插件的MD文件的最下面写入如下代码：

```
<link rel="stylesheet" href="//cdn.bootcss.com/gitalk/1.5.0/gitalk.min.css">
<script src="//cdn.bootcss.com/gitalk/1.5.0/gitalk.min.js"></script>
<div id="gitalk-container"></div>
<script>
    var gitalk = new Gitalk({
    clientID: '2eb19afceda708b27e64', // GitHub Application Client ID
    clientSecret: '36aedb5a30321626a8631689fee5fafd5929f612', // GitHub Application Client Secret
    repo: 'book',              // 存放评论的仓库
    owner: 'user',          // 仓库的创建者，
    admin: ['user'],        // 如果仓库有多个人可以操作，那么在这里以数组形式写出
    id: location.pathname,      // 用于标记评论是哪个页面的，确保唯一，并且长度小于50
    });
    gitalk.render('gitalk-container');    // 渲染Gitalk评论组件
 </script>
```

效果如下图：
![clipboard.png](https://segmentfault.com/img/bVbvgRp?w=1272&h=409)

### 3.8 hide-element隐藏元素

可以隐藏不想看到的元素，比如导航栏中`Published by GitBook`。
`hide-element`是通过HTML元素的`class`名字来查找要隐藏的元素，想要隐藏元素找到元素的样式类名加到插件配置里面就可以隐藏元素了。

在`book.json`的plugins参数中添加插件名和配置信息：

```
{
    "plugins": [
        "hide-element"
    ],
    "pluginsConfig": {
        "hide-element": {
            "elements": [".gitbook-link"]
        }
    }
}
```

然后使用`npm install gitbook-plugin-hide-element`命令安装插件。

上面的配置信息中设置了隐藏的类名，所以`Published by GitBook`就看不见，效果如下图：

![clipboard.png](https://segmentfault.com/img/bVbvmCo?w=822&h=272)

### 3.9 网站主题

#### 3.9.1 theme-fexa

插件地址：[https://github.com/tonyyls/gi...](https://github.com/tonyyls/gitbook-plugin-theme-fexa)

`book.json`中插件名和配置信息：

```
{
    "plugins": [
        "theme-fexa"
    ],
    "variables": {
        "themeFexa":{
            "nav":[
                {
                    "url":"http://...",
                    "target":"_blank",
                    "name": "简易教程"
                }
            ]
        },
    },
    "pluginsConfig": {
        "theme-fexa":{
            "search-placeholder":"输入关键字搜索", //搜索框提示信息
            "logo":"./logo.png", //logo地址
            "favicon": "./favicon.ico" //ico地址
        }
    }
}
```

使用`npm install gitbook-plugin-theme-fexa`命令安装插件。

效果如下图：

![clipboard.png](https://segmentfault.com/img/bVbvpGy?w=1016&h=402)

### 3.10 添加页面显示最后更新时间

在`book.json`的plugins参数中添加插件名和配置信息：

```
{
    "plugins": [
        "tbfed-pagefooter"
    ],
    "pluginsConfig": {
        "tbfed-pagefooter": {
            "copyright":"",
            "modify_label": "该文件最后修改时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        },
    }
}
```

然后使用`npm install gitbook-plugin-tbfed-pagefooter`命令安装插件。
页面效果：

![clipboard.png](https://segmentfault.com/img/bVbvwgY?w=1098&h=190)

## 参考资料

[gitbook 实用插件](https://www.cnblogs.com/mingyue5826/p/10307051.html)
[http://gitbook.zhangjikai.com...](http://gitbook.zhangjikai.com/plugins.html)
[https://blog.csdn.net/weixin_...](https://blog.csdn.net/weixin_38171180/article/details/89059127)





![img](https://sponsor.segmentfault.com/lg.php?bannerid=2&campaignid=1&zoneid=3&loc=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000019806829&referer=https%3A%2F%2Fwww.sogou.com%2Flink%3Furl%3DhedJjaC291NO8Gk_zr4njUJw9U14oc0bh6O4RiYb6h2ZcrHiwUV0DFfx9tBsqCyx&cb=ea9cb2af5b)



























