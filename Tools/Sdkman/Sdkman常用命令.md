- 查看可安装列表：`sdk list`
- 查看可安装的Java列表：`sdk list java`
- 安装最新版Java：`sdk install java`
- 安装指定版本Java：`sdk install java 18.0.1`
- 安装本地版本Java：`sdk install java 10-zulu /Library/Java/JavaVirtualMachines/zulu-10.jdk/Contents/Home`
- 卸载已安装的Java18：`sdk uninstall java 18.0.1`
- 升级sdkman：`sdk selfupdate`
- 强制升级sdkman：`sdk selfupdate force`
- 升级Java：`sdk upgrade java`
- 升级所有已安装软件：`sdk upgrade`
- 


- 在特定项目使用特定版本Java
	1. 进入项目根目录：`cd project_root_dir`
	2. 执行命令`sdk env init`创建`.sdkmanrc`配置文件
		1. 查看该文件`cat .sdkmanrc`
		2. 将其中的版本改为你想要的即可

```bash
# Enable auto-env through the sdkman_auto_env config
# Add key=value pairs of SDKs to use below
java=11.0.17-amzn
```

