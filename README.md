### kernel内核升级centos7版本

#### 一、安装yum源

```javascript
cat <<EOF > /etc/yum.repos.d/elrepo.repo
### Name: ELRepo.org Community Enterprise Linux Repository for el7
### URL: http://elrepo.org/

[elrepo]
name=ELRepo.org Community Enterprise Linux Repository - el7
baseurl=http://elrepo.org/linux/elrepo/el7/$basearch/
	http://mirrors.coreix.net/elrepo/elrepo/el7/$basearch/
	http://mirror.rackspace.com/elrepo/elrepo/el7/$basearch/
	http://repos.lax-noc.com/elrepo/elrepo/el7/$basearch/
mirrorlist=http://mirrors.elrepo.org/mirrors-elrepo.el7
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org
protect=0

[elrepo-testing]
name=ELRepo.org Community Enterprise Linux Testing Repository - el7
baseurl=http://elrepo.org/linux/testing/el7/$basearch/
	http://mirrors.coreix.net/elrepo/testing/el7/$basearch/
	http://mirror.rackspace.com/elrepo/testing/el7/$basearch/
	http://repos.lax-noc.com/elrepo/testing/el7/$basearch/
mirrorlist=http://mirrors.elrepo.org/mirrors-elrepo-testing.el7
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org
protect=0

[elrepo-kernel]
name=ELRepo.org Community Enterprise Linux Kernel Repository - el7
baseurl=http://elrepo.org/linux/kernel/el7/$basearch/
	http://mirrors.coreix.net/elrepo/kernel/el7/$basearch/
	http://mirror.rackspace.com/elrepo/kernel/el7/$basearch/
	http://repos.lax-noc.com/elrepo/kernel/el7/$basearch/
mirrorlist=http://mirrors.elrepo.org/mirrors-elrepo-kernel.el7
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org
protect=0

[elrepo-extras]
name=ELRepo.org Community Enterprise Linux Extras Repository - el7
baseurl=http://elrepo.org/linux/extras/el7/$basearch/
	http://mirrors.coreix.net/elrepo/extras/el7/$basearch/
	http://mirror.rackspace.com/elrepo/extras/el7/$basearch/
	http://repos.lax-noc.com/elrepo/extras/el7/$basearch/
mirrorlist=http://mirrors.elrepo.org/mirrors-elrepo-extras.el7
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org
protect=0
EOF
```

#### 二、列出可用源

```javascript
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```

#### 三、安装新内核.

```javascript
yum install kernel-lt.x86_64 --enablerepo="elrepo-kernel" -y
```

#### 四、查看内核并设置新内核启动

```javascript
cat /boot/grub2/grub.cfg | grep "CentOS" | grep "menuentry"
grub2-set-default "CentOS Linux (4.4.227-1.el7.elrepo.x86_64) 7 (Core)"

#重启
reboot
```

#### 五、查看内核启动项.

```javascript
grub2-editenv list
```

#### 六、检查

```javascript
uname -r
```

