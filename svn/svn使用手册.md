# SVN 使用手册

## 目录

- [常用命令](#常用命令)
  - [检出](#检出)
  - [导出](#导出)
  - [添加新文件](#添加新文件)
  - [提交](#提交)
  - [更新文件](#更新文件)
  - [删除文件](#删除文件)
  - [加锁解锁](#加锁解锁)
  - [比较差异](#比较差异)
  - [查看状态](#查看状态)
  - [查看日志](#查看日志)
  - [查看文件详细信息](#查看文件详细信息)
  - [查看版本库下的文件和目录列表](#查看版本库下的文件和目录列表)
  - [创建纳入版本控制下的新目录](#创建纳入版本控制下的新目录)
  - [恢复本地修改](#恢复本地修改)
  - [把工作拷贝更新到别的URL](#把工作拷贝更新到别的URL)
  - [新建一个分支copy](#新建一个分支copy)
  - [合并内容到分支merge](#合并内容到分支merge)

<a name="常用命令">
## 常用命令
</a>

<a name="检出">
### 检出
</a>

1. 功能
  > 从svn服务器上下载最新code，带.svn文件夹目录树。

2. 命令格式
  > `svn checkout http://路径(目录或文件的全路径)　[本地目录全路径] --username　用户名  --password 密码`
  > `svn checkout svn://路径(目录或文件的全路径)　[本地目录全路径] --username　用户名 --password 密码`

3. 命令缩写
  > `svn co`

4. 说明
  > 1. 如果不带\-\-password 参数传输密码的话，会提示输入密码，建议不要用明文的\-\-password 选项；
  > 2. 不指定本地目录全路径，则检出到当前目录下；

5. 示例
  > `svn co svn://localhost/测试工具 /home/testtools --username wzhnsc`
  > `svn co http://localhost/test/testapp --username wzhnsc`
  > `svn checkout svn://localhost/测试工具 /home/testtools --username wzhnsc`
  > `svn checkout http://localhost/test/testapp --username wzhnsc`

<a name="导出">
### 导出
</a>

1. 功能
  > 导出一个干净的不带.svn文件夹的目录树。

2. 命令格式
  > `svn export [-r 版本号] http://路径(目录或文件的全路径) [本地目录全路径]　--username　用户名`
  > `svn export [-r 版本号] svn://路径(目录或文件的全路径) [本地目录全路径]　--username　用户名`
  > `svn export 本地检出的(即带有.svn文件夹的)目录全路径  要导出的本地目录全路径`

3. 说明

  > 如果指定了修订版本号，会导出相应的版本，
  > 如果没有指定修订版本，则会导出最新的，导出到指定位置。
  > 如果省略 本地目录全路径，URL的最后一部分会作为本地目录的名字。

4. 示例
  > `svn export svn://localhost/测试工具 /home/testtools --username wzhnsc`
  > `svn export svn://localhost/test/testapp --username wzhnsc`
  > `svn export /home/testapp /home/testtools`

<a name="添加新文件">
### 添加新文件 
</a>

1. 功能
  > 添加新文件。

2. 命令格式
  > `svn　add 文件名`

3. 说明
  > 告诉SVN服务器要添加文件了，还要用svn commint -m真实的上传上去！

4. 示例
  > `svn add test.php ＜－ 添加test.php`
  > `svn commit -m “添加我的测试用test.php“ test.php`
  > `svn add *.php ＜－ 添加当前目录下所有的php文件`
  > `svn commit -m “添加我的测试用全部php文件“ *.php`

<a name="提交">
### 提交 
</a>

1. 功能
  > 将本地代码提交到svn服务器。

2. 命令格式
  > `svn　commit　-m　"提交备注信息文本"　[-N]　[--no-unlock]　文件名`
  > `svn　ci　-m　"提交备注信息文本"　[-N]　[--no-unlock]　文件名`

3. 命令缩写
  > `svn ci`

4. 说明
  > 必须带上-m参数，参数可以为空，但是必须写上-m

5. 示例
  > `svn commit -m “提交当前目录下的全部在版本控制下的文件“ * ＜－ 注意这个*表示全部文件`
  > `svn commit -m “提交我的测试用test.php“ test.php`
  > `svn commit -m “提交我的测试用test.php“ -N --no-unlock test.php ＜－ 保持锁就用–no-unlock开关`
  > `svn ci -m “提交当前目录下的全部在版本控制下的文件“ * ＜－ 注意这个*表示全部文件`
  > `svn ci -m “提交我的测试用test.php“ test.php`
  > `svn ci -m “提交我的测试用test.php“ -N --no-unlock test.php ＜－ 保持锁就用–no-unlock开关`

<a name="更新文件">
### 更新文件 
</a>

1. 功能
  > 将本地代码更新到指定版本。

2. 命令格式
  > `svn　update`
  > `svn　update　-r　修正版本　文件名`
  > `svn　update　文件名`

3. 命令缩写
  > `svn up`

4. 示例
  > `svn update <- 后面没有目录，默认将当前目录以及子目录下的所有文件都更新到最新版本`
  > `svn update -r 200 test.cpp <- 将版本库中的文件 test.cpp 还原到修正版本（revision）200`
  > `svn update test.php <- 更新与版本库同步。`

<a name="删除文件">
### 删除文件 
</a>

1. 功能
  > 将文件从本地和服务器上删除。

2. 命令格式
  > `svn　delete　svn://路径(目录或文件的全路径) -m "删除备注信息文本"`

3. 操作步骤
  > `svn　delete　文件名`
  > `svn　ci　-m　"删除备注信息文本"`

4. 示例
  > `svn delete test.php`
  > `svn ci -m "删除测试文件test.php"`

<a name="加锁解锁">
### 加锁解锁 
</a>

1. 功能
  > 加锁、解锁。

2. 命令格式
  > `svn　lock　-m　"加锁备注信息文本"　[--force]　文件名`
  > `svn　unlock　文件名`

3. 示例
  > `svn lock -m "锁信测试用test.php文件" test.php`
  > `svn unlock test.php`

<a name="比较差异 ">
### 比较差异  
</a>

1. 功能
  > 比较差异。

2. 命令格式
  > `svn　diff　文件名`
  > `svn　diff　-r　修正版本号m:修正版本号n　文件名`

3. 示例
  > `svn diff test.php＜－ 将修改的文件与基础版本比较`
  > `svn diff -r 200:201 test.php＜－ 对 修正版本号200 和 修正版本号201 比较差异`

<a name="查看状态">
### 查看状态 
</a>

1. 功能
  > 查看文件或者目录状态。

2. 命令格式
  > `svn st 目录路径/名`
  > `svn status 目录路径/名`

3. 说明
  > ?：不在svn的控制中；
  > M：内容被修改；
  > C：发生冲突；
  > A：预定加入到版本库；
  > K：被锁定

<a name="查看日志">
### 查看日志 
</a>

1. 功能
  > 查看日志。

2. 命令格式
  > `svn　log　文件名`

3. 示例
  > `svn log test.php <- 显示这个文件的所有修改记录，及其版本号的变化`

<a name="查看文件详细信息">
### 查看文件详细信息 
</a>

1. 功能
  > 查看文件详细信息。

2. 命令格式
  > `svn　info　文件名`

3. 示例
  > `svn info test.php`

<a name="查看版本库下的文件和目录列表  ">
### 查看版本库下的文件和目录列表  
</a>

1. 功能
  > 查看版本库下的文件和目录列表 。

2. 命令格式
  > `svn　list　svn://路径(目录或文件的全路径)`
  > `svn　ls　svn://路径(目录或文件的全路径)`

3. 缩写
  > `svn ls`

4. 示例
  > `svn list svn://localhost/test`


<a name="恢复本地修改   ">
### 恢复本地修改   
</a>

1. 功能
  > 恢复本地修改。

2. 命令格式
  > `svn　revert　[--recursive]　文件名`

3. 说明
  > 本子命令不会存取网络，并且会解除冲突的状况。但是它不会恢复被删除的目录。

4. 示例
  > `svn revert foo.c <- 丢弃对一个文件的修改`
  > `svn revert --recursive . <- 恢复一整个目录的文件，. 为当前目录 `

<a name="把工作拷贝更新到别的URL">
### 把工作拷贝更新到别的URL 
</a>

1. 功能
  > 把工作拷贝更新到别的URL。

2. 命令格式
  > `svn　switch　http://目录全路径　本地目录全路径`

3. 示例
  > `svn switch http://localhost/test/456 . <- (原为123的分支)当前所在目录分支到localhost/test/456`

<a name="新建一个分支copy">
### 新建一个分支copy 
</a>

1. 功能
  > 新建一个分支copy。

2. 命令格式
  > `svn copy branchA branchB -m "make B branch"`

3. 示例
  > `svn copy branchA branchB  -m "make B branch" // 从branchA拷贝出一个新分支branchB`

<a name="合并内容到分支merge">
### 合并内容到分支merge 
</a>

1. 功能
  > 合并内容到分支merge。

2. 命令格式
  > `svn merge branchA branchB`

3. 示例
  > `svn merge branchA branchB  // 把对branchA的修改合并到分支branchB`



