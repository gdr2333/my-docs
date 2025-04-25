*Lagrange v2正在开发中，本文档不适用于v2。*

## 这是在各种Linux发行版上安装Lagrange.OneBot的说明。

### 已知限制：

由于数据库不兼容，无法在基于musl libc的发行版（Alpine Linux, Gentoo Linux musl profile...）上正确运行Lagrange。 *不适用于v2*

Lagrange要求.NET 8.0或更高版本的运行时，这意味着早于Ubuntu 20.04的Linux发行版很可能连依赖都装不上。~~真的有人还在用这么老的系统吗~~

---

### 【可选】自己编译！

编译一个.NET项目其实很简单，并且在这个场景下能带来实际上的好处（比如使用未发布的补丁）。

下面的例子使用.NET SDK 8.0。

##### 略：安装git（这个教程自己找）

##### 略：安装.NET SDK（参见[微软网站](https://dotnet.microsoft.com/zh-cn/download/dotnet/8.0)）

##### 需要对github的网络连接（如果你能看到这一行，基本意味着你有。）

#### 第一步：找个空文件夹

需要我教你吗？

#### 第二步：拉取源码

```sh
git clone https://github.com/LagrangeDev/Lagrange.Core
```

#### 第三步：发布项目

##### 如果你希望不在目标机器上部署运行时：

```sh
dotnet publish Lagrange.Core\Lagrange.OneBot\Lagrange.OneBot.csproj --sc -r {os}-{arch} -c Release -f net8.0
```

<details>

--sc是--self-contained的短选项，意味着打包运行时。

-r是--runtime的短选项，用于指定目标平台。对于要打包运行时的情况，这是必须的。

-c是--configuration的短选项，用于指定配置。-c Release以为这使用发布配置。

-f用于指定框架。-f net8.0意味着使用.NET 8作为目标框架。

</details>

os是你要发布到的系统，arch是该系统的架构。

*注意：*

*对于使用musl libc的Linux发行版，os应该是linux-musl而非linux。但你不用管，因为Lagrange不支持musl。*

*arch使用Microsoft风格的标识符，这意味着你该使用：*

|Linux上常用的名字|这里用的名字|其他名字|备注|
|-|-|-|-|
|amd64|x64|x86_64，Intel64（注意不是IA64）||
|armhf|arm||需要硬件浮点单元；可能出现问题|
|aarch64|arm64|||
|loongarch|loongarch64|LA64|新世界；Lagrange官方大概不管你；真的有人用吗|

**对于没有在这里出现的架构，除非第三方发布了支持它们的SDK，否则部署一个单独的运行时是必须的。**

##### 如果你想要使用运行时，或者想要编译到非特定平台（Anycpu）：

```sh
dotnet publish Lagrange.Core\Lagrange.OneBot\Lagrange.OneBot.csproj -c Release -f net8.0
```

命令解释参见上面。

#### 第四步：打包

将`Lagrange.Core\Lagrange.OneBot\bin\Release\net8.0\{os}-{arch}\publish\`（指定平台）或`Lagrange.Core\Lagrange.OneBot\bin\Release\net8.0\publish\`（Anycpu）中的文件使用你喜欢的方式打包。

*其中的.pdb文件是调试符号，不需要调试的场景可以安全的删除它们。*

---

### 下载

到[Github Release](https://github.com/LagrangeDev/Lagrange.Core/releases)下载文件。

文件格式应该是`Lagrange.OneBot_{os}-{arch}_net*.*_SelfContained.*`。

**os表格**

|常用名|os的值|备注|
|-|-|-|
|MacOS|osx|并不真的支持MacOS 10|
|GNU/Linux|linux|不支持musl libc|
|Windows|win||

**arch的值见上面。**

---

### 【可选？】安装运行时

**如果你自己编译了Anycpu的版本，你必须要安装运行时。**

##### Ubuntu 22.04+

```sh
apt install dotnet-runtime-8.0
```

##### Enterprise Linux 8+, Fedora Linux

```sh
dnf install dotnet-runtime-8.0
```

##### Alpine Linux（这并不会让Lagrange兼容Alpine Linux，我只是写一下）

```sh
apk add dotnet8-runtime
```

~~也不知道为什么Alpine不随大流~~

##### Arch Linux

```sh
pacman -Sy dotnet-runtime-8.0
```

*你可以不加S，但是不同步数据库很可能出问题。*

##### Gentoo Linux

```sh
emerge -av =dev-dotnet/dotnet-sdk-8.0
```

##### 微软包源

参见 https://learn.microsoft.com/zh-cn/dotnet/core/install/linux

*可能需要科学上网。*

##### Snap（可能会出现奇奇怪怪的问题，备选中的备选）：

```sh
snap install dotnet-runtime-80
```

### 配置

我不会重新制作教程（除非写的太烂）。请[自己去看](https://lagrangedev.github.io/Lagrange.Doc/Lagrange.OneBot/)。

*直接把一些东西告诉你们是不被允许的，不过你可能想去问问。*

### 运行

使用运行时

```sh
dotnet ./Lagrange.OneBot.dll
```

自包含版本

```sh
./Lagrange.OneBot
```

*你可能需要`chmod +x ./Lagrange.OneBot`*

### 优化

其实没什么好优化的。

#### 启用DATAS

将`DOTNET_GCDynamicAdaptationMode=1`添加到你的环境变量。

### 自启动

这是一个写好的启动脚本。

```
[Unit]
Description=QQ NT Server
Documentation=https://github.com/LagrangeDev/Lagrange.Core
Requires=network.target

[Service]
User=lagrange
Restart=no
WorkingDirectory=/opt/Lagrange
Environment=DOTNET_GCDynamicAdaptationMode=1 DOTNET_gcServer=0
ExecStart=/usr/bin/dotnet /opt/Lagrange/Lagrange.OneBot.dll

[Install]
WantedBy=multi-user.target
```