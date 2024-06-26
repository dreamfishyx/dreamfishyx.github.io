---
title: windows和wsl美化
date: 2024-04-07 21:40:14
tags: 
  - linux
  - window
  - wsl
description: 关于windows中wsl的美化设置。
categories: 梦鱼的笔记
---

#### windows terminal

>   1.   `CTRL+SHIFT+,`打开配置文件。
>
>   2.   终端专注模式：
>
>        1.   `CTRL+SHIFT+P`打开搜索切换专注模式(退出也是这种方式)。
>
>        2.   cmd输入`wt/f`也可进入专注模式(`win+R`也行)。
>
>        3.   直接在设置中为切换专注模式设置一个快捷键，例如`ALT+Z`即可。<br><img src="/assets/image-20230804224101642.png" alt="image-20230804224101642"/>
>
>   

---



##### powershell

1.   安装`oh-my-posh`，实际详细配置参考[官网](https://ohmyposh.dev/docs/installation/windows)。下面命令均使用管理员权限下的`powershell`运行。

1.   `winget install JanDeDobbeleer.OhMyPosh -s winget --location xxx ` 安装`oh-my-posh`到指定位置。当然你也可以使用命令`winget upgrade JanDeDobbeleer.OhMyPosh -s winget --location xxx`更新。

1.   配置`oh-my-posh`环境。<br><img src="/assets/image-20230802210927729.png" alt="image-20230802210927729"  />

1.   安装推荐字体进入[Nerd Fonts](https://www.nerdfonts.com/)随便下载一款字体（但个人推荐`FiraCode Nerd Font`，`Caskaydia Cove Nerd Font`也还行），并在windows上安装。

1.   终端下使用 `CTRL + SHIFT + ,`打开配置文件，配置全局字体。当然也可以直接在 `windows terminal`设置中配置字体。(更推荐`FiraCode Nerd Font`)。<br><img src="/assets/image-20230523103456652.png" alt="image-20230523103456652" />

     

1.   此外建议在`设置->呈现中`开启`windows terminal`文本呈现器。此外在`设置->外观`中开启亚力克材料效果。在各个配置文件的`外观->透明度`中启用亚力克材料。<br><img src="/assets/image-20230522230645017.png" alt="image-20230522230645017"  /><br><img src="/assets/image-20240407214316980.png" alt="image-20230523115429689"  />

1.   powershell运行`get-Poshthemes`查看所有主题。

1.   powershell运行`notepad $profile`编辑powershell配置文件。其中`--config`后面接主题配置的文件位置(全部在`oh-my-posh`安装目录的`themes`目录下)。(`night-owl、neko、montys`不错)

     ```json
     oh-my-posh --init --shell pwsh --config D:\Environment\ohmyposh\themes\neko.omp.json | Invoke-Expression
     ```

     <br><img src="/assets/image-20230522223158710.png" alt="image-20230522223158710" />

1.   运行`. $profile`使配置生效。

1.   使用如下命令，下载美化终端的图标。<br>

     ```shell
     Install-Module -Name Terminal-Icons -Repository PSGallery
     ```

1.   `notepad $profile`编辑powershell配置文件。

     ```shell
     Import-Module -Name Terminal-Icons
     oh-my-posh --init --shell pwsh --config D:\Environment\ohmyposh\themes\atomic.omp.json | Invoke-Expression
     ```

1.   运行`. $profile`使配置生效。

1.   强调一下window终端下的一个配置，开启自动调整无法区分的文本的亮度可能会导致某些主题无法正常显示：<br><img src="/assets/image-20230708173601210.png" alt="image-20230708173601210"  />

     

---



##### cmd美化

1.   下载[clink](https://github.com/chrisant996/clink/releases)工具，安装一个已知位置。

2.   然后，进入clink安装目录，创建`oh-my-posh.lua`文件，添加如下内容：

     ```shell
     load(io.popen('oh-my-posh init cmd'):read("*a"))()
     ```

3.   ​	或者使用指定主题：

     ```shell
     load(io.popen('oh-my-posh init cmd --config D:\\Environment\\ohmyposh\\themes\\atomic.omp.json'):read("*a"))()
     ```



---



##### 配色

1.   自定义配色很繁琐，而且很好费时间，最好的方法是用别人做好的配色。可以在github项目 [iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes))里找，有两百多方案，先在 Screenshots 里挑选好颜色，然后到 `windwosterminal` 目录对应的 json 文件复制样式。<br><img src="/assets/image-20230802205915724.png" alt="image-20230802205915724"  />

2.   将样式粘贴到windwos terminal配置文件的`schemes`数组中即可。

     ```json
     "schemes": 
     [
         {
             "background": "#F7F7F7",
             "black": "#090300",
             "blue": "#01A0E4",
             "brightBlack": "#5C5855",
             "brightBlue": "#807D7C",
             "brightCyan": "#CDAB53",
             "brightGreen": "#3A3432",
             "brightPurple": "#D6D5D4",
             "brightRed": "#E8BBD0",
             "brightWhite": "#F7F7F7",
             "brightYellow": "#4A4543",
             "cursorColor": "#4A4543",
             "cyan": "#B5E4F4",
             "foreground": "#4A4543",
             "green": "#01A252",
             "name": "3024 Day",  //配色方案名称
             "purple": "#A16A94",
             "red": "#DB2D20",
             "selectionBackground": "#A5A2A2",
             "white": "#A5A2A2",
             "yellow": "#FDED02"
         },
     ]
     ```

3.   之后通过`name`在windwosterminal设置中使用即可。

4.   其他[配色网站](https://windowsterminalthemes.dev/)。



---



##### 隐藏启动信息

1.   windwosterminal打开powershell时，会有显示一些版本和加载信息。

2.   我们可以通过设置，对每个配置文件的的命令行配置中添加`-nologo`参数即可。

     ```text
     gsudo.exe %SystemRoot%\System32\cmd.exe -nologo
     ```

     <br><img src="/assets/image-20230523114847261.png" alt="image-20230523114847261"  />



---



##### gsudo

1.    安装 gsudo 只需要一条 Powershell 指令就行:

      ```shell
      PowerShell -Command "Set-ExecutionPolicy RemoteSigned -scope Process; iwr -useb https://raw.githubusercontent.com/gerardog/gsudo/master/installgsudo.ps1 | iex"
      ```

1.   安装过程中会问你是否要使用 `sudo`作为 `gsudo`的别名，我这里选择是。安装完后重启，环境变量生效后就可以使用 `sudo`来快速跳转到管理员级别的 Powershell 了。



---



#### ubuntu子系统(wsl)

##### zsh和oh-my-zsh

1.   运行`apt-get install zsh`安装`zsh`。并用`zsh --version`检查是否安装成功 。

2.   运行`sudo vim /etc/passwd`将`zsh`设为当前用户默认。或者使用`chsh -s $(which zsh)`命令将当前用户的shell修改为`zsh`。注意只需添加当前用户即可。

     ```text
     fish:x:1001:1001::/home/fish:/bin/zsh  
     ```

3.   安装`oh-my-zsh`，三种方式：

     ```shell
     # curl
     sudo apt install curl 
     sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     
     # wget
     sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     
     # fetch
     sh -c "$(fetch -o - https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     
     # 前几种不行,就手动安装(这里注意文件夹是oh-my-zsh,没有.)(建议使用国内镜像)
     git clone https://github.com/robbyrussell/oh-my-zsh	# 下载源码
     cd ~/oh-my-zsh/tools	# 执行安装命令
     sh install.sh	# 安装
     ls -a ~   # 查看.oh-my-zsh/目录
     
     uninstall_oh_my_zsh #卸载
     ```

4.   安装目录是`~/.oh-my-zsh/themes/`，可以使用`ls` 命令查看主题(`~`表示当前用户目录)。

5.   `vim ~/.zshrc `编辑文件设置喜欢的主题，其实就是修改` ZSH_THEME`，过程如下：

     ```shell
     ls ~/.oh-my-zsh/themes
     vim ~/.zshrc # 设置 ZSH_THEME="cloud" 
     ```

6.   运行`source ~/.zshrc`重新加载配置文件。

7.   当然你也可以在[官网](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)查看不同主题。

8.   由于 oh-my-zsh下主题的表现没有oh-my-posh的表现好，我决定装一个powerlevel10k，这款主题也是非常得受欢迎。`git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k`

9.   装完后使用 `vim ~/.zshrc`配置好 `ZSH_THEME="powerlevel10k/powerlevel10k"`

10.   重启终端你就可以看到配置界面(没有看到也可以使用 `p10k configure`指令手动调出)。其他一些命令：

      ```shell
      # 列出主题中包含的所有图标的名称
      get_icon_names
      
      # 禁用P9k/P10k
      prompt_powerlevel9k_teardown
      
      # 启用P9k/P10k
      prompt_powerlevel9k_setup
      
      # 配置p10k
      p10k configure
      ```

11.   `zsh`自带了很多的插件，相关的文件都放在了`~/.oh-my-zsh/plugins`目录中。默认使用Git插件，能提供 Git状态颜色编码和提示符。要想使用其他自带的插件，只需要编辑`~/.zshrc`文件，添加插件名称即可。

12.   安装几个插件：

      ```shell
      # ubuntu安装git
      sudo apt update
      sudo apt install git
      
      # zsh-syntax-highlighting:终端命令语法高亮
      git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.oh-my-zsh/plugins/zsh-syntax-highlighting
      
      
      # zsh-autosuggestions:自动补全
      git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/plugins/zsh-autosuggestions
      
      ```

13.   `vim ~/.zshrc`编辑文件，添加插件：

      ```text
      plugins=(
      ...  # 之前已经声明的插件名称
      zsh-autosuggestions
      zsh-syntax-highlighting
      )
      ```

14.   运行`source ~/.zshrc`重新加载配置文件。

15.   提一下，上述配置只对当前用户生效，文件都在用户目录下。

>   1.   似乎使用`zsh`在配置环境变量方面有些不同，后续待补。
>   2.   可参考`https://zhuanlan.zhihu.com/p/166103184`。



---



##### oh-my-posh

1.   说实话`oh-my-zsh`太丑了。我发现`wsl`也是可以安装`oh-my-posh`的。

2.   先运行`sudo vim /etc/passwd`编辑文件，将用户的shell修改回为`bash`

3.    安装`oh-my-posh`(更新就重新下载，覆原文件夹)。

      ```shell
      sudo wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
      sudo chmod +x /usr/local/bin/oh-my-posh
      ```

4.    下载主题：

      ```shell
      mkdir ~/.poshthemes
      wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O ~/.poshthemes/themes.zip
      unzip ~/.poshthemes/themes.zip -d ~/.poshthemes
      chmod u+rw ~/.poshthemes/*.omp.*
      rm ~/.poshthemes/themes.zip
      ```

5.   可以在`bash`的配置文件(`~/.bashrc`或 `~/.profile` 或`~/.bash_profile`)中配置一下，在最后一行加入喜欢的主题：

     ```shell
     eval "$(oh-my-posh --init --shell bash --config ~/.poshthemes/catppuccin_macchiato.omp.json)"
     ```

6.   运行`bash`生效(有的是运行`. ~/.profile `)。

7.   其他详细内容参考[官方文档](https://ohmyposh.dev/docs/installation/prompt)。



---



#### window美化

##### 鼠标样式

1.   去[github下载](https://github.com/PSGitHubUser1/Windows-11-Cursor-Concept-Pro-v2.x)对应的鼠标样式。
2.   解压，选择喜欢的鼠标样式，右键`.inf`文件安装鼠标样式。

---



##### mybockfinder

1.   去`steam`安装`mybockfinder`，按照自己的喜好设置即可。
2.   为了保证开机自启，相关设置选择`服务`选项。

---



##### 雨滴插件

1.   [官网安装](https://www.rainmeter.net/)。
2.   下载安装主题即可，推荐[致美化](https://zhutix.com/tag/rainmeter/)。

---



##### Wallpaper Engine

1.  去`steam`安装壁纸引擎(Wallpaper Engine,收费)，按照自己的喜好设置壁纸。
2.  设置为开机自启。
