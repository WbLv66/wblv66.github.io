# Git


&lt;!--more--&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2024/02/18/13/13/ai-generated-8581182_1280.jpg&#34;&gt;}}
# git

## 1. ssh配置

创建本地密钥

    cd ~/.ssh
    ssh-keygen -t rsa -C &#34;你的邮箱1@xxx.com&#34;

在`~/.ssh`添加文件config

    touch config
    vim config
    # 在里面添加
    Host github.com
    	User git
    	IdentityFile ~/.ssh/mykey   # 这里mykey换成你命名的私钥名称

## 2. 添加SSH key到github
拷贝 id_rsa.pub 文件的内容
```
vim ~/.ssh/id_rsa.pub
```
登录github账号，从右上角的设置进入，然后点击菜单栏的 SSH key 进入页面添加 SSH key

---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/539f164/  

