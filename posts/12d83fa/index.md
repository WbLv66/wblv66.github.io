# 设置开机自启动


&lt;!--more--&gt;
## 设置开机自启动

### 1. 创建一个启动脚本

```
cd ~
touch start_joy.sh
chmod &#43;x start_joy.sh
```

### 2. 编辑脚本文件



``vim start_joy.sh``

```
#!/bin/zsh

source /opt/ros/noetic/setup.zsh
source /home/nv/ants/devel/setup.zsh

roslaunch vehicle_rea joy_control.launch

```

### 3. 配置自动启动

- 创建 `~/.config/autostart` 目录（如果它不存在的话）
- 使用 `gnome-terminal` 打开一个新的终端窗口并执行上述脚本。编辑 `~/.config/autostart` 目录下的 `.desktop` 文件来实现这一点


``mkdir -p ~/.config/autostart``

创建一个新的 `.desktop` 文件，例如 `start_joy.desktop`

``vim ~/.config/autostart/start_joy.desktop``

```
[Desktop Entry]
Type=Application
Exec=gnome-terminal -- zsh -c &#34;~/start_joy.sh; exec zsh&#34;
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name[en_US]=Start Joy
Name=Start Joy
Comment[en_US]=Run start_joy.sh on startup
Comment=Run start_joy.sh on startup
```

其中``zsh``可以替换为``bash``

``gnome-terminal``可以替换为``terminator``

---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/12d83fa/  

