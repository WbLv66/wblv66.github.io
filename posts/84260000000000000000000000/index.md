# 升级Cmake


&lt;!--more--&gt;
&lt;!-- *   [升级CMake](#升级cmake)
    *   [1. 安装](#1-安装)
    *   [2. 替换](#2-替换) --&gt;
{{&lt; figure src=&#34;picture/4.jpg&#34;&gt;}}
## 升级CMake

### 1. 安装

安装依赖

    sudo apt install libssl-dev

去&lt;https://cmake.org/files/&gt;下载所需版本的源码。也可以使用wget下载，例如：

    wget https://cmake.org/files/v3.28/cmake-3.28.5.tar.gz

    tar -xvzf cmake-3.28.5.tar.gz

进入目录配置

    cd cmake-3.28.5
    chmod 777 ./configure
    ./configure
    make -j8
    sudo make install

### 2. 替换

最后使用新安装的cmake替换旧版本，其中/usr/local/bin/cmake为新安装的cmake目录

    sudo update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force



---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/84260000000000000000000000/  

