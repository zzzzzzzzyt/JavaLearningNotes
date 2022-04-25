# 心得体会

**==并不是笔记，而是针对自己需要记忆的东西，留下痕迹。一定要学会 好好用==**



- docker所解决的问题如下![1650710800911](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650710800911.png)

- docker火的原因是十分的轻巧    docker是容器化技术

- docker是基于go语言开发的

- [Docker Documentation | Docker Documentation](https://docs.docker.com/)  docker的文档非常详细
  [Docker Hub](https://hub.docker.com/) docker的仓库地址
  
- Docker如果是安在阿里云服务器上的话  还可以配置镜像加速

- Docker Run的原理示意图![1650761222173](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650761222173.png)

- 启动Docker指令 systemctl start docker     运行Docker指令 docker run XXX

- 底层原理![1650761599658](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650761599658.png)

- **==Docker常用的命令（其余不多记 直接看笔记）==**
  ![1650762106989](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650762106989.png)
  ![1650763449482](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650763449482.png)![1650763706514](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650763706514.png)![1650764125304](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650764125304.png)![1650764160903](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650764160903.png)

  ![1650764826238](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650764826238.png)

  ![1650765225083](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650765225083.png)

  ![1650765543807](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650765543807.png)![1650766287438](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650766287438.png)

![1650766233160](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650766233160.png)

![1650766601382](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650766601382.png)

![1650766891690](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650766891690.png)

![1650785841816](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650785841816.png)

![1650785939799](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650785939799.png)![1650785976455](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650785976455.png)

![1650786128934](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650786128934.png)

![1650786495145](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650786495145.png)

![1650786729761](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650786729761.png)

![1650786773454](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650786773454.png)

![1650787381577](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650787381577.png)

![1650787408191](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650787408191.png)



![1650787553171](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650787553171.png)



- docker images -q显示镜像id    dockers images -aq 显示所有镜像id 有些隐藏的镜像也可以显示

- Docker下载镜像采用的是分层下载  如果你下载一个镜像 他一些层级已经被下载过了  他就可以共用而不用下载了

- markdown的使用小技巧  ```+编程语言会创建代码段

- docker run -d XXX  默认是执行/bin/bash这个命令在后台启动成功后执行了就直接关闭了，如果要持久化的话  要指定一个持久的命令

- touch用来新建文件 mkdir用来新建文件夹  rm用来删除文件 

- 当下载一个新的镜像时  可以去dockerHub上查看关注文档

- Linux命令 whereis
  -b 　只查找二进制文件。

  -B<目录> 　只在设置的目录下查找二进制文件。

  -f 　不显示文件名前的路径名称。

  -m 　只查找说明文件。

  -M<目录> 　只在设置的目录下查找说明文件。

  -s 　只查找原始代码文件。

  -S<目录> 　只在设置的目录下查找原始代码文件。

  -u 　查找不包含指定类型的文件。

- 用完后会自动移除 而不是还存在![1650794874103](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650794874103.png)

- 像这些镜像其实很大程度都是被阉割过的 保证最小运行就行  就比如说tomcat webapp里没东西  其实在webapp.dist中有  把它复制过来就行了