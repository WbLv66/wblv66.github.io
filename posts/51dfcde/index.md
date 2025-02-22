# Tmux


&lt;!--more--&gt;
{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2022/10/19/14/53/sunset-7532726_1280.jpg&#34;&gt;}}

# Tmux

## 1. 安装

```bash
git clone git@github.com:tmux/tmux.git
cd tmux
sh autogen.sh
./configure &amp;&amp; make
```

## 2. 配置

再配合zsh使用时会出现提示代码为白色的现象，需要修改~/目录下的.tmux.conf

```bash
set -g default-terminal &#34;tmux-256color&#34;
```

为了让tmux支持鼠标操作，需要继续加入内容

```bash
set-option -g mouse on
```

## 3. 使用

tmux的使用可参考：

{{&lt; link &#34;https://www.cnblogs.com/zhiminyu/p/17457933.html&#34; &#34;burlingame Blog&#34; &#34;burlingame Blog&#34; true &#34;https://www.yuduo.cn/oss/yuduo/2024/1208/6686ad50b87c4d9cb750d5510e3f3a9c?x-oss-process=style/yuduo-app-logo&#34; &gt;}}

---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/51dfcde/  

