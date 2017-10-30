# maven-repo
My personal maven repository.

# Usage
pom.xml:
```
<repositories>
    <repository>
        <id>github-maven-repo</id>
        <url>https://raw.githubusercontent.com/lijinhuai/maven-repo/master/</url>
    </repository>
</repositories>
```

# 利用github搭建个人maven仓库
简单来说，共有三步：
1. deploy到本地目录
2. 把本地目录提交到gtihub上
3. 配置github地址为仓库地址

## 配置local file maven仓库
### deploy到本地 
maven可以通过http, ftp, ssh等deploy到远程服务器，也可以deploy到本地文件系统里。例如：
```
<distributionManagement>
    <repository>
        <id>github-mvn-repo</id>
        <url>file:/Users/user/WorkSpaces/maven_repo/repository/</url>
    </repository>
</distributionManagement>
```
### 通过命令行则是：
```
mvn deploy -DaltDeploymentRepository=github-mvn-repo::default::file:/Users/user/WorkSpaces/maven_repo/repository/
```
**推荐使用命令行来deploy，避免在项目里显式配置。**

[https://maven.apache.org/plugins/maven-deploy-plugin/](https://maven.apache.org/plugins/maven-deploy-plugin/)

[https://maven.apache.org/plugins/maven-deploy-plugin/](https://maven.apache.org/plugins/maven-deploy-plugin/)

## 把本地仓库提交到github上
上面把项目发布到本地目录/Users/user/WorkSpaces/maven_repo/repository/里，下面把这个目录提交到github上。

在Github上新建一个项目，然后把/Users/user/WorkSpaces/maven_repo/repository/下的文件都提交到gtihub上。
```
cd /Users/user/WorkSpaces/maven_repo/
git init
git add repository/*
git commit -m 'deploy xxx'
git remote add origin git@github.com:lijinhuai/maven-repo.git
git push origin master
```

## github maven仓库的使用
因为github使用了raw.githubusercontent.com这个域名用于raw文件下载。所以使用这个maven仓库，只要在pom.xml里增加
```
<repositories>
    <repository>
        <id>github-maven-repo</id>
        <url>https://raw.githubusercontent.com/lijinhuai/maven-repo/master/repository</url>
    </repository>
</repositories>
```
## 配置使用本地仓库
```
<repositories>
    <repository>
        <id>github-maven-repo</id>
        <url>file:/Users/user/WorkSpaces/maven_repo/repository/</url>
    </repository>
</repositories>
```
