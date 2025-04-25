*Lagrange v2���ڿ����У����ĵ���������v2��*

## �����ڸ���Linux���а��ϰ�װLagrange.OneBot��˵����

### ��֪���ƣ�

�������ݿⲻ���ݣ��޷��ڻ���musl libc�ķ��а棨Alpine Linux, Gentoo Linux musl profile...������ȷ����Lagrange�� *��������v2*

LagrangeҪ��.NET 8.0����߰汾������ʱ������ζ������Ubuntu 20.04��Linux���а�ܿ�����������װ���ϡ�~~������˻�������ô�ϵ�ϵͳ��~~

---

### ����ѡ���Լ����룡

����һ��.NET��Ŀ��ʵ�ܼ򵥣�����������������ܴ���ʵ���ϵĺô�������ʹ��δ�����Ĳ�������

���������ʹ��.NET SDK 8.0��

##### �ԣ���װgit������̳��Լ��ң�

##### �ԣ���װ.NET SDK���μ�[΢����վ](https://dotnet.microsoft.com/zh-cn/download/dotnet/8.0)��

##### ��Ҫ��github���������ӣ�������ܿ�����һ�У�������ζ�����С���

#### ��һ�����Ҹ����ļ���

��Ҫ�ҽ�����

#### �ڶ�������ȡԴ��

```sh
git clone https://github.com/LagrangeDev/Lagrange.Core
```

#### ��������������Ŀ

##### �����ϣ������Ŀ������ϲ�������ʱ��

```sh
dotnet publish Lagrange.Core\Lagrange.OneBot\Lagrange.OneBot.csproj --sc -r {os}-{arch} -c Release -f net8.0
```

<details>

--sc��--self-contained�Ķ�ѡ���ζ�Ŵ������ʱ��

-r��--runtime�Ķ�ѡ�����ָ��Ŀ��ƽ̨������Ҫ�������ʱ����������Ǳ���ġ�

-c��--configuration�Ķ�ѡ�����ָ�����á�-c Release��Ϊ��ʹ�÷������á�

-f����ָ����ܡ�-f net8.0��ζ��ʹ��.NET 8��ΪĿ���ܡ�

</details>

os����Ҫ��������ϵͳ��arch�Ǹ�ϵͳ�ļܹ���

*ע�⣺*

*����ʹ��musl libc��Linux���а棬osӦ����linux-musl����linux�����㲻�ùܣ���ΪLagrange��֧��musl��*

*archʹ��Microsoft���ı�ʶ��������ζ�����ʹ�ã�*

|Linux�ϳ��õ�����|�����õ�����|��������|��ע|
|-|-|-|-|
|amd64|x64|x86_64��Intel64��ע�ⲻ��IA64��||
|armhf|arm||��ҪӲ�����㵥Ԫ�����ܳ�������|
|aarch64|arm64|||
|loongarch|loongarch64|LA64|�����磻Lagrange�ٷ���Ų����㣻�����������|

**����û����������ֵļܹ������ǵ�����������֧�����ǵ�SDK��������һ������������ʱ�Ǳ���ġ�**

##### �������Ҫʹ������ʱ��������Ҫ���뵽���ض�ƽ̨��Anycpu����

```sh
dotnet publish Lagrange.Core\Lagrange.OneBot\Lagrange.OneBot.csproj -c Release -f net8.0
```

������Ͳμ����档

#### ���Ĳ������

��`Lagrange.Core\Lagrange.OneBot\bin\Release\net8.0\{os}-{arch}\publish\`��ָ��ƽ̨����`Lagrange.Core\Lagrange.OneBot\bin\Release\net8.0\publish\`��Anycpu���е��ļ�ʹ����ϲ���ķ�ʽ�����

*���е�.pdb�ļ��ǵ��Է��ţ�����Ҫ���Եĳ������԰�ȫ��ɾ�����ǡ�*

---

### ����

��[Github Release](https://github.com/LagrangeDev/Lagrange.Core/releases)�����ļ���

�ļ���ʽӦ����`Lagrange.OneBot_{os}-{arch}_net*.*_SelfContained.*`��

**os���**

|������|os��ֵ|��ע|
|-|-|-|
|MacOS|osx|�������֧��MacOS 10|
|GNU/Linux|linux|��֧��musl libc|
|Windows|win||

**arch��ֵ�����档**

---

### ����ѡ������װ����ʱ

**������Լ�������Anycpu�İ汾�������Ҫ��װ����ʱ��**

##### Ubuntu 22.04+

```sh
apt install dotnet-runtime-8.0
```

##### Enterprise Linux 8+, Fedora Linux

```sh
dnf install dotnet-runtime-8.0
```

##### Alpine Linux���Ⲣ������Lagrange����Alpine Linux����ֻ��дһ�£�

```sh
apk add dotnet8-runtime
```

~~Ҳ��֪��ΪʲôAlpine�������~~

##### Arch Linux

```sh
pacman -Sy dotnet-runtime-8.0
```

*����Բ���S�����ǲ�ͬ�����ݿ�ܿ��ܳ����⡣*

##### Gentoo Linux

```sh
emerge -av =dev-dotnet/dotnet-sdk-8.0
```

##### ΢���Դ

�μ� https://learn.microsoft.com/zh-cn/dotnet/core/install/linux

*������Ҫ��ѧ������*

##### Snap�����ܻ��������ֵֹ����⣬��ѡ�еı�ѡ����

```sh
snap install dotnet-runtime-80
```

### ����

�Ҳ������������̳̣�����д��̫�ã�����[�Լ�ȥ��](https://lagrangedev.github.io/Lagrange.Doc/Lagrange.OneBot/)��

*ֱ�Ӱ�һЩ�������������ǲ�������ģ������������ȥ���ʡ�*

### ����

ʹ������ʱ

```sh
dotnet ./Lagrange.OneBot.dll
```

�԰����汾

```sh
./Lagrange.OneBot
```

*�������Ҫ`chmod +x ./Lagrange.OneBot`*

### �Ż�

��ʵûʲô���Ż��ġ�

#### ����DATAS

��`DOTNET_GCDynamicAdaptationMode=1`��ӵ���Ļ���������

### ������

����һ��д�õ������ű���

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