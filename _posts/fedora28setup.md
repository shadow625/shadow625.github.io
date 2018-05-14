全新Linux设置集合

1. 命令行

{% highlight bash %}
[bogon@shadow ]~ $vi .bashrc 

# .bashrc

export PS1="[\h@\u ]\[\033[01;32m\]\W\[\033[00m\] \$"

source .bashrc

{% endhighlight %}

2. ssh 免密登录 ssh-keygen -t rsa
vi authorized_keys
chmod 600 ~/.ssh/authorized_keys 

3.配置源，（国内设置阿里云，比较快）
sudo wget -O /etc/yum.repos.d/fedora.repo http://mirrors.aliyun.com/repo/fedora.repo
sudo wget -O /etc/yum.repos.d/fedora-updates.repo http://mirrors.aliyun.com/repo/fedora-updates.repo
sudo yum makecache


**-错误：同步仓库 'updates-modular' 缓存失败-**
到/etc/yum.repos.d/下删除对应repo
停在源这里了   

dnf repolist all
vi /var/log/dnf.log 查看发生什么错误。

提示没找到key<br>
rpmkeys --import /etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-**28**-primary
