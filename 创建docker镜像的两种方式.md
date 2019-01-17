 <h3>方式一: 使用docker commit创建镜像</h3>> </br>
1. <b>先将本地容器提交为镜</b>
    `docker commit  [OPTIONS] [REPOSITORY:[TAG]]`<br>
	`OPTION` 包括 </br>-a  --author 作者名称,  -m --message 描述信息</br>
	`REPOSITORY` 容器的名称 ps:名称必须是已存在的容器 , `TAG` 为标签 可以理解为版本号 <br>
2. <b>将本地镜像提交到镜像仓库(这里用阿里云仓库来举例)</b>
	`registry.cn-hangzhou.aliyuncs.com/commit_test/commit_test` 为阿里云的传输地址 <br>
 
- <font color="Indigo">第一步 登录阿里云镜像仓库</font> `docker login --username=279951088@qq.com registry.cn-hangzhou.aliyuncs.com`<br> 
<font color="silver">username是登录阿里云时的fullname 后面的地址是你仓库的地域名 如果不确定可以点击<a href="https://cr.console.aliyun.com/repository/cn-hangzhou/commit_test/commit_test/detail">这里</a>登录后查看 <br></font>
- <font color="Indigo">第二步 为镜像创建标签</font> `$ sudo docker tag [ImageId] registry.cn-hangzhou.aliyuncs.com/commit_test/commit_test:[镜像版本号]`
- <font color="Indigo">第三步 push刚刚打过标签的镜像 上传到仓库</font>
	` $ sudo docker push registry.cn-hangzhou.aliyuncs.com/commit_test/commit_test:[镜像版本号]`
<br><h3><b>方式二: 使用docker commit创建镜像</b>> </h3>
<b>第一步> 在宿主机上创建存放DockerFile文件的目录</b><br>
<b>第二步> 编写Docker文件 如下: </b><br>

    	# 注释
	    FROM centos
	    MAINTAINER scott "coldfishzz@163.com"
	    RUN yum install -y wget
	    RUN wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
	    RUN yum install -y epel-release
	    RUN yum install -y nginx
	    EXPOSE 80
 每个代码的含义:

-  `FORM` 用哪个本地镜像作为基础镜像 
-  `MAINTAINER` 作者的名字和联系方式
-  `RUN` 要执行的命令 (lunix命令)
-  `EXPOSE` 指定端口 

<b>第二步> 编译Dockerfile文件</b><br>
`docker build -t='IMAGE_NAME'  ./dockerfileDictionary`

- -t后为编译后的镜像名字
-  最后跟的是Dockerfile文件所在的<font color="red" size="6">文件夹的路径.</font>