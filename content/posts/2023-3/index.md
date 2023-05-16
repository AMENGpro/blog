---
title: "终端代理设置"
date: 2023-05-03T00:00:00+08:00
draft: false
authors: ["zhyoch"]
tags: [Bash,CMD,Git,Linux,PowerShell,Proxy,Windows,ZSH]
featuredImagePreview: "/2020-1/featuredImagePreview.svg"
summary: Git, Linux 与 Windows 的终端代理设置。
---

## CMD

### 临时代理

{{< admonition type=note title="注意" open=true >}}
只对当前终端有效, 新建终端需要重新设置。
{{< /admonition >}}

**格式**: 

```shell
set http_proxy=protocol://[proxy_userid]:[proxy_password]@proxy_ip:proxy_port
```

输入设置代理的命令: 

**HTTP代理**: 

```shell
set http_proxy=http://127.0.0.1:7890
set https_proxy=http://127.0.0.1:7890
```

或者

**SOCKS5代理**: 

```shell
set http_proxy=socks5://127.0.0.1:7890
set https_proxy=socks5://127.0.0.1:7890
```

使用命令查看是否设置成功: 

```shell
echo %http_proxy%
echo %https_proxy%
```

### 取消代理

取消当前终端的代理设置: 

```shell
set http_proxy=
set https_proxy=
```

### 永久代理

#### 方法一: 默认开启代理

1. 新建一个`cmd_init.cmd`, 将上面相应的代理命令写入。
2. 打开注册表, 在`HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor\`下新建名为`AutoRun`的**字符串值**, 数据的值是一个绝对路径, 路径指向刚才新建的`cmd_init.cmd`, 比如`C:\Users\Username\cmd_init.cmd`。
3. 此脚本会在每次打开cmd时被预加载。
4. 修改文件权限, 禁用继承 (转化为显式权限) , 除`SYSTEM`和`Administrators`设为**完全控制**外, 其余用户均设为**读取和执行**。

{{< image src="cmd.png" caption="cmd_init.cmd" height="auto" width="100%">}}

#### 方法二: function作为开关(推荐)

上面的[方法一: 默认开启代理](#方法一-默认开启代理), 终端一打开就默认启用了代理, 如要关闭还需输入一长串命令。有一种更好的办法: 在`cmd_init.cmd`中不默认启用代理, 而是设置灵活的别名作为代理的开关: 

```shell
DOSKEY proxy-on=set http_proxy=http://127.0.0.1:7890$tset https_proxy=http://127.0.0.1:7890
DOSKEY proxy-off=set http_proxy=$tset https_proxy=
```
{{< admonition type=tip title="注意" open=true >}}
没错, `$t`的前后不需要有空格, 可以直接连接两条命令: command1`$t`command2。
{{< /admonition >}}

日常使用时, 输入`proxy-on`即可设置代理, 输入`proxy-off`即可取消设置代理。

## PowerShell

### 临时代理

{{< admonition type=note title="注意" open=true >}}
只对当前终端有效, 新建终端需要重新设置。
{{< /admonition >}}

**格式**: 

```shell
$env:http_proxy="protocol://[proxy_userid]:[proxy_password]@proxy_ip:proxy_port"
```

输入设置代理的命令: 

**HTTP代理**: 

```shell
$env:http_proxy="http://127.0.0.1:7890"
$env:https_proxy="http://127.0.0.1:7890"
```

或者

**SOCKS5代理**: 

```shell
$env:http_proxy="socks5://127.0.0.1:7890"
$env:https_proxy="socks5://127.0.0.1:7890"
```

使用命令查看是否设置成功: 

```shell
$env:http_proxy
$env:https_proxy
```

### 取消代理

取消当前终端的代理设置: 

```shell
$env:http_proxy=""
$env:https_proxy=""
```

### 永久代理

#### 方法一: 默认开启代理

参考微软[官方文档](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles#how-to-create-a-profile), 为所有用户、所有主机生成`profile`文件: 

1. 在PowerShell中运行以下命令: 

    ```shell
    if (!(Test-Path -Path $PROFILE.AllUsersAllHosts)) { New-Item -ItemType File -Path $PROFILE.AllUsersAllHosts -Force };
    ```

    {{< admonition type=tip title="其他级别" open=true >}}
- Current User, Current Host - $PROFILE
- Current User, Current Host - $PROFILE.CurrentUserCurrentHost
- Current User, All Hosts - $PROFILE.CurrentUserAllHosts
- All Users, Current Host - $PROFILE.AllUsersCurrentHost
- All Users, All Hosts - $PROFILE.AllUsersAllHosts
    {{< /admonition >}}

2. 使用`notepad $PROFILE.AllUsersAllHosts`命令调用记事本打开`profile`文件, 在文件中写入上面相应的代理命令, 保存关闭即可, 该文件会在每次打开PowerShell时被预加载。
3. 如果是`Current User, Current Host`级别, 则`profile`文件为`此电脑/文档/WindowsPowerShell/Microsoft.PowerShell_profile.ps1`
4. 如果是`All Users, All Hosts`级别, 则`profile`文件为`C:\Windows\System32\WindowsPowerShell\v1.0\profile.ps1`
5. 如果在PowerShell 7生成`profile`文件, 则一律为`C:\Program Files\PowerShell\7\profile.ps1`
6. 修改文件权限, 禁用继承 (转化为显式权限) , 除`SYSTEM`和`Administrators`设为**完全控制**外, 其余用户均设为**读取和执行**。

{{< image src="powershell.png" caption="Microsoft.PowerShell_profile.ps1" height="auto" width="100%">}}

##### Windows不允许运行脚本? 
参考微软官方文档[Set-ExecutionPolicy](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.security/set-executionpolicy), 以管理员身份运行PowerShell, 运行以下命令: 

```shell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
```

#### 方法二: function作为开关(推荐)

上面的[方法一: 默认开启代理](#方法一-默认开启代理-1), 终端一打开就默认启用了代理, 如要关闭还需输入一长串命令。有一种更好的办法: 在`profile`文件中不默认启用代理, 而是设置灵活的`function`作为代理的开关: 

```shell
function proxy-on {
    $env:http_proxy="http://127.0.0.1:7890"
    $env:https_proxy="http://127.0.0.1:7890"
}

function proxy-off {
    $env:http_proxy=""
    $env:https_proxy=""
}
```

日常使用时, 输入`proxy-on`即可设置代理, 输入`proxy-off`即可取消设置代理。

## Bash、Zsh等

### 临时代理

{{< admonition type=note title="注意" open=true >}}
只对当前终端有效, 新建终端需要重新设置。
{{< /admonition >}}

输入设置代理的命令: 

**格式**: 

```bash
export http_proxy=protocol://[proxy_userid]:[proxy_password]@proxy_ip:proxy_port
```

**HTTP代理**: 

```bash
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
```

**SOCKS5代理**:

```bash
export http_proxy=socks5://127.0.0.1:7890
export https_proxy=socks5://127.0.0.1:7890
```

设置终端中的**wget**、**curl**等软件都走**SOCKS5**代理: 

```bash
export ALL_PROXY=socks5://127.0.0.1:7890
```

### 取消代理

取消当前终端的代理设置: 

```bash
unset http_proxy https_proxy
unset ALL_RPOXY
```

### 永久代理

#### 方法一: 默认开启代理

{{< admonition type=note title="环境变量配置文件" open=true >}}
`/etc/envirnoment`与`shell`无关, 所以无法使用脚本或通配符展开。此文件仅接受`variable=value`键值对格式。

其他文件的加载顺序: `/etc/profile`>`/etc/bash.bashrc`>`~/.profile`=`~/.bash_profile`>`~/.bashrc`
{{< /admonition >}}

1. 将上面的临时代理命令写入环境变量配置文件中。
2. 运行`source /etc/bash.bashrc`或`source ~/.bashrc`以应用新的环境变量。
3. 这样当前终端和新建的终端就会使用代理。

#### 方法二: alias作为开关(推荐)

1. 通过设置**alias**来简化操作。将以下命令写入环境变量配置文件中。

    ```bash
    alias proxy-on="export http_proxy=http://127.0.0.1:7890;export https_proxy=http://127.0.0.1:7890"
    alias proxy-off="unset http_proxy https_proxy"
    ```

2. 运行`source /etc/bash.bashrc`或`source ~/.bashrc`以应用新的环境变量。
3. 每次要使用代理就输入`proxy-on`, 不用了就输入`proxy-off`。

#### 方法三: function作为开关(推荐)

1. 通过设置**function**来简化操作。将以下命令写入环境变量配置文件中。

    ```bash
    function proxy-on() {
        export http_proxy=http://127.0.0.1:7890
        export https_proxy=http://127.0.0.1:7890
    }

    function proxy-off() {
        unset http_proxy https_proxy
    }
    ```

2. 运行`source /etc/bash.bashrc`或`source ~/.bashrc`以应用新的环境变量。
3. 每次要使用代理就输入`proxy-on`, 不用了就输入`proxy-off`。

## Git设置代理

### 永久代理

#### 方法一: 默认开启代理

{{< admonition type=note title="注意" open=true >}}
使用`--global`参数即全局永久生效, 不使用则对当前仓库永久生效, 相当于`--local`, 关于配置级别, 参考[Git Config](https://zhyoch.netlify.app/2020-7/#配置级别)。
{{< /admonition >}}

**格式**: 

```shell
git config --global http.proxy protocol://[proxy_userid]:[proxy_password]@proxy_ip:proxy_port
```

**HTTP代理**: 

```shell
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

**SOCKS5代理**: 

```shell
git config --global http.proxy socks5://127.0.0.1:7890
git config --global https.proxy socks5://127.0.0.1:7890
```

##### 取消代理

```shell
git config --global --unset http.proxy
git config --global --unset https.proxy
```

使用`git config --global --list`命令查看是否设置成功。

#### 方法二: 使用作用于Shell的方案(推荐)

使用上文中作用于`cmd`, `PowerShell`, `bash`, `zsh`等shell的方案, 在shell中使用git命令, git也会走代理, 这样更灵活。