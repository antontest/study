<a name="HTML,CSS学习笔记">
# HTML,CSS学习笔记
</a>

<a name="目录">
## 目录
</a>

- [字体式样](#字体式样)
  - [字体颜色](#字体颜色)
  - [字体背景颜色](#字体背景颜色)
  - [字体加粗](#字体加粗)
- [垂直导航栏](#垂直导航栏)

<a name="字体式样">
## 字体式样
</a>

<a name="字体颜色">
### 字体颜色
</a>

```
<font color="green">字体背景颜色</font>
```

<a name="字体背景颜色">
### 字体背景颜色
</a>

```
<font style="background-color:yellow">字体背景颜色</font>
```

<a name="字体加粗">
### 字体加粗
</a>

```
<font style="font-weight: bold;">字体加粗</font>
```

<a name="垂直导航栏">
## 垂直导航栏
</a>

```
<style type="text/css">
.top span {
	position:fixed;
	top: 10px; 
	left: 10px;
	width: 100px; 
	text-decoration: none;
	/*font-weight: bold;*/
	color: green;
	padding: 5px;
	border: 1px gray solid;
}

.top a {
	color: green;
	text-decoration: none;
}
</style>
<div class="top">
<span><a href="#">回到最顶部</a></span>
</div>

<style type="text/css">
/*---------竖向菜单（非必需）---------*/
.bl-vernav li{ 
	border-bottom: 1px solid #ddd; 
	margin-bottom: 0px;
	padding-top: 1px;
	cursor: pointer;
}
.bl-vernav a{ 
	height: 10px; 
	line-height: 10px; 
	padding:10px 10px;
	display:block;
}
.bl-vernav a:hover{ 
	background: #E2144A;
	text-decoration: none;
}
/*
.bl-vernav .cur a{ 
	background: #428BCA; 
	color: #fff;
}
*/

.bl-vernav-ord{ 
	border: 1px solid #ddd;
}
.vernav-level li li{ 
	border-left: none;
	border-right: none;
}
.vernav-level li li a{ 
	padding-left: 10px;
	font-size: 15px;
	height: 15px; 
}
.vernav-level li li a:hover { 
	color: #E2144A; 
	background: #f9f9f9; 
} /* Hover Styles */
.vernav-level .one{ 
	background: #F9F9F9; 
	font-size: 16px;
	height: 16px; 	
	line-height: 16px; 
	margin:0 auto;
	font-weight:bold;
}
.vernav-level li .cur a{ 
	background: #F8F8F8;
}

.popup span {
	position:fixed;
	top: 45px; 
	left: 10px;
	width: 100px; 
	text-decoration: none;
	/*font-weight: bold;*/
	color: green;
	padding: 5px;
	border: 1px gray solid;
}
.popup .box div {
	display:none;
}
.box span:hover div {
	display: block;
	top: -1200px;
	left: 0px; 
	width: 320px; 
	height: 500px;
	relative: absolute;
	overflow-y: auto;
	overflow-x: hidden;
	border: 1px gray solid;
	/*
	padding: 10px;
	border: 1px #00FF00 solid;
	*/
	background-color: #F8F8F8;
	font-size: 14px; 
	font-family: 'Hiragino Sans GB','Microsoft Yahei',"WenQuanYi Micro Hei",SimSun,Tahoma,Arial,Helvetica,STHeiti;
}
/*下面这两端是演示用的和整个功能没有必然关系 ，你可以使用你自己的 字体字号颜色设置*/
.popup .box .demobox .bl-vernav-warp .vernav-level { 
	overflow-y: auto;
	top: -600px;
	left: 0px; 
	width: 300px; 
	height: 100%;
}
</style>

<div class="popup">
	<div class="box">
	<span>导航栏
		<div class="demobox">
			<ul class="bl-vernav vernav-level">
				<li><a href="#南京电信测试资料整理" class="one">南京电信测试资料整理</a></li>
				<li><a href="#目录" class="one">目录</a></li>
				<li class="cur">
					<a href="#ITMS平台" class="one">ITMS平台</a>
					<ul>
						<li><a href="#ITMS平台地址">ITMS平台地址</a></li>
						<li><a href="#ITMS平台登陆信息">ITMS平台登陆信息</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#逻辑ID" class="one">逻辑ID</a>
					<ul>
						<li><a href="#LOID范围">LOID范围</a></li>
						<li><a href="#GPON逻辑ID">GPON逻辑ID</a></li>
						<li><a href="#EPON逻辑ID">EPON逻辑ID</a></li>
						<li><a href="#南京电信分公司LOID">南京电信分公司LOID</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#PPPoE拨号帐号" class="one">PPPoE拨号帐号</a>
					<ul>
						<li><a href="#南京NOC_PPPoE拨号帐号">南京NOC PPPoE拨号帐号</a></li>
						<li><a href="#南京电信分公司PPPoE拨号帐号">南京电信分公司PPPoE拨号帐号</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#终端登录信息" class="one">终端登录信息</a>
					<ul>
						<li><a href="#查看WEB登陆密码">查看WEB登陆密码</a></li>
						<li><a href="#Debug页面功能">Debug页面功能</a></li>
						<li><a href="#终端串口登陆信息">终端串口登陆信息</a></li>
						<li><a href="#终端Telnet登陆信息">终端Telnet登陆信息</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#IPTV相关信息" class="one">IPTV相关信息</a>
					<ul>
						<li><a href="#机顶盒设置密码">机顶盒设置密码</a></li>
						<li><a href="#vlc组播源">vlc组播源</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#INTERNET数据测试网址" class="one">INTERNET数据测试网址</a>
					<ul>
						<li><a href="#IPv6测试相关网址">IPv6测试相关网址</a></li>
						<li><a href="#FTP测试网址">FTP测试网址</a></li>
						<li><a href="#带宽测试网址">带宽测试网址</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#VOIP相关信息" class="one">VOIP相关信息</a>
					<ul>
						<li><a href="#VOIP登陆信息">VOIP登陆信息</a></li>
						<li><a href="#VOIP_IMS设置">VOIP IMS设置</a></li>
						<li><a href="#VOIP软交换设置">VOIP软交换设置</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#EPON、GPON版本信息" class="one">EPON、GPON版本信息</a>
					<ul>
						<li><a href="#E8C终端信息">E8C终端信息</a></li>
						<li><a href="#E8C终端信息设置命令">E8C终端信息设置命令</a></li>
					</ul>
				</li>
				<li class="cur">
					<a href="#终端操作" class="one">终端操作</a>
					<ul>
						<li><a href="#升级img">升级img</a></li>
						<li><a href="#恢复出厂设置">恢复出厂设置</a></li>
						<li><a href="#修改ACS">修改ACS</a></li>
						<li><a href="#终端修改MAC地址操作">终端修改MAC地址操作</a></li>
						<li><a href="#路由拨号不能上网问题解决">路由拨号不能上网问题解决</a></li>
						<li><a href="#终端硬件、软件版本查看及设置">终端硬件、软件版本查看及设置</a></li>
						<li><a href="#终端抓包">终端抓包</a></li>
						<li><a href="#Wireshark抓包过滤">Wireshark抓包过滤</a></li>
						<li><a href="#修改软件版本">修改软件版本</a></li>
						<li><a href="#设置多终端上网">设置多终端上网</a></li>
						<li><a href="#设置默认配置文件">设置默认配置文件</a></li>
						<li><a href="#设置PON类型">设置PON类型</a></li>
						<li><a href="#LOID烧制">LOID烧制</a></li>
						<li><a href="#VOIP_log开关">VOIP log开关</a></li>
					</ul>
				</li>
			</ul>
		</div>
		</span>
	</div>
</div>
```