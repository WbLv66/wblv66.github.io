# Git


&lt;!--more--&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2024/02/18/13/13/ai-generated-8581182_1280.jpg&#34;&gt;}}
# git

## 1. ssh配置

创建本地密钥

    ssh-keygen -t rsa -b 4096 -C &#34;你的邮箱@xxx.com&#34; -f /home/用户名/.ssh/你的名字_rsa

在`~/.ssh`添加文件config

    touch ~/.ssh/config
    vim ~/.ssh/config
    # 在里面添加
    Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_me
    # 这里mykey换成你命名的私钥名称

      

## 2. 添加SSH key到github
拷贝 id_rsa.pub 文件的内容
```
vim ~/.ssh/id_rsa.pub
```
登录github账号，从右上角的设置进入，然后点击菜单栏的 SSH key 进入页面添加 SSH key


## 3. 设置git信息
```
git config --global user.name &#39;你的名字&#39; 
git config --global user.email &#39;你的邮箱&#39;
```

``git config --list``可以查看信息

---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/539f164/  

