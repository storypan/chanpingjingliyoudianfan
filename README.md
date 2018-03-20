在经过了长时间的折腾之后，终于在Mac环境成功的安装了Gitbook。

安装Gitbook的主要流程如下：

安装node.js&gt;安装Gitbook&gt;安装Gitbook编辑器&gt;安装calibre&gt;导出PDF。

### 1. 安装node.js

安装node.js，在node.js官网下载，直接安装。

下载地址：[https://nodejs.org/en/](https://link.jianshu.com?t=https://nodejs.org/en/)。

> 这里需要注意的是，node.js有两个版本，一个是大多数人使用的，也就是稳定版；另一个是最新版，拥有最新的特性。在这里，我们下载稳定版即可。

安装成功之后输入`node -v`，显示node.js版本代表安装成功。

```
huixingdeMacBook-
Air:
~ huixing$ node -v
v6.
10.2
```

### 2. 安装Gitbook

这个点是最坑的。尤其是在Mac环境下，我先后尝试了以下代码：

```
npm install gitbook -g
npm install -g gitbook-cli

```

还有好几个，先说明下，以上代码都是错误的，不是卡主了就是不能动。原来，Mac环境下需要用到`sudo`这个指令。

```
sudo npm install gitbook-cli -g

```

> 一定要用到`-g`，这个代表全局安装，我去掉`-g`安装了一次，也成功了，但是在终端使用`gitbook -V`查看的时候发现根本没安装，这是我遇到的坑最多的地方。

在终端输入`gitbook -V`之后即可查看当前Gitbook版本，代表安装成功。需要注意的是“V”一定要大写。

```
huixingdeMacBook-Air:~ huixing$ gitbook -V

CLI
 version: 
2.3
.0

GitBook version: 
3.2
.2
```

### 3. 安装Gitbook编辑器

接下来就是安装Gitbook桌面编辑器了。有的人可能会问，你都已经安装了终端环境下的Gitbook了，为什么还要安装桌面端呢？

下载地址：[https://www.gitbook.com/editor/](https://link.jianshu.com?t=https://www.gitbook.com/editor/)

其实，使用Gitbook桌面编辑器能够很方便的进行文章书写，终端环境下的Gitbook只是为了生成HTML文档与PDF文档而使用的。

安装了Gitbook桌面端之后，你可以在客户端中新建一本书籍。然后用终端生成HTML。

> 使用`gitbook build`命令。

```
huixingdeMacBook-
Air:
import huixing$ cd jianli
huixingdeMacBook-
Air:
jianli huixing$ gitbook build

info:
7
 plugins are installed 

info:
6
 explicitly listed 

info:
 loading plugin 
"highlight"
... OK 

info:
 loading plugin 
"search"
... OK 

info:
 loading plugin 
"lunr"
... OK 

info:
 loading plugin 
"sharing"
... OK 

info:
 loading plugin 
"fontsettings"
... OK 

info:
 loading plugin 
"theme-default"
... OK 

info:
 found 
1
 pages 

info:
 found 
7
 asset files 

info:
>
>
generation finished with success in 
1.0
s ! 
huixingdeMacBook-
Air:
jianli huixing$ 

```

看到success的提示没，这个时候系统文件根目录下就生成了一个`_book`的文件夹。打开就是该书籍的HTML格式了。

你也可以直接将该书籍在本地预览。

> 使用`gitbook serve`命令

```
huixingdeMacBook-Air:jianli huixing$ gitbook serve
Live reload server started on port: 
35729

Press CTRL+C to quit ...

info: 
7
 plugins are installed 
info: loading plugin 
"livereload"
... OK 
info: loading plugin 
"highlight"
... OK 
info: loading plugin 
"search"
... OK 
info: loading plugin 
"lunr"
... OK 
info: loading plugin 
"sharing"
... OK 
info: loading plugin 
"fontsettings"
... OK 
info: loading plugin 
"theme-default"
... OK 
info: found 
1
 pages 
info: found 
7
 asset files 
info: 
>
>
 generation finished 
with
 success 
in
1.2
s ! 

Starting server ...
Serving book on http:
//localhost:4000
```

> Gitbook编辑器需要同终端里安装的Gitbook配合，完美实现在线HTML的生成，PDF的生成。当然，如果愿意将文档公开到gitbook或者gitbub仓库的看到这里就可以了，因为Gitbook网站上可以直接导出PDF，MOBI，EBUP等电子书格式。如果不想将书籍公开，那么可以往下面继续看了！

### 4. 安装calibre插件

玩过kindle的都知道，calibre是一款非常方便的开源电子书转换软件。在这里，我们也是用到ebook-convert这个插件。

首先在calibre官网下载插件，下载链接：[https://calibre-ebook.com/download](https://link.jianshu.com?t=https://calibre-ebook.com/download)。下载适合自己系统的版本。

下载到电脑之后我做了很多尝试，刚下载之后我兴冲冲的去使用`gitbook pdf . mypdf.pdf`指令，结果发现提示ebook-convert未安装。

这里我通过咨询了一些大神，在这个过程中他们给了我很大的帮助。也查看了很多教程，所有教程中都说了两个问题。

* 将安装的calibre放在系统应用中，然后将app添加到path中。

  > 这个说实话我也没怎么看懂，但是下面我会详细的说这一步如何操作。

* 执行一个命令`sudo ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin`。

以上两部我都做了，最终也成功的将Gitbook导出了PDF，但具体是哪一步起了作用，我估计是第二步，不过在教程中我优先推荐使用第二步。第二步遇到的坑是，在网上我们找到的教程只是输入`ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin`，但是执行多次都没有结果，WIN系统执行这步可能已经正确了。因为Mac环境权限的原因，这里加入sudo重新执行即可。

执行完成之后，重新进入书籍目录。

```
huixingdeMacBook-
Air:
import huixing$ cd jianli
huixingdeMacBook-
Air:
jianli huixing$ gitbook pdf . jianli.pdf

info:
7
 plugins are installed 

info:
6
 explicitly listed 

info:
 loading plugin 
"highlight"
... OK 

info:
 loading plugin 
"search"
... OK 

info:
 loading plugin 
"lunr"
... OK 

info:
 loading plugin 
"sharing"
... OK 

info:
 loading plugin 
"fontsettings"
... OK 

info:
 loading plugin 
"theme-default"
... OK 

info:
 found 
1
 pages 

info:
 found 
7
 asset files 

info:
>
>
generation finished with success in 
7.5
s ! 

info:
>
>
1
 file(s) generated 

```

执行完以上代码，进入书籍目录，即可看到已经转换完成的PDF了。大功告成！

特别感谢：Dandy，烟头γ两位大神的指导。

  


  


作者：慧行产品说

  


链接：https://www.jianshu.com/p/4824d216ad10

  


來源：简书

  


著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



