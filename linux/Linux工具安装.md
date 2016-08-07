# Linux工具安装

## 目录

- [常用网站](#常用网站)
- [cygwin](#cygwin)
  - [安装源](#cygwin安装源)
  - [必需工具](#cygwin必需工具)
  - [默认进入 zsh](#cygwin_zsh_default)
  - [安装软件](#cygwin下安装软件)
  - [常见问题汇总](#cygwin常见问题汇总)
- [autojump安装和使用](#autojump安装和使用)
  - [安装](#autojump安装)
  - [配置](#autojump配置)
  - [使用](#autojump使用)
  - [问题解决](#autojump问题解决)
- [搜狗输入法](#搜狗输入法)
- [命令行翻译工具](#命令行翻译工具)
- [git vimdiff查看](#git_vimdiff查看)
- [Graphviz + CodeViz 生成 C/C++ 函数调用图](#Graphviz_CodeViz)
- [Ubuntu 安装 PPA 图形化管理软件 Y PPA Manager](#y_ppa_manager)
- [ubuntu安装python3的python-pip](#pip3)
- [Linux下最好用的微信客户端](#Electronic_WeChat)
- [FontAwesome图标字体的代码列表](#FontAwesome)
- [Markdown软件Haroopad安装](#Haroopad)
- [加快npm下载速度的方法](#加快npm下载速度的方法)
- [Haroopad中使用mermaid画流程图](#Haroopad中使用mermaid画流程图)
- [Linux 系统实时监控的瑞士军刀 —— Glances](#Linux 系统实时监控的瑞士军刀_Glances)
- [j4-dmenu-desktop](#j4_dmenu_desktop)
- [dmenu-extended](#dmenu_xtended)
- [i3-xfce](#i3_xfce)
- [unity-tweak-tool修改系统字体](#unity_tweak_tool)
- [Oh My Zsh](#Oh_My_Zsh)
- [极速蜗牛：apt-fast](#apt_fast)
- [Linux下的简单好用的计算器bc](#Linux下的简单好用的计算器bc)sudo apt-get update
sudo apt-get install i3 i3-wm i3blocks i3lock i3status 
- [i3 window manager](#i3_manager)

<a name="通信词典">
## 常用网站
</a>

|名称|地址|说明|
|---|----|----|
|[通信词典](http://www.mscbsc.com/cidian/)|http://www.mscbsc.com/cidian/|开放、专业、智能的通信词语解释大全|
|[IETF Tools](https://tools.ietf.org/)|https://tools.ietf.org/|在线查看、下载RFC文档|

<a name="cygwin">
## cygwin
</a>

<a name="cygwin安装源">
### 安装源
</a>

> http://mirrors.163.com/cygwin/
> http://www.cygwin.cn/pub/
> ftp://cygwin.uib.no

<a name="cygwin必需工具">
### 必需工具
</a>

|功能|工具|
|---|:---:|
|编译工具|gcc make cmake automake libtool|
|窗口管理器|tmux|
|编辑器|vim|
|代码管理|git subversion|
|下载|wget curl|
|shell|zsh|
|man手册|man-pages-posix|

<a name="cygwin_zsh_default">
### 默认进入 zsh
</a>

Cygwin中默认进入zsh配置步骤如下：
1. 编辑~/.bash_profile
  > `vim ~/.bash_profile`  

2. 在最后一行加入：`exec zsh`

保存退出，下次进入就是 zsh 了。

<a name="cygwin下安装软件">
### 安装软件
</a>

很多时候，我们在windows下安装完cygwin后，使用时发现装少了软件。那么怎么办？
- 1）有的人说用setup.exe那个玩意再搞一遍。个人比较觉得那个方法蛋疼。
- 2）有的人说用find命令，怎么安装之类的，也不太爽。
- 3）后来发现**apt-cyg**这个程序，真是强大啊。使用方法和ubuntu下的apt-get一样。爽死啦。


安装apt-cyg的方法如下（在cygwin中输入如下命令）：
> `lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg`
> `chmod +x /bin/apt-cyg`

使用apt-cyg来安装软件：
> `apt-cyg install git-core gnupg flex bison gperf build-essential zip curl`


<a name="cygwin常见问题汇总">
### 常见问题汇总
</a>

1. 编译链接动态库时，出现找不到链接库文件的问题
  > cygwin中默认搜索后缀名为*.dll的动态库，因此，只需要将原.so的动态库文件链接为.dll即可。


<a name="autojump安装和使用">
## autojump安装和使用
</a>

<a name="autojump安装">
### 安装
</a>

1. 克隆autojump的repo，Terminal下执行：
  > `git clone git://github.com/joelthelion/autojump.git`

2. 然后进入clone下来的目录，执行安装脚本：
  > `./install.python`

在安装过程中，会在～/下建立.autojump文件夹。

<a name="autojump配置">
### 配置
</a>

1. 首先，在shell的配置文件.zshrc中添加如下配置信息
  > [[ -s ~/.autojump/etc/profile.d/autojump.zsh ]] && . ~/.autojump/etc/profile.d/autojump.zsh

2. 重新加载配置文件，令刚才添加的配置信息生效，Terminal下执行：
  > `source ~/.zshrc`

3. 配置完成

<a name="autojump使用">
### 使用
</a>

　　**工作原理**：它会在你每次启动命令时记录你当前位置，并把它添加进它自身的数据库中。这样，某些目录比其它一些目录添加的次数多，这些目录一般就代表你最重要的目录，而它们的“权重”也会增大。
　　详细使用说明如下：

|功能|命令|说明|
|---|----|----|
|目录跳转|j [目录的名字或名字的一部分]|不受当前所在目录的限制|
|查看当前权重|j --stat|无|
|进入权重最高的目录|j|无|
|改变权重值|j -i [权重]<br>j -d [权重]|增加或减少权重|

　　刚开始掌握autojump的使用可能会需要少量的时间和学习成本，但是掌握之后会极大地提高工作效率。  
　　Autojump：一个可以在Linux文件系统快速导航的高级cd命令：http://www.linuxdiyf.com/linux/13220.html

<a name="autojump问题解决">
### 问题解决
</a>

使用中出现了如下问题：
~~~
zsh compinit: insecure directories, run compaudit for list.
Ignore insecure directories and continue [y] or abort compinit [n]?
~~~

解决方法：
  > `compaudit | xargs chmod g-w`

<a name="搜狗输入法">
## 搜狗输入法
</a>

```
sudo add-apt-repository ppa:fcitx-team/nightly
sudo apt-get update
sudo apt-get install fcitx libopencc-dev libopencc1 fcitx-libs fcitx-libs-dev fcitx-libs-qt
sudo dpkg -i sogoupinyin_2.0.0.0078_i386.deb
```
系统注销或重启后即可使用。

<a name="命令行翻译工具">
## 命令行翻译工具
</a>

![linux命令行翻译工具](http://i.imgur.com/09Ldu2W.png "linux命令行翻译工具")

```
sudo apt-get install ruby
sudo gem install fy  
```

<a name="git_vimdiff查看">
## git vimdiff查看
</a>

~~~
git config --global diff.tool vimdiff
git config --global difftool.prompt false
git config --global alias.d difftool
~~~
Typing `git d` yields the expected behavior, typing `:wq` in vim cycles to the next file in the changeset. 

<a name="Graphviz_CodeViz">
## Graphviz + CodeViz 生成 C/C++ 函数调用图
</a>

<a name="Graphviz和CodeViz编译安装">
### Graphviz和CodeViz编译安装
</a>

> 1. 安装gcc依赖库
> `sudo apt-get install libgmp3-dev libmpfr-dev libmpc-dev`

> 2. 安装图形绘制库
> `sudo apt-get install graphviz`

> 3. 安装 GCC
> 下载gcc-4.6.2.tar.gz到 cd codeviz-1.0.12目录下的compilers里。
> 下载地址：ftp://ftp.gnu.org/pub/gnu/gcc/gcc-4.6.2/gcc-4.6.2.tar.gz

> 4. 下载CodeViz
> `wget -c http://www.csn.ul.ie/~mel/projects/codeviz/codeviz-1.0.12.tar.gz`

> 5. 安装codeviz
> `tar -zxvf codeviz-1.0.3.tar.gz`
> `cd codeviz-1.0.3`
> `./configure && sudo make install-codeviz`

<a name="y_ppa_manager">
## Ubuntu 安装 PPA 图形化管理软件 Y PPA Manager
</a>

> `sudo add-apt-repository ppa:webupd8team/y-ppa-manager`
> `sudo apt-get update`
> `sudo apt-get install y-ppa-manager`

<a name="pip3">
## ubuntu安装pip3
</a>

> `sudo apt-get install python3-pip`
> `sudo pip3 install packagename`

<a name="Electronic_WeChat">
## Linux下最好用的微信客户端
</a>

> `# Clone this repository`
> `git clone https://github.com/geeeeeeeeek/electronic-wechat.git`
> `# Go into the repository`
> `cd electronic-wechat`
> `# Install dependencies and run the app`
> `npm install && npm start`


<a name="FontAwesome">
## FontAwesome图标字体的代码列表
</a>

> [FontAwesome图标字体的代码列表](http://www.bootcss.com/p/font-awesome/design.html)

<a name="Haroopad">
## Markdown软件Haroopad安装
</a>

1. Haroopad下载
> [https://bitbucket.org/rhiokim/haroopad-download/downloads](https://bitbucket.org/rhiokim/haroopad-download/downloads) 或者 [http://pad.haroopress.com/user.html#download](http://pad.haroopress.com/user.html#download)

2. 安装
> `wget https://bitbucket.org/rhiokim/haroopad-download/downloads/haroopad-v0.12.2-i386.deb`
> `sudo apt-get install gdebi`
> `sudo gdebi haroopad-v0.12.2-i386.deb`

3. Haroopad使用
> Haroopad使用可参考文章: *[最好用的离线markdown编辑器Haroopad介绍](http://www.jianshu.com/p/1ff6e833e2e6/comments/2758337)*。

4. 其他
> 安装步骤还可参照文章: *[How To Install Haroopad 0.12.2 On Ubuntu, Debian And Derivative Systems](http://linuxg.net/how-to-install-haroopad-0-12-2-on-ubuntu-debian-and-derivative-systems/)*.

<a name="加快npm下载速度的方法">
## 加快npm下载速度的方法
</a>

1. 关闭npm的https
> `npm config set strict-ssl false`

2. 设置npm的获取地址
> `npm config set registry "http://registry.npmjs.org/"`

3. 增加参数查看进度
> 为了解决安装时卡着没反应，聪明的人类发现了可以加参数，例如：
> `npm install hexo -g --verbose`

4. 使用smart-npm加快下载速度
> `npm install --global smart-npm --registry=https://registry.npm.taobao.org/`
> 安装可参考*[smart-npm](https://github.com/qiu8310/smart-npm)*

5. 其他
> 其他方法可参考文章: *[NPM太慢了怎么办](http://www.tuicool.com/articles/eUJNfm)*、*[加快npm的下载速度](http://cnodejs.org/topic/53330242edf0031c2c00ca81)*

<a name="Haroopad中使用mermaid画流程图">
## Haroopad中使用mermaid画流程图
</a>

1. 安装mermaid
> `npm install -g mermaid`
> `npm install -g phantomjs`

2. 使用
代码如下：  
```
~~~mermaid
graph LR;
	A-->B;
    A-->C;
    B-->D;
    C-->D;
~~~
```
效果如下：  
~~~mermaid
graph LR;
	A-->B;
    A-->C;
    B-->D;
    C-->D;
~~~

说明：
1. 安装步骤可参考文章*[用代码画流程图和时序图快餐教程(2) - mermaid数据流图速成](https://yq.aliyun.com/articles/53909)*；
2. mermaid使用可参考*[http://knsv.github.io/mermaid/mermaidCLI.html](http://knsv.github.io/mermaid/mermaidCLI.html)*；

<a name="Linux 系统实时监控的瑞士军刀_Glances">
## Linux 系统实时监控的瑞士军刀 —— Glances
</a>

> `sudo apt-add-repository ppa:arnaud-hartmann/glances-stable`
> `sudo apt-get update`
> `sudo apt-get install glances```language

说明：安装及说明可参考*[Linux 系统实时监控的瑞士军刀 —— Glances](https://linux.cn/article-2782-1.html)* 或者 *[使用资源监控工具 glances](http://www.ibm.com/developerworks/cn/linux/1304_caoyq_glances/)*。

<a name="j4_dmenu_desktop">
## j4-dmenu-desktop
</a>

> `git clone https://github.com/enkore/j4-dmenu-desktop`
> `cd j4-dmenu-desktop`
> `mkdir build && cd build` 
> `cmake ..` 
> `make` 
> `sudo make install` 

<a name="dmenu_xtended">
## dmenu-extended
</a>

> `sudo apt-get install suckless-tools xfonts-terminus` 
> `git clone https://github.com/markjones112358/dmenu-extended` 
> `cd dmenu-extended` 
> `sudo python setup.py install` 

<a name="i3_xfce">
## i3-xfce
</a>

> `sudo add-apt-repository ppa:ansible/ansible`
> `sudo add-apt-repository ppa:aacebedo/i3-xfce-stable`
> `sudo apt-get update`
> `sudo apt-get install i3-xfce`
> `sudo i3-xfce install`

<a name="unity_tweak_tool">
## unity-tweak-tool修改系统字体
</a>

> `sudo apt-get install unity-tweak-tool ` 

<a name="Oh_My_Zsh">
## Oh My Zsh 
</a>

<a name="Oh_My_Zsh安装">
### 安装
</a>

> `sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"` 

<a name="Oh_My_Zsh插件">
### 插件
</a>

> 1. `git clone https://github.com/zsh-users/zsh-completions ~/.oh-my-zsh/custom/plugins/zsh-completions` 
> 2. `git clone git://github.com/jimmijj/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting`

同时，在~/.zshrc中配置如下参数：  
> `plugins+=(zsh-syntax-highlighting zsh-completions)`

<a name="apt_fast">
## 极速蜗牛：apt-fast
</a>

　　如果你在Debian或Ubuntu系统上经常感觉到apt-get 或 aptitude包安装速度过慢，那么这里就有几种改善这一情况的方法。你有没有考虑过改变正被使用的默认镜像站点？你有没有排除因特网连接的上游带宽成为瓶颈的可能？
　　如果不是这些原因，你可以尝试第三个选择：使用apt-fast工具。apt-fast实际上是一个围绕apt-get和aptitude所写的shell脚本容器，它能加速包的下载速度。apt-fast本质上采用aria2下载工具，这款工具能够以“块”的方式从多个镜像并行下载一个文件（就像BitTorrent下载）。
　　Ubuntu 14.04 以及更高版本安装：  

> `sudo add-apt-repository ppa:saiarcot895/myppa`
> `sudo apt-get update`
> `sudo apt-get install apt-fast`

　　选择完那些地理上靠近你的镜像后，你需按照下面的格式将选择的镜像加入到/etc/apt-fast.conf。

　　Ubuntu/Mint：

    MIRRORS=('http://us.archive.ubuntu.com/ubuntu,http://mirror.cc.columbia.edu/pub/linux/ubuntu/archive/,http://mirror.cc.vt.edu/pub2/ubuntu/,http://mirror.umd.edu/ubuntu/,http://mirrors.mit.edu/ubuntu/')

<a name="Linux下的简单好用的计算器bc">
## Linux下的简单好用的计算器bc
</a>

1. 关于bc
bc是任意精度计算器语言，通常在linux下当计算器用，简单好用。相当于windows下的计算器。

2. 支持的运算符
基本的数学运算： + 加法 - 减法 * 乘法 / 除法 ^ 指数 % 余数
还支持表达式， 逻辑运算， 数学函数。

3. 使用
在linux下输入bc

        $ bc
        bc 1.06
        Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
        This is free software with ABSOLUTELY NO WARRANTY.
        For details type `warranty'.
然后输入运算，按回车会输出运算结果

        2+5
        7

4. 通过管道
bc支持传入参数方式。下面使用管道来试试。 
        $ echo "3+4" | bc
        7

<a name="i3_manager">
## i3 window manager
</a>

### 安装

> `sudo apt-get update`
> `sudo apt-get install i3 i3-wm i3blocks i3lock i3status`
> `sudo apt-get install pactl xbacklight`
> `sudo apt-get install rofi`
> `sudo apt-get install compton`

可参考文章：[setupi3](https://github.com/alexbooker/setupi3)。