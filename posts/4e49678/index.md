# 升级GCC


&lt;!--more--&gt;
&lt;!-- - [升级gcc/g&#43;&#43;](#升级gccg)
  - [1. 查看版本](#1-查看版本)
  - [2. 下载指定版本](#2-下载指定版本)
  - [3. 设置软链接](#3-设置软链接)
  - [4. 更新系统libstdc&#43;&#43;版本](#4-更新系统libstdc版本) --&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2022/12/24/11/42/home-7675773_1280.jpg&#34;&gt;}}
# 升级gcc/g&#43;&#43;
## 1. 查看版本
`` gcc -v ``
`` g&#43;&#43; -v ``
## 2. 下载指定版本
进入清华源下载相应版本
``` 
https://mirror.tuna.tsinghua.edu.cn/gnu/gcc

wget https://mirror.tuna.tsinghua.edu.cn/gnu/gcc/gcc-14.1.0/gcc-14.1.0.tar.gz
```
解压文件进入目录,我下载的是gcc-14.1.0,版本因人而异
`` tar -xf gcc-14.1.0.tar.gz cd gcc-14.1.0 ``
下载依赖包
``./contrib/download_prerequisites``
创建一个用于编译GCC的目录：
``mkdir build &amp;&amp; cd build``
配置编译选项：
```
../configure --prefix=/opt/gcc-14.1.0 --enable-languages=c,c&#43;&#43; --disable-multilib
```
开始编译
``make -j8``
最后，安装GCC：
``sudo make install``
&lt;!-- ## 3. 设置环境变量(应该不需要)
永久加入到系统环境变量中
``gedit ~/.bashrc``
```
PATH=/opt/gcc-14.1.0/bin:$PATH
LD_LIBRARY_PATH=/opt/gcc-14.1.0/lib:$LD_LIBRARY_PATH
LD_LIBRARY_PATH=/opt/gcc-14.1.0/lib64:$LD_LIBRARY_PATH
LD_LIBRARY_PATH=/opt/gcc-14.1.0/libxec:$LD_LIBRARY_PATH
LD_LIBRARY_PATH=/opt/gcc-14.1.0/include:$INCLUDE
```
``source ~/.bashrc`` --&gt;
## 3. 设置软链接
查看系统gcc/g&#43;&#43;版本
```
locate g&#43;&#43;|grep /usr/bin/
locate gcc|grep /usr/bin/ 
```
设置软链接的优先级
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 10
sudo update-alternatives --install /usr/bin/g&#43;&#43; g&#43;&#43; /usr/bin/g&#43;&#43;-9 10

sudo update-alternatives --install /usr/bin/gcc gcc /opt/gcc-14.1.0/bin/gcc 20
sudo update-alternatives --install /usr/bin/g&#43;&#43; g&#43;&#43; /opt/gcc-14.1.0/bin/g&#43;&#43; 20
```
手动切换gcc与g&#43;&#43;版本
```
sudo update-alternatives --config gcc
sudo update-alternatives --config g&#43;&#43;
```
## 4. 更新系统libstdc&#43;&#43;版本
libstdc{?&#43;}&#43;是适应于g{?&#43;}&#43;的标准库,位于`/usr/lib/x86_64-linux-gnu/`下面
使用指令先看下系统目前都有哪些版本的
``
strings /usr/lib/x86_64-linux-gnu/libstdc&#43;&#43;.so.6 | grep GLIBCXX
``
寻找安装高版本gcc目录下的libstdc{?&#43;}&#43;.so.6
``sudo find / -name &#34;libstdc&#43;&#43;.so.6*&#34;|grep /opt``
使用之前的指令看看其是否包含需要的版本
``strings /opt/gcc-14.1.0/lib64/libstdc&#43;&#43;.so.6.0.33 | grep GLIBCXX``
将文件复制到指定目录并建立新的链接
```
# 复制
sudo cp /opt/gcc-14.1.0/lib64/libstdc&#43;&#43;.so.6.0.33 /usr/lib/x86_64-linux-gnu/
# 删除之前链接
sudo rm /usr/lib/x86_64-linux-gnu/libstdc&#43;&#43;.so.6
# 创建新的链接
sudo ln -s /usr/lib/x86_64-linux-gnu/libstdc&#43;&#43;.so.6.0.33 /usr/lib/x86_64-linux-gnu/libstdc&#43;&#43;.so.6
```

---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/4e49678/  

