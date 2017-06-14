# cordova/cordova-hot-code-push-plugin

### 第一步
>在已有项目目录下添加插件 cordova plugin add cordova-hot-code-push-plugin 
### 第二步
>全局安装npm install -g cordova-hot-code-push-cli(前提是node环境已经配置好)，安装完成后执行cordova-hcp server查看是否正常。如果运行报错则有可能是因为端口占用。
### 第三步
>在服务器可访问路径下创建一个目录，比如：hotcode (我这里用的是express)
### 第四步
>在项目的根目录下新建一个cordova-hcp.json的文件添加以下内容：
```
{
  "autogenerated": true,
  "release": "2016.11.08-15.13.26",
  "content_url": "你的服务器访问路径/hotcode",
  "update": "now"
}

```
### 第五步： 
>在项目路径下运行cordova-hcp build，运行后会在www目录下生成chcp.json和chcp.manifest文件
### 第六步： 
>将项目中的www目录下所有文件上传到服务器刚才新建的目录hotcode下面 
### 第七步： 
>将以下代码加入项目的config.xml中，然后运行cordova build Android
```
<chcp>
  <config-file url=" 你的服务器访问路径/hotcode/chcp.json"/>
</chcp>
```
### 第八步： 
>修改www目录下的内容，例如：修改index.html中的代码，然后运行cordova-hcp build.再将index.html和chcp.json和chcp.manifest一起上传到服务器对应的位置。重新打开app将会看见更新的内容。

---
## 之前基本是在客户端打开后自动请求后台自动更新，如果想要客户端提示更新...
### 第九步
>将第七步中加入的代码 进行修改如下:
```
<chcp>
    <auto-download enabled="false" />
    <auto-install enabled="false" />
    <config-file url=" 你的服务器访问路径/hotcode/chcp.json"/>
</chcp>

```
>js中的代码就可以这样写
```
//备注：这里的使用了Framework7
chcp.fetchUpdate(function(error, data) {
    if(!error) {
        myApp.modal({
            title: "提示",
            text: "有更新，确定更新吗?",
            buttons: [{
                text: '不更新'
            }, {
                text: "立即更新",
                onClick: function() {
                    myApp.showPreloader('正在升级，升级完毕应用将自动重启...');
                    chcp.installUpdate(function(error) {
                        myApp.alert("更新完成", ["提示"]);
                    })
                }
            }]
        })
    } else {
        myApp.alert("你当前是最新版本", ["提示"]);
    }
})
   ```
# 编写可维护的Javascript代码

- [欢迎来提issue进行改进](https://github.com/Kelichao/work.expressive)

- [参考《编写可维护的JavaScript》](http://baike.baidu.com/link?url=zn9j-dvLCZyZ-BsCdBr5kO674AagHo4iMdq6zR1KDvxnDCV4VzlDZ_IBnMeg7fhOutujqk_zomnsWG-sFcfrZjwyVb-T8BfsDLFUAB99w72UdOEaIbcLMkA9_JnoF_ghH0ZxSQmn_vG_-POH2THmxWWkkTgeev2Yb0x6euwyNvK)

- [wiki前端框架的基本的架构方案]( http://wiki.evun.cn/pages/viewpage.action?pageId=3933068)

> 代码风格根据团队内部成员总结所得，大家有好的意见或建议可以一起来进行定制O(∩_∩)O


# PDA 打包与热更新-发布流程
### 一 打包环境
1. cordova 全局安装
2. 生成安卓平台：

   ```
   cordova platform add android

   ```
3. 安装plugin cordova-hot-code-push-plugin：

   ```
   cordova plugin add cordova-hot-code-push-plugin

   ```
4. 全局安装 cordova-hot-code-push-cl:

   ```
   npm install -g cordova-hot-code-push-cli

   ```

### 二 打包流程
1. 将需要打包的文件防止www目录下。
2. 执行命令：

   ```
   cordova-hcp build //www文件夹下生成两个热更新所需文件

   ```
3. 执行打包命令：

   ```
   cordova build //生成安卓平台apk 

   ```
   > apk生成目录:"platforms\android\build\outputs\apk"
   
### 三 热更新
1. 将所更新文件放置www文件夹下，执行打包流程中的等2步。最后将www文件夹下所需更新文件以及生成的两个热更新文件放置服务器相应位置即可。详见[cordova-hotupdata](https://github.com/zhouyuzhuo1123/cordova-cordova-hot-code-push-plugin)
