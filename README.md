# cordova-cordova-hot-code-push-plugin

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


