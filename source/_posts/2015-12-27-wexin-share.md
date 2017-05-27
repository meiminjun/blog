title: 微信开发-朋友、朋友圈分享
date: 2015-12-27 10:44:22
tags:
	- 微信开发
---

先看个效果图：
![微信分享](/images/blogImg/weixin1227_1.jpg)

目前来说，对于前端开发者来说想要自定义来让分享出去的文章有图标和标题有两种方式，一种是通过微信提供的sdk进行开发，另外一种是通过一些小方法来达到同样目的，下面就向大家介绍一下：

<!-- more -->

# 不通过微信sdk的方式巧妙解决方式:
以图片中第一个分享为例，标题为“微信标题测试”,代码如下：
``` bash
// 在你的html中的title
<html>
	<head>
		<!-- ** 此处就是你的标题 ** -->
		<title>微信标题测试</title>
	</head>
	<body>
		<!-- ** 此处就是你的图标，但是图片大小一定要大于等于300*300 才会有显示 ** -->
		<img src="http://sandbox.runjs.cn/uploads/rs/438/v2eacmoa/2.png">
	</body>
</html>
```
几点注意的地方:
* img标签一定要尽量靠近body标签，否则无效果
* 如果当你的文章中木有图片你将咋办呢？我是这样解决的：将图片宽度width="0%"，就可以了

> `这个方式不好的地方在于,无法自定义内容，导致分享出去的内容框中是个链接`

# 通过官方sdk进行分享
## 第一步：微信公众号中设置绑定域名，只有绑定的域名下的网页才可以调用微信官方的js，否则会报错，目前域名可以绑定3个（绑定步骤如下）

1. ** 进入公众号，点击左边主菜单栏“设置”→“公众号设置” **
![微信分享](/images/blogImg/weixin1227_2.jpg)
1. ** 然后点击上方的“功能设置” **
![微信分享](/images/blogImg/weixin1227_3.jpg)

## 第二步：在自己的网页中引入微信官方js：http://res.wx.qq.com/open/js/jweixin-1.0.0.js
> 如果你的页面启用了https，务必引入 https://res.wx.qq.com/open/js/jweixin-1.0.0.js ，否则将无法在iOS9.0以上系统中成功使用JSSDK
## 第三步：在页面添加配置信息和js代码
``` javascript
wx.config({
            debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
            appId: 'wxb5f2540cff5*****', // 必填，公众号的唯一标识
            timestamp:'1414587457' , // 必填，生成签名的时间戳
            nonceStr: 'Wm3WZYTPz0wzccnW', // 必填，生成签名的随机串
            signature: '0f9de62fce790f9a083d5c99e95740ceb90c27ed',// 必填，签名
            jsApiList: ['onMenuShareAppMessage'] // 必填，需要使用的JS接口列表
        });
        wx.ready(function(){
            wx.onMenuShareAppMessage({
                title: '测试标题', // 分享标题
                desc: '测试描述', // 分享描述
                link: 'http://zicp.zicp.net/ycdh_real/mobile/productInfo?id=1e72e158-f3f5-46df-8385-7fe1059e142f', // 分享链接
                imgUrl: 'http://sandbox.runjs.cn/uploads/rs/438/v2eacmoa/2.png', // 分享图标
                type: 'link', // 分享类型,music、video或link，不填默认为link
                dataUrl: '', // 如果type是music或video，则要提供数据链接，默认为空
                success: function () {
                    alert("分享成功！");
                },
                cancel: function () {
                    // 用户取消分享后执行的回调函数
                }
            });
            wx.error(function(res){

                // config信息验证失败会执行error函数，如签名过期导致验证失败

            });
        });
```
这里重点说一下配置参数中的signature(签名)
获取签名的步骤：
1. 首先通过公众号的AppID(应用ID)和AppSecret(应用密钥)得到access_token，具体方法 [获取access_token方法](http://mp.weixin.qq.com/wiki/11/0e4b294685f817b95cbed85ba5e82b8f.html)
1. 通过上一步得到的access_token得到api_ticket，具体方法：
调用接口https://api.weixin.qq.com/cgi-bin/ticket/getticket?access_token=ACCESS_TOKEN&type=jsapi
返回json格式：
``` javascript
{
	"errcode":0,
	"errmsg":"ok",
	"ticket":"sM4AOVdWfPE4DxkXGEs8VMCPGGVi4C3VM0P37wVUCFvkVAy_90u5h9nbSlYy3-Sl-HhTdfl2fzFy1AOcHKP7qg",
	"expires_in":7200
}
```
1. 通过前两步的到的jsapi_ticket获取签名signature
* noncestr=Wm3WZYTPz0wzccnW		// 可以自定义
* jsapi_ticket=sM4AOVdWfPE4DxkXGEs8VMCPGGVi4C3VM0P37wVUCFvkVAy_90u5h9nbSlYy3-Sl-HhTdfl2fzFy1AOcHKP7qg
* timestamp=1414587457 	// 时间戳
* url=http://mp.weixin.qq.com?params=value
	+ 对所有待签名参数按照字段名的ASCII 码从小到大排序（字典序）后，使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串string1：
　　string1=jsapi_ticket=sM4AOVdWfPE4DxkXGEs8VMCPGGVi4C3VM0P37wVUCFvkVAy_90u5h9nbSlYy3-Sl-HhTdfl2fzFy1AOcHKP7qg&noncestr=Wm3WZYTPz0wzccnW&timestamp=1414587457&url=http://mp.weixin.qq.com?params=value
	+ 对string1进行sha1签名，得到signature：
	signature=sha1(string1);
　　经过上述算法得出 signature=0f9de62fce790f9a083d5c99e95740ceb90c27ed

注意事项：
> 签名用的noncestr和timestamp必须与wx.config中的nonceStr和timestamp相同。
> 签名用的url必须是调用JS接口页面的完整URL。
> `出于安全考虑，开发者必须在服务器端实现签名的逻辑。`

微信官方推出了 JS 接口签名校验工具 [地址](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=jsapisign)

到这为止微信分享就完成了，上述只是分享给好友，分享到朋友圈和这个类似，结合SDK官方文档照着写就可以了，分享效果出来了，看下图
![微信分享](/images/blogImg/weixin1227_4.png)

---
微信JS-SDK文档：http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html




