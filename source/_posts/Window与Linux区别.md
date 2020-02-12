---
title: Window与Linux的区别
date: 2020-02-12 21:08:07
tags:
	- dos
	- shell
categories:
	- 教程
---

### 文件目录操作

| Command            | Linux                 | Windows           |
| :----------------- | :-------------------- | :---------------- |
| 批处理             | .sh                   | .bat              |
| 帮助               | cmd --help /-h        |                   |
| 列出目录文件       | ls / ls -l            | dir               |
| 改变当前目录       | cd                    | cd                |
| 进入父级目录       | cd ..                 | cd ..             |
| 进入根目录         | cd  /                 | cd /              |
| 复制               | cp                    | copy              |
| 删除               | rm                    | del               |
| 新建目录           | mkdir                 | md                |
| 新建文件           | touch fileName        | type nul>fileName |
| 删除目录           | rmdir folderName      | rmdir folderName  |
| 设置目录文件所有者 | chown user.group file |                   |
| 设置目录文件权限   | chmod u+rwx fileName  |                   |

<!--more-->

### 文件内容操作

| Command            | Linux              | Windows |
| ------------------ | ------------------ | ------- |
| 显示文件内容       | cat                | type    |
|                    | more/less          | more    |
|                    | head /tail         |         |
| 统计行数           | wc                 |         |
| 显示文件信息       | file               |         |
| 查找文件           | find /bin -name ls |         |
| 定位可执行文件位置 | which              |         |
| 在文本文件内查找   | grep str1 1.txt    | find    |
| 启动运行程序       | gnome-open/open    | start   |

### 网络命令

| Command            | Linux                | Windows    |
| ------------------ | -------------------- | ---------- |
| 显示启动的网络服务 | netstat -anli less   | netstat    |
| 显示路由表信息     | netstat -r           | netstat -r |
| 显示ip             | ip a/ifconfig        | ipconfig   |
| 显示防火墙信息     | iptables -list       |            |
| 远程登陆           | ssh user@host        |            |
| 发送ping信息       | ping ip              | ping ip    |
| 命令行下载         | wget url/curl -o url |            |

### 进程/任务控制

| Command              | Linux               | Windows |
| -------------------- | ------------------- | ------- |
| 显示进程信息         | ps -auxf            |         |
| 杀死进程             | kill proc_id        |         |
| 杀死所有进程         | killall p ostgresql |         |
| 暂停中断当前前台任务 | ctrl - z            |         |
| 恢复任务到后台       | bg                  |         |
| 恢复任务到前台       | fg                  |         |

### 用户管理

| Command                | Linux            | Windows |
| ---------------------- | ---------------- | ------- |
| 修改密码               | passwd           |         |
| 创建用户               | useradd          |         |
| 删除用户               | userdel          |         |
| 修改用户               | usermod          |         |
| 退出                   | exit / ctrl + D  |         |
| 切换用户至（默认root） | su - user        |         |
| 以su后的权限执行       | sudo -u user cmd |         |

### 其他

| Command           | Linux                      | Windows           |
| ----------------- | -------------------------- | ----------------- |
| 显示日期时间      | date                       | date              |
| 日历              | cal2014                    |                   |
| 清除屏幕          | clear / ctrl + L           | cls               |
| 搜索软件包        | yum search tree            |                   |
| 删除软件包        | yum remove pkg_name        |                   |
| 安装软件包        | yum install pkg_name       |                   |
| 重启系统          | reboot                     | shutdown -r -t 00 |
| 关闭系统          | halt -p                    | shutdown -s -t 00 |
| 设置环境变量      | export  PATH=$PATH：～/bin | set               |
| 显示信息/环境变量 | echo $HOME                 | echo              |

### vi/vim编辑器使用

| vim的模式 |          |
| --------- | -------- |
| ESC       | 退出     |
| ：        | 命令行   |
| i         | 编辑模式 |

### vi命令行命令

| 命令     | 含义             |
| -------- | ---------------- |
| i        | 编辑模式         |
| I        | 行首插入         |
| a        | 追加模式         |
| A        | 行尾追加         |
| R        | 替换文字         |
| v        | 选择             |
| ctrl + v | 选择举行区域     |
| x        | 删除             |
| dd       | 剪切/删除行      |
| dw       | 剪切/删除字      |
| yy       | 拷贝行           |
| p        | 光标之后粘贴     |
| P        | 光标之前粘贴     |
| r        | 替换单个字符     |
| J        | 连接两行         |
| /        | 搜索             |
| n        | 下一个搜索结果   |
| cw       | 修改词语         |
| .        | 重复最后一个命令 |
| u        | 撤销             |
| ctrl + r | 重做             |
| w        | 保存             |
| q        | 关闭             |
| wq       | 保存并退出       |



