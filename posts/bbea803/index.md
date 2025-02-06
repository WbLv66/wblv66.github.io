# Zsh


&lt;!--more--&gt;
{{&lt; figure src=&#34;picture/2.jpg&#34;&gt;}}
## 配置zsh
### 1. 安装zsh
```
sudo apt-get update
sudo apt-get install zsh

#设为默认
chsh -s $(which zsh) 

```
不要关闭终端
### 2. 安装oh-my-zsh

```
sh -c &#34;$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)&#34; 

```
### 3. 修改主题

```
vim ~/.zshrc
```
找到ZSH_THEME=“”，这句话，在双引号里面写上 crunch就可以啦

### 4. 设置插件

- zsh-autosuggestions：历史补全

下载安装
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
vim ~/.zshrc进去配置zsh-autosuggestions
```
plugins=(
   git
   # other plugins...
   zsh-autosuggestions
```

### 5. 终端美化

打开JSON设置，定位到Defaults里添加：
```
使用亚克力效果：

&#34;useAcrylic&#34;: true,

&#34;opacity&#34;: 80

设置背景：
&#34;backgroundImage&#34;: &#34;C:/Users/lwb/Desktop/picture/yourname.jpg&#34;,
&#34;backgroundImageOpacity&#34;: 0.4
```

---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/bbea803/  

