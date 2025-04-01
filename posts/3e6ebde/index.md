# 设置IP变化同步脚本


&lt;!--more--&gt;

# 设置IP变化同步脚本

## 1. 创建无密码密钥

生成无passphrase密钥的命令

```
ssh-keygen -t rsa -b 4096 -f ~/.ssh/rsa_no_pass -N &#34;&#34;
```

在`~/.ssh`添加文件config
```
    touch ~/.ssh/config
    vim ~/.ssh/config
    # 在里面添加
    Host gitee.com
    HostName gitee.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/rsa_no_pass
```


## 2. 将本地git与gitee建立联系

将本地无密码公钥添加到gitee上

创建并切换到main分支

```
git switch -c main 
```

然后按照gitee提示的操作

## 3. 创建脚本

创建Bash脚本，该脚本每次检测IP是否变化，如果变化则更新仓库中的一个文件（例如 current_ip.txt），提交并推送到 gitee 的 main 分支

```
vim update_ip.sh
```

添加内容
```
#!/bin/bash
export GIT_SSH_COMMAND=&#34;ssh -i /home/lwb/.ssh/rsa_no_pass&#34;
# 定义仓库路径
REPO_DIR=&#34;/home/lwb/lwb_ws/A100IP&#34;
# 定义 IP 信息文件
IP_FILE=&#34;$REPO_DIR/current_ip.txt&#34;
# 定义日志文件
LOG_FILE=&#34;$REPO_DIR/update_ip.log&#34;

# 每 6 小时清空一次日志（当小时数可以被 6 整除时）
if [ $(( $(date &#39;&#43;%H&#39;) % 6 )) -eq 0 ]; then
    echo &#34;[$(date &#39;&#43;%Y-%m-%d %H:%M:%S&#39;)] 清空日志文件&#34; &gt; &#34;$LOG_FILE&#34;
fi

# 记录当前时间到日志
echo &#34;[$(date &#39;&#43;%Y-%m-%d %H:%M:%S&#39;)] 脚本开始执行&#34; &gt;&gt; &#34;$LOG_FILE&#34;

# 获取 ifconfig 命令的 IPv4 和 IPv6 地址
NEW_OUTPUT=$(ifconfig | grep -E &#34;inet |inet6 &#34;)

# 如果文件不存在，则认为第一次运行，直接写入并提交
if [ ! -f &#34;$IP_FILE&#34; ]; then
    echo &#34;$NEW_OUTPUT&#34; &gt; &#34;$IP_FILE&#34;
    cd &#34;$REPO_DIR&#34; || exit 1
    git add .
    git commit -m &#34;Initial commit: ifconfig output&#34; &gt;&gt; &#34;$LOG_FILE&#34; 2&gt;&amp;1
    git push origin main &gt;&gt; &#34;$LOG_FILE&#34; 2&gt;&amp;1
    echo &#34;[$(date &#39;&#43;%Y-%m-%d %H:%M:%S&#39;)] 初次保存 ifconfig 输出并推送到 Gitee&#34; &gt;&gt; &#34;$LOG_FILE&#34;
    exit 0
fi

# 读取之前保存的 IP 信息
OLD_OUTPUT=$(cat &#34;$IP_FILE&#34;)

# 检查 ifconfig 输出是否发生变化
if [ &#34;$NEW_OUTPUT&#34; != &#34;$OLD_OUTPUT&#34; ]; then
    echo &#34;[$(date &#39;&#43;%Y-%m-%d %H:%M:%S&#39;)] ifconfig 输出发生变化，开始更新...&#34; &gt;&gt; &#34;$LOG_FILE&#34;
    echo &#34;$NEW_OUTPUT&#34; &gt; &#34;$IP_FILE&#34;
    cd &#34;$REPO_DIR&#34; || exit 1
    git add .
    git commit -m &#34;Updated ifconfig output&#34; &gt;&gt; &#34;$LOG_FILE&#34; 2&gt;&amp;1
    git push origin main &gt;&gt; &#34;$LOG_FILE&#34; 2&gt;&amp;1
    echo &#34;[$(date &#39;&#43;%Y-%m-%d %H:%M:%S&#39;)] ifconfig 变化已提交到 Gitee&#34; &gt;&gt; &#34;$LOG_FILE&#34;
else
    echo &#34;[$(date &#39;&#43;%Y-%m-%d %H:%M:%S&#39;)] ifconfig 输出没有变化&#34; &gt;&gt; &#34;$LOG_FILE&#34;
fi
```

并确保文件具有可执行权限

```
sudo chmod &#43;x update_ip.sh
```

测试脚本

```
./update_ip.sh
```

## 4. 使用 systemd 服务

创建 systemd 服务单元,新建一个服务单元文件，例如``sudo vim /etc/systemd/system/update-ip.service``,内容如下：

```
[Unit]
Description=Run update_ip.sh script

[Service]
Type=oneshot
User=lwb
Group=lwb
WorkingDirectory=/home/lwb/repository/A100IP
ExecStart=/home/lwb/repository/A100IP/update_ip.sh
```

新建一个 timer 单元文件，这里设置开机后延迟1分钟启动，然后每隔5分钟执行一次。例如 ``sudo vim /etc/systemd/system/update-ip.timer``，内容如下：

```
[Unit]
Description=Run update_ip.sh every 5 minutes

[Timer]
OnBootSec=1min
OnUnitActiveSec=5min
Persistent=true

[Install]
WantedBy=timers.target
```

运行以下命令：

```
sudo systemctl daemon-reload
sudo systemctl enable update-ip.timer
sudo systemctl start update-ip.timer
```





      


---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/3e6ebde/  

