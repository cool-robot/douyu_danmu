# douyu_danmu
#斗鱼弹幕节奏大师
---
## 环境说明
> * 该版本是在windows环境下使用
> * python 2.7或2.X版本
> * 需要按照requests模块

---

## 简单使用说明
```python
> python douyu.py saro
  ...
  please input content($-exit):我要带节奏~~~~~~~
  please input content($-exit):我要带节奏~~~~~~~
  please input content($-exit):$
```
使用方式很简单，douyu.py后面可以输入主播的名称，也可以输入直播房间的ID号。然后输入你要输入的弹幕就行了。

---

## 原理以及修改说明
>**如何添加账号和密码。**

登陆到弹幕服务器所使用的账号和密码都是经过加密的，账号是后台加密，在你登陆之后由后台返回到cookie中，我们可以通过chrome调试器来看到cookie中，acf_username中的值就是加密后的账号信息（昵称登陆一般是以auto_开头）；password很简单，如果只是用来发送弹幕的话，就只需要对你的密码做一一个32位小写的md5加密，推荐一个[在线加密工具](http://tool.chinaz.com/tools/md5.aspx)。对应好顺序填写到users和passes中，realname写自己的明文账号。
```python
    realname=[]
    users=[]
    passes=[]
```

>**关于斗鱼弹幕系统的说明**
    1.最重要的一点，你登陆直播的账号不能同时再放在机器人账号中，不然你登陆之后你是看不到自己发送的弹幕的。（账号只能同时登陆一个地方）
    2.如果你长时间登陆之后没有发送弹幕，tcp可能会断开。解决方案是重启或者发送心跳包。经过逆向flash发现了心跳包每隔60秒发送一次，心跳包的构造在代码中也有，你们根据自己需要来决定是否要开个子进程来保活。
    3.后台弹幕长度限定在51个字符中
    4.我由于没有恶意过，也不知道能否绕过前端的禁言，如果有人被禁言后无法发送请告知。
 
 ----
 
>   PS. 求助有精通flascc逆向的大神
        或者有意愿破解斗鱼登陆系统（或者极验研制吗的），代码原理都看懂了，但是关键是图片和拉伸长度对应关系标注真的是个力气活。
    **最后.经过测试，在**14**个账号同时发送的情况下可以覆盖弹幕全屏，持续2秒。由于程序本身针对每个账号只有一个tcp连接，数据量很少，你就是登陆300个账号也不会出现卡顿，但是为了体验效果，希望大家不要恶意刷屏。小小的娱乐一下就行了**
