## 在华为云鲲鹏920服务器上安装Fedora的备注

由于鲲鹏920的一些固件Bug，必须添加一些内核参数才能启动。

启动安装介质后，选择‘Install Fedora’，然后按e更改命令行，将以下参数加入到linux开头的行末尾：

```
initcall_blacklist=hisi_ddrc_pmu_module_init arm64.nompam
```

然后就可以启动了。

由于另一些Bug，在安装页面中鼠标指针似乎无法渲染，请使用Tab 空格和回车键进行操作。

然后可以执行正常安装流程。

相比于X86服务器，ARM服务器上的一些安装操作似乎很慢。我认为这可能是因为鲲鹏920的性能导致的。

在安装完成后，继续添加参数来初次启动服务器。

然后执行下面的命令添加并固化启动参数：

```sh
echo "GRUB_CMDLINE_LINUX_DEFAULT=\"initcall_blacklist=hisi_ddrc_pmu_module_init arm64.nompam\"" >> /etc/default/grub
grub2-mkconfig -o /boot/grub2/grub.cfg
```

然后按照[标准步骤](./InstallFedora.md)操作。

参考：[OpenSUSE.org](https://zh.opensuse.org/%E9%B2%B2%E9%B9%8F920%E5%8F%B0%E5%BC%8F%E6%9C%BA%E5%AE%89%E8%A3%85)
