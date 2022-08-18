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

![1650852477454](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650852477454.png)

![1650852452286](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650852452286.png)



打包后的就是类似于这样，类似虚拟机的快照

![1650852724189](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650852724189.png)









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

- 镜像分层的理解  如果加一层是之前那层的更新 会进行替换     拉取镜像的时候 已经存在的就不会再拉了![1650850692165](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650850692165.png)

- 镜像都是只读的  当我们镜像启动容器的时候  会有个新的可写层加到镜像层的顶部，这一层我们可以进行操作 这层通常来说叫做容器层  我们所有的操作都是基于容器层的  我做的修改什么的会保存在容器层

- docker -p 可以设置要映射的端口和容器端口  一个端口上只能绑定一个容器

- 卷技术，就是容器目录的挂载，容器间的数据共享机制    目的就是容器的持久化和同步操作、容器间数据共享

  映射过后  对容器内部的文件进行操作 会自动同步到外部 对外部进行操作 会自动同步到容器内部（就算是容器停止运行了  也会同步）  **好处：我们以后修改直接在本地修改即可，容器内部会自动同步**

- ==卷技术的使用 **指令**==

  ![1650853968342](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650853968342.png)

  ![1650861186878](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650861186878.png)

  ![1650862630616](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650862630616.png)

  ![1650863101402](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650863101402.png)

  `也可以使用dockerfile进行挂载`![1650863902597](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650863902597.png)

  `容器间的挂载:--volumes-from ` 拷贝的概念

  当两个挂载一到一个上面的时候  相当于全部都挂载上了  就算把挂载的那个对象删了  其他两个照样同步

  ![1650867175134](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650867175134.png)

  

- 当我拉取mysql镜像的时候，拉了mysql8版本太高 读取需要些插件  换成5.7就可以了 

- docker启动mysql需要做的

  ![1650860312511](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650860312511.png)

- 有些镜像启动需要配置环境  -e   需要去docker hub上看帮助文档进行测试

- 就算在本地把对应的容器删了   但你容器中挂载出来的文件还是会存在 数据并不会丢失

- 图床指的是存储图片的服务器

- 如果要查看docker挂载的对应目录在哪  用docker inspect 容器id  查看具体信息  在mounts看到挂载的信息 可以找到对应的目录

- 通过dockerfile 挂载卷  如果容器内没有对应的文件夹 也会自动生成  如果没有挂载卷 那么之后就要以手动的方式 -v挂载卷

- ==**DockFile指令**==

  ![1650868496106](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650868496106.png)

  ![1650868508792](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650868508792.png)

  

  

  

  

  

  

- 例子什么的 在最全笔记中看

- yum -y中 -y的意思就是代替手动输入yes

- $符号在Linux的shell中使用 作用就是获取一个变量的值

- docker build -f 指定要使用dockerfile的路径

- docker build -f zytdockfile-centos -t mycentos:0.1 ==.==  这个点的意思就是目的地址为当前地址 构建这个镜像在这个目的地址    

- CMD ENTRYPOINT的区别
  ![1650871228569](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650871228569.png)
  ![1650872614684](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650872614684.png)

  在CMD命令下 如果运行时追加参数  会将CMD的命令进行替换   比如说 CMD里是 ls -a  我们在外面写个-l  会报错  除非我们些的是 ls -al 就不报错  因为会被替换

  

- 实战Tomcat这是精髓一定要好好看，之后自己有机会发布镜像的时候  模仿这个进行构建

- 构建dockerfile采用官方命名`Dockerfile`这样build的时候 都不需要指定-f了 会自动去寻找  直接 

  ```shell
  docker build -t "name" #即可 会自动去寻找Dockerfile
  ```

  

- WORKDIR 是进去的第一个落脚点      ENV 就是设置环境变量

- ![1650874256508](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650874256508.png)
  `设置PATH变量是为了让操作系统找到指定的工具程序，那么设置CLASSPATH变量的目的就是让执行环境找到程序对应的class文件以及程序中引用的其他class文件`

- javaweb生成项目后默认的其实页是index.jsp和index.html

- tomcat是热部署的

- 自己push的镜像一定要带版本号     使用 docker tag 给镜像附上版本也可以一开始取名的时候就附上   前面一定是要自己`docker hub的用户名`/镜像名：版本号！

- 除了推送到docker hub还有推送到阿里云上，阿里云推送有固定的方法

- ![1650935337032](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650935337032.png)

- `Docker 网络`

- 容器和容器之间是可以互相ping通的

- 容器和容器之间联通实际上是通过路由器相接    删掉对应的容器 网卡就会消失![1650939538442](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650939538442.png)
  ![1650939727074](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650939727074.png)

- ![1650939832717](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650939832717.png)

- 通过服务名直接ping通  不用ip地址  这样有助于当我们对应的服务器ip地址进行更换 不用重启 修改

- “hosts文件是一个用于储存计算机网络中各节点信息的计算机文件；作用是将一些常用的网址域名与其对应的IP地址建立一个关联“数据库”，当用户在浏览器中输入一个需要登录的网址时，系统会首先自动从Hosts文件中寻找对应的IP地址。”  所以很多代理映射都放到这里面   `docker中--link的操作就是在hosts配置中加了一个映射`  目前已经不建议使用--link了  而是使用自定义网络 不适用docker0  因为docker0不支持服务名访问

- **网络模式**

  - bridge  :  桥接 docker(默认，自己创建也使用桥接模式)
  - none    :  不配置网络
  - host     :   和宿主机共享网络
  - container :   容器网络连同！(用的少！局限大)

- ![1650941422023](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650941422023.png)![1650941385208](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650941385208.png)
  直接启动 它会默认连接docker0   我们想用自己网络的话  可以创建一个网络  按照上面的方法启动

  - docker0特点：默认，域名不能访问  能通过--link打通连接   有局限性
  - 所以我们可以自定义网络

- 
  ![1650941832117](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650941832117.png)
  自定义网络可以直接ping 名字

- **网络联通   在不同网段中的容器是无法联通的**

  ![1650946676275](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1650946676275.png)

  联通了之后可以在对应的network inspect中看到    这就是一个容器 多个ip地址

  `假如要跨网络操作别人，就需要使用 docker network connect联通`

- 创建集群  看狂神笔记  玩玩看

- 网关是实现不同网络之间的通信  像仅仅是搭建redis集群 可以不设置网关



