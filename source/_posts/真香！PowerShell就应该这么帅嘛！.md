---
title: 真香！PowerShell就应该这么帅嘛！（以及 WindowsTerminal 使用
date: 2020-05-23 13:10:21
category: 瞎折腾
tags: Powershell
thumbnail: https://media.everdo.cn/tank/pic-bed/2020/05/23/hxf-powershell.png
---

> 开学第三周了，两个字描述自己的生活（颓废）。

学校封闭式管理无法出门，寝室里熙熙攘攘凌晨一二点才睡。然而这一切都阻挡不了我是条咸鱼的事实。

无聊的刷着电脑的时候，突然对 Windows 自带的 PowerShell 心生歹念（dog

为什么这蓝底白字的命令行就这么丑呢？（根本配不上我帅气的颜值【yeah！】

[![ugly-powershell.jpg](https://media.everdo.cn/tank/pic-bed/2020/05/23/ugly-powershell.jpg)](https://up.media.everdo.cn/image/h7rx)

那么，让他变帅的时刻就到了！！！

## 改变颜色！

肤色当然是最影响观感的啦！长得白谁不喜欢（dog

改变 PowerShell 的颜色不仅可以通过系统自带的属性进行设置。还可以使用颜色工具包，设置主题色。

> 微软官方提供了一个更换 PowerShell 配色的小工具：ColorTool.exe，我们可以利用它来更换 PowerShell 的主题颜色。ColorTool 支持 iTerm 主题（以 .itermcolors 结尾的主题文件）。

下载地址：[ColorTool](https://github.com/Microsoft/console/tree/master/tools/ColorTool)

将下载的文件解压，移动到 C:\Windows

[![move-colortools.jpg](https://media.everdo.cn/tank/pic-bed/2020/05/23/move-colortools.jpg)](https://up.media.everdo.cn/image/hByI)

到这里，我们可以使用 ColorTools 命令为 PowerShell 导入主题配色

```powershell
#显示现有的主题包
ColorTool -s

#应用当前主题
ColorTool OneHalfDark.itermcolors

#设置默认配色方案
ColorTool -d OneHalfDark.itermcolors
```

[![colortools.jpg](https://media.everdo.cn/tank/pic-bed/2020/05/23/colortools.jpg)](https://up.media.everdo.cn/image/hRlX)

这里我选则使用 OneHalfDark 暗黑色配色文件，emm果然好看多了呢！

> ColorTool 直接支持 iTerm 主题配置文件，因此我们可以在 [iterm2colorschemes](https://iterm2colorschemes.com/) 这个网站找到我们想要的主题背景进行配置，方法和上面介绍的一样：在 PowerShell 中定位至你希望更换的主题文件，使用命令 colortool <主题名称>.itermcolors 进行配置即可。同时，如果你对上面的主题都不满意，你也可以直接在这个网站：[terminal.sexy](https://terminal.sexy/) 自行配置自己想要的主题，并通过同样的方式进行应用。


## 更换字体

肤色变好看只是变帅的第一步，那么现在到了发型的环节啦！！这一步，我们要为 PowerShell 安装自定义的字体：

PowerShell 默认的字体的新宋体，不用说，真的一点也不好看。更换字体的过程，理论上可以更换任何我们想要的字体。不过为了下一步能和我们的主题模块更好的兼容，这里推荐安装 powerline 字体

Powerline 字体在 GitHub 开源，我们可以在这里： [powerline/fonts](https://github.com/powerline/fonts) 下载支持相关字符的字体。

> 这里我使用的是 [Meslo LG M Regular Nerd Font](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Meslo/M/Regular/complete/Meslo%20LG%20M%20Regular%20Nerd%20Font%20Complete.ttf)

同样的 [更纱黑体](https://github.com/be5invis/Sarasa-Gothic) 也是一款很棒的 powerline 字体，不过因为某些原因，在我的电脑显示不正常

### 安装字体

下载了字体的 ttf 以后，只要右键安装就可以了！

[![install-font.jpg](https://media.everdo.cn/tank/pic-bed/2020/05/23/install-font.jpg)](https://up.media.everdo.cn/image/hoVi)

安装完不要忘记在设置中启用哦！

[![hxf-powershellfont.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/hxf-powershellfont.png)](https://up.media.everdo.cn/image/h2s4)

如果和我一样遇到在设置选项中找不到字体的，可以看这里（修改注册表！）

```
修改下列注册表值：
计算机\HKEY_CURRENT_USER\Console\%SystemRoot%_System32_WindowsPowerShell_v1.0_powershell.exe
```

将 CodePage 的十六进制数值改为 1b5 即可

[![eidt-regedittable.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/eidt-regedittable.png)](https://up.media.everdo.cn/image/hdrG)

现在就可以在字体设置列表看到本来不被兼容的字体啦，换上后，果然好看多了呢！

[![hxf-powershellfont82243b1a91387686.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/hxf-powershellfont82243b1a91387686.png)](https://up.media.everdo.cn/image/hFGM)

## 使用主题

人靠衣装佛靠金装，好看的小哥哥当然还得配好看的衣服，也就是这一步要安装的皮肤啦（滑稽

我们通过在 PowerShell 中执行下面的命令安装配置 oh-my-posh。

安装 posh-git 和 oh-my-posh 这两个模块，其中 posh-git 是 oh-my-posh 的依赖：

```powershell
Install-Module posh-git -Scope CurrentUser 
Install-Module oh-my-posh -Scope CurrentUser
```

[![install-onmyosh.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/install-onmyosh.png)](https://up.media.everdo.cn/image/hAoY)

安装过程如果遇到上述提示，不需要多考虑，直接选 Y 即可。如果遇到下述提示，不需要多考虑，直接选 A 即可。

[![install-onmyosh2.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/install-onmyosh2.png)](https://up.media.everdo.cn/image/hDNa)

现在，我们通过命令试一下能否正常切换到 ohmyposh 主题：

```powershell
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox
```

[![hxf-powershellsettheme.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/hxf-powershellsettheme.png)](https://up.media.everdo.cn/image/hVts)

可以看到，主题已经生效啦！！

但是这样设置的主题只能在当前 powershell 会话中生效，为了使之全局生效，我们需要修改用户自定义配置文件

```powershell
#用记事本打开配置文件
notepad $PROFILE
```

这里要做的，就是把上面的那些代码统统复制过来就好啦！

[![install-onmyoshuserprofile.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/install-onmyoshuserprofile.png)](https://up.media.everdo.cn/image/hbh3)

## 使用 PowerShell 7

微软官方在 GitHub 提供了 Powershell7 的下载。只要下载 msi 安装包，就可以很轻松的安装程序啦！

https://github.com/PowerShell/PowerShell/releases

[![download-powerhell.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/download-powerhell.png)](https://up.media.everdo.cn/image/hiuj)

安装不用多说，一路 Next。全新安装的 PowerShell7 会继承原先旧 PowerShell 的配色方案，但不会继承主题。

恢复的方法只要重新走一遍上面的过程就好啦！

最后看一下效果：

[![powershell7.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/powershell7.png)](https://up.media.everdo.cn/image/hQVO)

## 使用 WindowsTerminal

帅气的男孩子当然还得有点小肌肉才能撩到小姐姐哇（xiaogege），WindowsTermiinal 就像是一个多功能的瑞士军刀，能把多种命令行工具集合在一起，让本来单调的 powershell 在其加持下更加强大。

Terminal 的安装非常简单，只要在应用商店下载安装即可：

[![installwindowsterminal.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/installwindowsterminal.png)](https://up.media.everdo.cn/image/hey9)

刚刚安装完的 Terminal 打开后，会使用最原始的配色和字体，就像下面一样，会导致我们的自定义主题不正常显示。这里我们修改 Terminal 的配置文件。

[![terminalerr.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/terminalerr.png)](https://up.media.everdo.cn/image/hqs6)

（点击菜单栏的设置图标，系统会自动使用 VScode 打开一个配置的 json

[![terminalsettings.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/terminalsettings.png)](https://up.media.everdo.cn/image/hxKn)

这里可以先不管那么多，用我这里给大家的代码直接怼进去：

```json
"profiles":
    {
        "defaults":
        {
            // Put settings here that you want to apply to all profiles.
        },
        "list":
        [
            {
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "name": "Work PowerShell",
                "colorScheme" : "One Half Dark",
                "fontFace" : "等距更纱黑体 SC",
                "fontSize" : 11,
                "source": "Windows.Terminal.PowershellCore"
            },
            {
                // Make changes here to the powershell.exe profile.
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "name": "Windows PowerShell",
                "colorScheme" : "One Half Dark",
                "fontFace" : "等距更纱黑体 SC",
                "fontSize" : 11,
                "commandline": "powershell.exe",
                "hidden": false
            },
            {
                // Make changes here to the cmd.exe profile.
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "name": "命令提示符",
                "colorScheme" : "One Half Dark",
                "fontFace" : "等距更纱黑体 SC",
                "fontSize" : 11,
                "commandline": "cmd.exe",
                "hidden": false
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            }
        ]
    },
……
```

至此，我们在 Terminal 内可以同时使用经过美化的 Powershell5 和 Powershell7，还可以在快速调出 CMD 命令提示符。

[![terminalpowershell.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/terminalpowershell.png)](https://up.media.everdo.cn/image/h6oS)

### 在 Terminal 下使用 Git

到目前为止，Terminal 包含了两个版本的 PowerShell 以及老式的 CMD，已经比较强大了。但是我们仍然可以为他集成 Git 功能。

集成 Git 的首要条件就是电脑中预先安装了 Git。这里因为我电脑中已经有 Git，故不再演示。

启用 Git 只需要把下述代码添加到 Terminal 设置的配置文件中。

```json
{
    // GIT
    //"acrylicOpacity" : 0.75,
    "closeOnExit" : true,
    "colorScheme" : "One Half Dark",
    "commandline" : "D:\\Git\\bin\\bash.exe", // 改为 bash.exe，在环境变量里面配置了它之前的路径，用绝对路径也应该是可以的
    //"cursorColor" : "#FFFFFF",
    "cursorShape" : "bar",
    "fontFace" : "等距更纱黑体 SC",
    //"fontFace" : "Consolas",
    "fontSize" : 11,
    "guid" : "{0caa0dad-35be-5f56-a8ff-afceeeaa6109}", // 改一下 guid，此处我将最后一位改为9
    "historySize" : 9001,
    "icon" : "C:\\ProgramData\\Microsoft\\Windows\\Start Menu\\Programs\\Git\\gwindows_logo.png", // git-bash的logo地址
    "name" : "Git", // 改个名字
    "padding" : "5, 0, 0, 0",
    "snapOnInput" : true,
    "startingDirectory" : "%USERPROFILE%"
    //"useAcrylic" : true
},
```

然后，因为 Terminal 默认不集成图标，我们需要导入外部的 Git 图标到我们刚才配置文件中的图标路径：

```
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Git\gwindows_logo.png
```

[![import-git-icon.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/import-git-icon.png)](https://up.media.everdo.cn/image/hNkQ)

git 的图标可以点击下面的图另存为：

[![gwindows_logo.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/gwindows_logo.png)](https://up.media.everdo.cn/image/hkwJ)

现在我们来看下 Terminal 中能不能正常显示 Git 图标吧：

[![terminal-git.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/terminal-git.png)](https://up.media.everdo.cn/image/h9hy)

完美！

### Terminal 默认启动项

细心的朋友可能会发现，照我们刚才那样设置，Terminal 新启动的时候，会默认打开旧版的 PowerShell5，那么怎样设置我们想要的呢？比如 Git，CMD等等

想要完成这一步，其实只需要修改 Terminal 配置文件中的 defaultProfile

```
"defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
```

将这一栏的 uuid 改为我们需要启动的终端的 uuid 即可。

[![terminal-defaultprofile.png](https://media.everdo.cn/tank/pic-bed/2020/05/23/terminal-defaultprofile.png)](https://up.media.everdo.cn/image/hEQd)

> 好啦，到此为止，一个美美而强大的终端就打造完毕啦，看着这帅气的UI，撸代码的心情也会好很多哇！

![hxf-powershell](https://media.everdo.cn/tank/pic-bed/2020/05/23/hxf-powershell.png)


> 参考文章：https://sspai.com/post/52907