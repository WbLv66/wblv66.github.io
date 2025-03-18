# Wsl


&lt;!--more--&gt;

# wsl

在wsl的/etc/wsl.conf文件中加入如下内容
```
[interop]
appendWindowsPath = false
[automount]
enabled = false
```
理论上可以关闭与windows的交互，但是由于wsl共享了windows的网络，所以无法真正禁止磁盘挂载。

可以修改updatedb的搜索范围来减小磁盘挂载的影响，编辑 /etc/updatedb.conf的方法并不是对所有发行版全部适用，可以在.zshrc或者.bashrc中加入如下内容
```
alias updatedb=&#34;sudo updatedb --prunepaths=\&#34;/mnt/c /mnt/d\&#34;&#34;
```
以后只需要执行updatedb就行了


---

> 作者: Lv Wenbo  
> URL: https://WbLv66.github.io/posts/b9c4490/  

