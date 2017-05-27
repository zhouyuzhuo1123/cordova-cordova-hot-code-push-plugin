# cordova-cordova-hot-code-push-plugin

### 第一步
>在已有项目目录下添加插件 cordova plugin add cordova-hot-code-push-plugin 
### 第二步
>全局安装npm install -g cordova-hot-code-push-cli(前提是node环境已经配置好)，安装完成后执行cordova-hcp server查看是否正常。如果运行报错则有可能是因为端口占用。
### 第三步
>在服务器可访问路径下创建一个目录，比如：hotcode (我这里用的是express)
### 第四步
>在项目的根目录下新建一个cordova-hcp.json的文件添加以下内容：

---

```
{
"autogenerated": true,
"release": "2016.11.08-15.13.26",
"content_url": "你的服务器访问路径/hotcode",
"update": "now"
}

```



