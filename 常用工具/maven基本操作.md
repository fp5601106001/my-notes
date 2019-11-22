# maven基本操作

### 安装jar到maven本地库

* 安装maven中央仓库中没有的包
* 安装自定义包

> mvn install:install-file -Dfile=c:\kaptcha-version.jar -DgroupId=com.google.code -DartifactId=kaptcha -Dversion={version} -Dpackaging=jar