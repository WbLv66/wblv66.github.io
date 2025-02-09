# Git


&lt;!--more--&gt;
{{&lt; figure src=&#34;picture/7.jpg&#34;&gt;}}
# git

## 1. ssh配置

创建本地密钥

    cd ~/.ssh
    ssh-keygen -t rsa -b 4096

在`~/.ssh`添加文件config

    touch config
    vim config
    # 在里面添加
    Host github.com
    	User git
    	IdentityFile ~/.ssh/mykey   # 这里mykey换成你命名的私钥名称



---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/539f164/  

