# linux挂载webdav到本地并开机自启
## 通过Webdav将网盘挂载到本地
### 安装davfs2
	sudo apt-get install davfs2 -y
### 配置davfs2
	/etc/davfs2/davfs2.conf
	在配置文件中找到下面这两项。如果前面有注释符号，请删除它，并并修改后面的数字：
	use_locks 0
	ignore_dav_header 1
	保存并退出编辑器
	键盘Esc
	输入 :wq
	
### 创建网盘挂载位置(注意进行用户提权)
	sudo mkdir /mnt/webdav/
	
### 挂载网盘到/mnt/webdav/
## 方式一 临时挂载
	sudo mount.davfs "http://127.0.0.1:5244/dav" /mnt/webdav/ -o uid=1000,gid=1000
	终端中会提示让你填写Username(登录的用户名）及Password(登录的密码)
### 检查是否已挂载
	ls /mnt/webdav/

### 添加以下内容
	"http://127.0.0.1:5244/dav"    admin(用户名)    JSnMmK2z(密码)
	注意替换自己的用户名和密码，且括号内容不用写
## 方式二 设置系统启动时自动挂载
	sudo vim /etc/fstab
	http://ip或者域名:端口号/dav /mnt/webdav davfs _netdev,auto 0 0
	这样设置后，每次debian启动时，都会自动尝试挂载WebDav到 /mnt/webdav目录

## 配置挂载自动认证
### 将用户名、密码写入配置文件
	vim /etc/davfs2/secrets
 	添加以下内容

	"http://127.0.0.1:5244/dav"    admin(用户名)    JSnMmK2z(密码)
