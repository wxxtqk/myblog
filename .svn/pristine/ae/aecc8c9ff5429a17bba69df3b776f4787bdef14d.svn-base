---
title: gitlab在centos7上的安装及一些配置
categories:
  -gitlab
---
前期的准备，centos7+虚拟机（或者真实机）,本教程介绍的是Linux的yum安装，这样会自动解决一些依赖关系
首先安装好centos，并确定已经电脑联网

1、安装gitlab

在centos7上,执行以下命令，将在系统防火墙里面开放HTTP和SSH端口.在执行以下命令的时候最好更新一下yum，该gitlab是在root下面安装。

    yum update

然后在安装

    sudo yum install curl policycoreutils openssh-server openssh-clients
    sudo systemctl enable sshd
    sudo systemctl start sshd
    sudo yum install postfix
    sudo systemctl enable postfix
    sudo systemctl start postfix
    sudo firewall-cmd --permanent --add-service=http
    sudo systemctl reload firewalld

2、添加GitLab仓库,并安装到服务器上

    curl -sS http://packages.gitlab.cc/install/gitlab-ce/script.rpm.sh | sudo bash
    sudo yum install gitlab-ce

3、 启动GitLab

    sudo gitlab-ctl reconfigure

4、使用浏览器访问GitLab

首次访问GitLab,系统会让你重新设置管理员的密码,设置成功后会返回登录界面.

默认的管理员账号是root,如果你想更改默认管理员账号,请输入上面设置的新密码登录系统后修改帐号名.

5、gitlab创建备份

使用一条命令即可创建完整的gitlab备份

    gitlab-rake gitlab:backup:create

使用以上命令会在/var/opt/gitlab/backups目录下创建一个名称类似为148402929020170110gitlab_backup.tar的压缩包,这个压缩包就是Gitlab整个的完整部分, 其中开头的20170110是备份创建的日期，可以进入到备份的目录下查看

    cd /var/opt/gitlab/backups

然后在执行

    ls

就可以查看你所有的备份

6、gitlab修改备份文件默认目录

你也可以通过修改/etc/gitlab/gitlab.rb来修改默认存放备份文件的目录

    gitlab_rails['backup_path'] = '/mnt/backups'

/mnt/backups修改为你想存放备份的目录即可, 修改完成之后使用gitlab-ctl reconfigure命令重载配置文件即可.

7、gitlab自动备份

通过通过crontab使用备份命令实现自动备份

    sudo su -
    crontab -e

加入以下, 实现每天凌晨6点进行一次自动备份:

    0 6 * * * /opt/gitlab/bin/gitlab-rake gitlab:backup:create

建议每隔几天备份，不需要每天都备份，如果数据比较重要的话，就每天自动备份

8、gitlab恢复

    # 停止相关数据连接服务
    gitlab-ctl stop unicorn
    gitlab-ctl stop sidekiq
    
    # 从148402929020170110编号备份中恢复
    gitlab-rake gitlab:backup:restore BACKUP=148402929020170110
    
    # 启动Gitlab
    sudo gitlab-ctl start

9、gitlab迁移

迁移如同备份与恢复的步骤一样, 只需要将老服务器/var/opt/gitlab/backups目录下的备份文件拷贝到新服务器上的/var/opt/gitlab/backups即可(如果你没修改过默认备份目录的话). 但是需要注意的是新服务器上的Gitlab的版本必须与创建备份时的Gitlab版本号相同. 比如新服务器安装的是最新的7.60版本的Gitlab, 那么迁移之前, 最好将老服务器的Gitlab 升级为7.60在进行备份

10、gitlab服务器ip地址设置，解决仓库地址为localhost的问题

修改gitlab.yml 文件的localhost的即可,进入一下文件

    cd /opt/gitlab/embedded/service/gitlab-rails/config  

修改gitlab.yml 

    vi gitlab.yml

打开文件后把host:localhost改为lost:你对应的ip就行了

然后重启gitlab

    sudo gitlab-ctl restart  

然后打开浏览器，输入ip就行行了啦
