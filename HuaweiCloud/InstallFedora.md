## 在华为云上安装Fedora的流程

**鲲鹏服务器用户请参照[这个文档](./FedoraOnKunpeng920.md)进行额外操作。**

请先按照标准华为云文档创建ISO镜像并创建安装服务器，然后按照标准流程安装Fedora Server。

安装后，先配置一些额外软件。一般来讲，cloud-init是建议安装的。

```sh
sudo dnf install cloud-init -y
```

如果你跟我一样喜欢用Cockpit，那么最好再安装一些Cockpit的额外组件

```sh
sudo dnf install cockpit cockpit-files cockpit-networkmanager cockpit-packagekit cockpit-selinux -y
```

*想用Cockpit的话，别忘了把TCP/9090加入安全组，当然如果你是全打开的狠人那当我没说。*

然后，在安装uniagent（华为的*傻逼*密码重置插件）之前，我们需要先为uniagent创建一个selinux策略文件。

```sh
echo "module my-uniagent 1.0;

require {
	type http_port_t;
	type usr_t;
	type user_tmp_t;
	type init_t;
	class file { append execute setattr write };
	class tcp_socket name_connect;
}

#============= init_t ==============

#!!!! This avc is allowed in the current policy
allow init_t http_port_t:tcp_socket name_connect;
allow init_t user_tmp_t:file execute;

#!!!! This avc is allowed in the current policy
allow init_t usr_t:file { append setattr write };" > my-uniagent.te

checkmodule -M -m -o my-uniagent.mod my-uniagent.te
semodule_package -o my-uniagent.pp -m my-uniagent.mod
sudo semodule -i my-uniagent.pp
```

然后安装uniagent。

在这一步的最后，我们还需要修复华为安装的时候留下的烂摊子——SELinux标签。

```sh
sudo restorecon -Rv /usr/local/uniagentd/bin
```

现在服务器镜像算是装完了。请用这个服务器制作系统盘镜像然后加入Fedora用户大军吧:D
