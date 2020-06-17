# WindowsTerminal

My windows terminal configfile.

## 安装 Chocolatey
安装 Chocolatey，只需要在 Windows 系统的命令行工具下面去执行一行命令（cmd），只需要在其中的一个上面安装 Chocolatey 就可以了。你要用管理员的身份去运行命令行工具，不然会遇到权限问题。
终端下执行。
```bash
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```
安装完成后，在命令行工具的下面，输入：
```bash
choco help
```
如果出现一些有用的帮助信息，比如 Chocolatey 的版本号，安装到的目录，相关的命令，还有示例等等，这就说明我们已经可以在系统上使用 Chocolatey 了。
Chocolatey的使用也很简单，使用指令如下：
```bash
choco search <keyword>    搜索软件
choco list <keyword>  跟 search 命令功能类似
choco install <package1 package2 package3...>  安装软件
choco install <package>  -version *** 安装指定版本
choco  uninstall name 卸载软件
choco version <package>  查看安装包的版本情况
choco  upgrade <package>   更新某个软件 
choco list -localonly        查看一下所有安装在本地的包的列表
choco list -lo       功能同上
```

## 安装 Windows Terminal

在安装 Windows Terminal 之前，需要确保 Windows 版本号在 18362 以上。使用搜索功能或访问链接即可到达商店页面。
在下一步配置之前，你可能想要安装 VSCode 以编辑配置文件。你可能还想安装更纱黑体字体以获取更好的观感。（可跳过）
下文假设你已成功安装 Windows Terminal。
## WSL2 安装
检查 windows 版本

>Windows 10, updated to version 2004, Build 19041 or higher.

开启 "Windows Subsystem for Linux"  

以管理员身份打开 PowerShell，输入如下命令，并重启电脑
```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
设置 WSL2 为默认

打开 PowerShell，输入如下命令：
```bash
wsl --set-default-version 2
```

## 安装Linux发行版
打开Microsoft Sotre，搜索Linux，本例选择 Ubuntu 18.04.

## 美化 Powershell

由于 Windows 10 后期版本主推 Powershell 而非 cmd，对 Windows Terminal 的美化实际上主要是针对 Powershell。
本文所用的 PS 主题搭配是比较热门的 oh-my-posh 和 Paradox.

### 安装 oh-my-posh（和 posh-git）

按照主页的指示，一步一步在 Powershell 终端执行以下语句：(使用 Win-X 组合键，选中 Powershell）

```
# 安装posh-git和oh-my-posh
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```

如果你使用管理员权限打开 PowerShell 并且想把 oh-my-posh 安装到所有用户，则输入

```
Install-Module posh-git
Install-Module oh-my-posh
```

这里如果让你允许什么不可信的来源，输入 Y 表示同意即可。
安装完成后，输入

```
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme PowerLine
```
**如果你的电脑里没有安装Git，在输入Import-Module posh-git会报错，解决方法是安装Git或者把这一行去掉。**

但是这次使用Import-Module的指令，再次启动PowerShell就会发现没有效果，这是因为这些指令仅限于本次会话的PowerShell有效，因此，若要使这一效果在每次启动的时候都有效，那就要将其添加到启动脚本中。

打开~\Documents\WindowsPowerShell，新建文本文档，叫做Microsoft.PowerShell_profile.ps1（记得开拓展名显示），输入以下内容，保存。
```
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme PowerLine
```
这样，在每次PoweShell打开的时候都能启用PowerLine主题。

### 配置终端

Windows Terminal的配置文件储存在
**~\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\setting.json**
这个json文件中。
添加*setting.json*文件到此目录中,图标在icon文件夹下。

在下箭头处展开列表，选中设置打开JSON配置文件（也可使用默认的“Ctrl+,”组合键）后定位到profiles区域，可单独对不同终端进行配置。
```
    "profiles" : 
    [
        {
            "acrylicOpacity" : 0.70, //亚克力背景透明度（需启用useAcrylic）
            "background" : "#012456", //背景颜色，PS默认为蓝色
            "closeOnExit" : true, //关闭窗口的时候退出所有挂载的程序
            "colorScheme" : "Dracula", //配色方案（Dracula需导入）
            "commandline" : "powershell.exe", //此处终端打开PS
            "cursorColor" : "#FFFFFF", //光标颜色
            "cursorShape" : "bar", //光标形状（默认为bar，即条状）
            "fontFace" : "Consolas", //所用字体
            "fontSize" : 14, //字体大小
            "guid" : "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}", //唯一标识符，随机生成
            "historySize" : 9001, //缓存大小
            "icon" : "ms-appx:///ProfileIcons/{61c54bbd-c2c6-5271-96e7-009a87ff44bf}.png", //图标
            "name" : "Windows PowerShell", //在下拉菜单里显示的名称
            "tabTitle" : "Windows PowerShell", //在选项卡上显示的名称
            "padding" : "0, 0, 0, 0", //内容的边框距，默认填充全部空间
            "snapOnInput" : true, //输入的时候自动滚动到输入位置
            "startingDirectory" : "%USERPROFILE%", //初始工作目录，默认为用户目录
            "useAcrylic" : true //使用亚克力效果
        }
    ]
```

## 安装其他应用
安装Screenfetch
```bash
Install-Module -Name windows-screenfetch
Set-ExecutionPolicy -ExecutionPolicy Unrestricted
Import-Module windows-screenfetch
```