---
layout: "post"
title: "三星Galaxy Watch 5国行使用品鉴"
date: "2022-11-10 17：26"
---
作为伪三星粉最近搞了块三星Galaxy watch 5（后文简称GW5）手表。之所以看好gw5主要是喜欢它的圆表盘和wear OS 3的系统加持当然还有盼着有朝一日和google paly接轨以及以前有个gw active2的遗留问题。手表分国际版和国行版，国行版屏蔽了google套装，但是国际版又多了你400块钱还没保修。贫穷想象力让我趁着双11买了国行版。买之前在网络上大概搜了下国国行的面临的问题主要是只支持国行手机系统不过好在有人已经搞定了gw4的配对，那么gw5照抄应该问题不大。

gw4的国行手表配对教程主要是这一篇。gw5就不多说了有需要的可以参考这篇[博客](https://blog.xuegaogg.com/posts/1931/)。只支持国行手机是因为不能有google框架，有了框架就被判定为国际版手机我用的是lineage os 19自然当属非国行手机，那么在相关验证的时候就要禁用之。文章主要介绍的是配对和健康同步以及心电图血压之类的安装方法。这里我主要说一下配对细节问题，文章里提到的有些不太清楚。

绑定非国行手机引用文章里提到需要使用Wear OS的中国版。其实不使用中国版也可以直接使用Google Play版本的进行配对，但是配对的过程中几个节点需要注意，禁用Google Play和Google framework的时机。

1.  登录使用Wear OS for Android配对的时候不要禁用框架，否则闪退。如果任何遇到闪退的情况都是因为禁用框架的原因。显示已配对即可。让软件后台同步即可。  
2.  这一步比较急，需要立即进行配置，否则久了蓝牙就断开连接了导致初始化到一半就失败了。可以提前在play下载好三星穿戴和Watch 5 manager。这时打开穿戴app就会显示自己手表的蓝牙配件，可以利用app 设置中的删除存储和强行终止GW5manager进行初始化。同时使用冰箱冻结Google Play和Google framework就可以进行跳过国行检查，skip三星账户后，需要启用Google Play和Google framework转入Google相关的确认框否则闪退。两个google相关选项框禁用点下一步理论上就可以进行手表的初始化了。如果三星账户相关内容都可以在初始化完成后再行设置。有时候会出现白屏这时候就需要重复此步骤删除存储+强退重新打开穿戴，应该不需要重复1。也可能是wear os for android 掉了。关表重启重复1。  
3.  或者可以直接用官方给的配对意见进行配对,全程禁用框架。中国版的wear os会在配对中自动下载。  

> 连接方法如下：1）手机预先下载应用Galaxy Wearable（三星智能穿戴）、Samsang Health（三星健康）下载连接：http://apps.samsung.cn/gear
> 2）打开三星健康，并登录三星账户
> 在设置界面，找到配件，扫描配件，找到对应型号的手表连接；
> 
> 3）连接过程中，会提示下载Wear OS by Google、Galaxy Watch4 Plugin/Galaxy Watch5 Plugin（均为连接手表必备软件），点击允许下载安装；
> 
> 4）安装好无需打开，回到三星智能穿戴，根据步骤安装、允许权限使用，即可连接使用；
> 注意：连接手表使用时，会提示是否安装Wear OS by google及Galaxy Watch4 Plugin，需要全部安装才可以正常使用手表功能。
> Wear OS by google及Galaxy Watch4 Plugin/Galaxy Watch5 Plugin、SAMSUNG Health（三星健康）连接手表必备软件，不能删除。

下面主要说一下我面临的其他问题。

1.  **手机本身使用的整体是英文版的系统然后希望手表支持中文。**  
**wear os** 的系统语言是和手机里的GW5 manager的语言相匹配的，程序独立设置语言这个功能在android 13才被实现，所以lineage os 19目前还没有这个功能。所以只能用插件解决。推荐使用插件APP settings Reborn。这个插件目前可以解决app独立语言问题。设置中的关键字是Locale，其他默认即可。手机设置好后重启手表。  

2.  **因为使用过Galaxy Watch active 2，曾经把国行的手表刷成美版来解锁美版的商店和美版的运动附加功能。**  
**三星**账号归属是美国，导致和国行手表冲突。不能同步step 不能备份，不能各种舒服。解决方法是XPrivacyLua插件。之所以使用这个插件是因为定制化高，免费。这个插件可以自定义各种钩子，本来想尝试用此插件一起解决1的问题，但是好像没搞通。使用这个插件比较麻烦，主要的钩子项是TelephonyManager/getSimOperatin设置的给的运营商代号310440即可。需要拦截三星健康和穿戴相关程序让sim卡的归属到美国来解锁美国的相关功能。具体玩法参考[This](https://blog.1a23.com/2020/03/25/switch-galaxy-wearable-store-location-using-xprivacylua/)。可以直接在原脚本上赋值`fake=‘310410’`然后勾选即可。但是这个方法解决不了galaxy store 的中国版问题。手表上依然只能使用国行的市场。  
![Screenshot_20221110-012413_XPrivacyLua Pro.png](/assets/img/fd964aa6688a4aa39c618f6496122839.png)

3.  **支付宝和微信步数同步问题。**  
**微信**同步比较简单，下载“三星健康步数排行插件”即可解决，在play中下载一个Shortcut Maker创建一个插件的activaty即可激活插件，每次手动登陆微信运动才可同步步数。支付宝比较复杂需要将使用2的插件将Build.MANUFACTURER里的值设置成“samsung”并钩到支付宝上，这时候支付宝运动的设置里就多了可以和三星健康同步的设置了。如果有其他这种可以修改设置的插件也可以试试。  
![Screenshot_20221110-014027_三星健康步数排行插件.png](/assets/img/ecc55adf02424279995176b6d25e4373.png#center)
![Screenshot_20221110-014008_XPrivacyLua Pro.png](/assets/img/077f14dca7b0431cb51bcd70992e26b2.png)

4.  **三星pay如果没有三星手机暂时应该是废了？**  
**3和2**的方法可以运行play里的pay插件，但是无法连接到服务器绑不上卡。  
5.  **软件去哪下？**  
**apkmirro**r站可以下载一部分wear os软件，关键字是wear os，需要用adb进行安装，也可以手机装个wear installer之类的用手机加载。开发者模式的入口在关于>软件信息>软件版本。比较实用的比如pixel watch的表面，三星浏览器，shazam识歌，google massage，yaoyao跳绳，洗手提醒有点费电也不太实用只是好玩，sumsang自家的一些适配软件等。毕竟谷歌被阉掉了相当限制一大部分功能。可以逛逛xda的galaxy watch 4的条目。手机可以使用galaxy store的远古版本，可以到apkpure下载，但是只能限制中国版本切美版会启动不起来。国内有零星几个三方市场，软件也都是从别的表里提取的，适配程度很一般。有些功能主要还得靠手机的花式推送。比如使用automate或者是tasker之类的。  
没找到比较好的手表词典软件，不过从网页兼容性看，海词的mobile版和手表浏览器兼容性还是比较好的。有道也行但不推荐，因为有道的页面渲染比较复杂，加载速度明显不如海词的。
6.  **关于手表里的recoder的speech to text 问题。**  
**三星**的recoder其实是挺好的应用。导出的m4a文件是内嵌语音识别文字的，但是用非三星手机提取不来。用不了三星的recoder。不过可以用记事本打开提取内容。  


**吐槽**，wear os bug 太多。有时候按键会失灵有时候会卡，充满电一般玩个大概一天半的样子。小逼逼作为智能助手稍微弱了一点，来个英翻中都费事。期待谷歌助手。躺着的时候手势唤醒不咋好用。市场里的软件又老又烂。期望手表早日润出去。
<div align=center><img src="/assets/img/PXL_20221110_173812474.jpg" align=center></div>