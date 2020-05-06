# WindowsTerminal

My windows terminal configfile.

## 安装 Windows Terminal

在安装 Windows Terminal 之前，需要确保 Windows 版本号在 18362 以上。使用搜索功能或访问链接即可到达商店页面。
在下一步配置之前，你可能想要安装 VSCode 以编辑配置文件。你可能还想安装更纱黑体字体以获取更好的观感。（可跳过）
下文假设你已成功安装 Windows Terminal。

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