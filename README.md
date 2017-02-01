# 关于

生成 Dash 格式的微信小程序的离线文档。

# 直接使用

下载我编译好的 [minapp.docset](https://github.com/kamidox/html2Dash/releases/download/minapp-docset-V0.1/minapp.docset.v0.1.tar.gz) ，添加到 Dash 里即可。如果你不知道 Dash 是什么，去了解一下绝对赚到。在 Linux/Windows 下也有相应的替代品。在此不赘述。

# 自己生成微信小程序离线文档

## 步骤一：下载微信小程序文档

我们使用 wget 把微信小程序的开发文档全部下载下来。

```shell
$ mkdir -p ~/temp/wxadoc
$ cd ~/temp/wxadoc
$ wget -r -p -k -np https://mp.weixin.qq.com/debug/wxadoc/dev/
```

成功下载后的目录树大概长这样子：

```shell
$ tree -L 2
.
├── dev
│   ├── api
│   ├── component
│   ├── demo
│   ├── demo.html
│   ├── demo.html?t=2017117.html
│   ├── devtools
│   ├── framework
│   ├── image
│   ├── index.html
│   ├── index.html?t=2017117.html
│   ├── index.html?t=2017119.html
│   ├── qa.html
│   └── qa.html?t=2017117.html
└── gitbook
    ├── fonts
    ├── gitbook-plugin-highlight
    ├── gitbook-plugin-lunr
    ├── gitbook-plugin-search
    ├── gitbook.js?t=2017117
    ├── gitbook.js?t=2017119
    ├── images
    ├── style.css?t=2017117.css
    ├── style.css?t=2017119.css
    ├── theme.js?t=2017117
    └── theme.js?t=2017119

13 directories, 13 files
```

## 步骤二：转换成 Dash 格式的 docset

```shell
$ python html2dash.py -n minapp -d ./ -i ~/temp/wxadoc/mp.weixin.qq.com/debug/wxadoc/gitbook/images/icon_note_logo@2x.png -p dev/framework/MINA.html ~/temp/wxadoc/mp.weixin.qq.com/debug/wxadoc

Create the Docset Folder!
Copy the HTML Documentation!
Create the SQLite Index
Create the Info.plist File
Create the Icon for the Docset!
Generate Docset Successfully!
```

运行之前需要安装 Python，另外还需要安装 beautifulsoap4。

```shell
$ pip install beautifulsoup4==4.3.2
```

运行成功后，会在当前目录生成 minapp.docset 目录。直接导入 Dash 即可使用。

-------------------------------------------------------------------------------

# html2Dash

html2Dash is an Documentation Set generator intended to be used with the [Dash.app](http://kapeli.com/dash/) API browser for OS X or one of its many clones. html2Dash is just like [doc2dash](https://github.com/hynek/doc2dash) but generating docset from any HTML documentations.

If you’ve never heard of Dash.app, you’re missing out: together with html2Dash it’s all your API documentation at your fingertips!

Third part library required:

    beautifulsoup4==4.3.2

It’s tested on Python 2.7, OS X 10.9.

# How to Use

The usage is as simple as:

	$ html2Dash <htmldir>

html2dash will create a new directory called `<htmldir>.docset` in `~/Library/Application Support/html2dash/DocSets` containing a Dash.app-compatible docset. When finished, the docset is automatically added to Dash.app.

**Options and Arguments**

The full usage is:

	$ doc2dash [OPTIONS] SOURCE

The `SOURCE` is a directory containing the HTML documents you would like to convert.

Valid `OPTIONS` are the following:

* -n, --name

	Name the docset explicitly instead of letting doc2dash guess the correct name from the directory name of the source.

* -d PATH, --destination PATH

	Put the resulting docset into PATH. Default is the directory `~/Library/Application Support/html2dash/DocSets`

* -i FILENAME, --icon FILENAME

	Add PNG icon FILENAME to docset that is used within Dash.app to represent the docset.

* -p INDEX_PAGE, --index-page INDEX_PAGE

	Set the file that is shown when the docset is clicked within Dash.app.

* -h, --help

	Show a brief usage summary and exit.

DEPENDENCIES:

* BeautifulSoup HTML parsing library

# Demo

Generate the Docset for requests: `requests.docset`. Command：

    $ ./html2dash.py -n requests -i ~/Documents/requests-sidebar.png ~/Documents/requests
    Create the Docset Folder!
    Copy the HTML Documentation!
    Create the SQLite Index
    Create the Info.plist File
    Create the Icon for the Docset!
    Generate Docset Successfully!


