
# IP-guard加密软件的攻防之路


# IP-guard加密系统评价
IP-guard系统整体而言仅适合文职类电脑加密,一旦对于IT类开发系统进行加密,则更多问题频出. 由于需要授权机制,基本每个新的exe文件要想读取文档类文件,均会受到加密系统的干扰. 
- 开发人员自己编译个exe都用不了,还得网管授权才能使用,严重影响各种软件的正常使用,极大的降低了工作效率
- 加密系统需要对电脑文件进行遍历加密,严重消耗电脑系统
- IP-guard能够后台实时监控电脑所有的使用情况.Boss is Watching U. 

这些设定对于开发人员而言都是无法忍受.俗话说：魔高一尺,道高一丈.都是开发人员,既然改变不了公司制度,那么就改变自己吧



# 加密攻防理论基础
IP-guard 其实由两个模块组成. 加密系统和解密系统
- 加密系统：
> 加密系统将会自动遍历电脑所有文档类文件,并且对其存储的数据进行可逆的加密. 所以存储在文件的里面的数据实际上已经被改写过. 由于加密本身是具备主动遍历加密的特性,一旦产生新的文件,加密模块均会主动尝试对其进行加密工作,这一过程将严重拖累电脑性能

- 解密系统：
> 解密系统的机制,笔者估计其技术机制是是由解密钩子来完成. 原本简单的**文件-应用程序**的流程,变成了 **文件->解密模块->应用程序**的流程.解密模块使用钩子,拦截系统中所有读取文件的请求,由解密模块代理去读取文件,将文件解密后再转发给应用程序.这一流程无疑同样将消耗电脑性能. 

## 总结
既然是分两个模块来工作,那么我们只需要干掉加密模块,然后让解密模块正常工作,IP-guard将老老实实变成我们需要的样子

### windows加密攻防流程
- 定位加密进程位置
- 导出加密模块数字证书
- 禁用加密模块数字证书
- 如需恢复加密模块,则直接恢复加密模块数字证书即可让加密模块死灰复燃.(期间需要重启)


#### 定位加密模块
> 加密模块需要向公司内部服务器上传数据,只需要捕捉到其网络连接,则可以将加密进程挖出来.任其藏的再深都无济于事
![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/1.1.png)

#### 导出程序应用证书
![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/2.1.png)

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/3.2.png)

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/4.1.png)



![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/5.1.png)

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/6.1.png)

#### 禁用数字证书
1. 步骤一：启动命令行工

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/7.1.jpg)

2. 步骤：定位到软件限制策略
 
![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/8.1.jpg)

3.步骤： 创建新的软件策略

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/8.2.jpg)

4. 步骤：

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/9.1.jpg)

5.步骤：

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/10.1.jpg)

6.步骤：

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/11.1.jpg)

7. 步骤：

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/12.1.jpg)

8.步骤：选择不允许,则加密模块将被禁用.重启电脑后,加密模块将无法运行. 如需恢复,则只需按照以上流程选择允许即可恢复加密模块正常运行

![image](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/13.1.jpg)

# 技术免责声明
本文仅作技术性研究.请酌情使用,由此引发的一系列后果请自行承担. 

# 攻防技术升级
> 此文仅是利用了IP-guard的一个漏洞来实现避免加密系统对电脑的干扰. 攻防之路需要持续升级更新.

[证书下载](https://github.com/lion117/FuckIPGuard_E/blob/master/pic/IP-guard%E8%AF%81%E4%B9%A6.cer)
[Github持续更新,欢迎贡献您的破解方案](https://github.com/lion117/FuckIPGuard_E)





