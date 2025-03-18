# 终端美化


&lt;!--more--&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2022/12/30/15/04/anime-7687171_1280.jpg&#34;&gt;}}
# 终端美化

## 1. zsh

### 1.1 安装zsh
```
sudo apt-get update
sudo apt-get install zsh

#设为默认
chsh -s $(which zsh) 

```
不要关闭终端
### 1.2 安装oh-my-zsh
1、curl/wget下载
```
sh -c &#34;$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)&#34;
```
2、手动下载
```
git clone git@github.com:ohmyzsh/ohmyzsh.git

 cd ohmyzsh/tools/

 ./install.sh
```
### 1.3 修改主题

```
vim ~/.zshrc
```
找到ZSH_THEME=“”，这句话，在双引号里面写上 crunch就可以啦

### 1.4 修改远程仓库地址

HTTPS访问GitHub经常受到网络限制或防火墙的影响，改用SSH是一个更稳定的选择

打开配置文件：

```
vim ~/.oh-my-zsh/.git/config
```

将仓库 URL 从 HTTPS 改为 SSH 格式：

```
remote &#34;origin&#34;]  
    url = git@github.com:ohmyzsh/ohmyzsh.git  
    fetch = &#43;refs/heads/*:refs/remotes/origin/*
```

### 1.5 设置插件

- zsh-autosuggestions：历史补全

下载安装
```
git clone git@github.com:zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
vim ~/.zshrc进去配置zsh-autosuggestions
```
plugins=(
   git
   # other plugins...
   zsh-autosuggestions
   )
```

### 1.6 终端美化

打开JSON设置，定位到Defaults里添加：
```
使用亚克力效果：

&#34;useAcrylic&#34;: true,

&#34;opacity&#34;: 80

设置背景：
&#34;backgroundImage&#34;: &#34;C:/Users/lwb/Desktop/picture/yourname.jpg&#34;,
&#34;backgroundImageOpacity&#34;: 0.4
```

## 2. oh my posh
安装参考官方文档
{{&lt; link &#34;https://ohmyposh.dev/docs/installation/linux&#34;&gt;}}

设置主题
```
vim ~/.zshrc
```
添加如下语句
```
export PATH=&#34;$HOME/.local/bin:$PATH&#34;

# 想使用windows系统上的主题可以加入
eval &#34;$(oh-my-posh --init --shell zsh --config  /mnt/c/Users/lwb/AppData/Local/Programs/oh-my-posh/themes/M365Princess.json)&#34;

# 想使用本系统上的主题可以加入
eval &#34;$(oh-my-posh --init --shell zsh --config  /home/lwb/.cache/oh-my-posh/themes/M365Princess.json)&#34;
```
home目录下conda版本不生效：在主题文件中将python segment的&#34;home_enabled&#34;设置为true
```
{
	&#34;type&#34;: &#34;python&#34;,
	...
	&#34;properties&#34;: {
		&#34;home_enabled&#34;: true,
    ...
	},
	...
},

```


## 3. git bash

删除键窗口会闪烁:新建一个~/.inputrc 文件，输入set bell-style none，保存；

---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/17f286e/  

