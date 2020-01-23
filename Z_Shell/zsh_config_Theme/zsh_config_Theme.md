---
noteId: "a32d96103dff11eab6b029848471ae9a"
tags: [zsh_config_theme]

---

# Z_Shell 主题的配置
这是一篇zsh主题配置的日志.   日期: 2020/1/24

## oh_my_zsh
主题的配置使用了zsh插件 *oh_my_zsh*，用curl安装：

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" 
```
curl的安装路径在 _Users/wangshijie/_下

安装完成可以看到提示：*oh my zsh is installed*， 并且Terminal的主题也已经换成了oh my zsh的默认主题“robbyrussel”

<div align=center> <img src="/Z_Shell/zsh_config_Theme/robbyrussel.png" width=50% /> </div>
<div align=center>
robbyrussel_Zhihu
</div>

## oh_my_zsh主题切换

oh_my_zsh带了很多不同的主题，可以在 [Themes of oh_my_zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes "Wiki_oh_my_zsh")中看到.

主题的切换通过配置 ~/.zshrc文件来进行.

```shell
vim ~/.zshrc #使用vim打开.zshrc文件
ZSH_THEME="avit" #在.zshrc中找到这一行，将“”内写入想要使用的主题
```
我使用的主题是avit，参考主题如下:
<div align=center> <img src="/Z_Shell/zsh_config_Theme/avit.png" width=80% /> </div>
<div align=center>
avit_github
</div>

注：使用agnoster主题要安装并使用Powerline字体，安装命令如下：

```shell
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```
## Customize
oh_my_zsh的各种主题可以自定义样式，下面以我对avit主题自定义的过程为例.
首先打开avit.zsh-theme文件，通过这个文件可以对avit主题自定义.
```shell
vim ~/.oh-my-zsh/themes/$ZSH_THEME.zsh-theme #注意路径和文件名称
```
### 显示日期和时间
首先要利用local指令创建一个字符串变量：
```shell
local DT="%{$fg[yellow]%}[`date "+%Y-%m-%d %H:%M:%S"`]%{$reset_color%}"
# fg[yellow]代表黄色字体，若要使用粗体字可用fg_bold[yellow]
# 中间的是日期格式
# 末尾的%{$reset_color%}我推测是用来结束字体颜色区间的
# “”内部可以自定义输出显示样式，包括中括号[]
```
然后在PROMPT中加入$DT：
```shell
ROMPT='
$DT$(_user_host)${_current_dir} $(git_prompt_info) $(_ruby_version)
%{$fg[$CARETCOLOR]%}▶%{$resetcolor%} '
# 这里每个$后面都是一类输出字符串
```

### 显示_user_host
注意到PROMPT中的$(_user_host)，默认设置中只在连接ssh时会显示user和host，我们希望能在任何时候都显示，所以需要修改_user_host的定义.
容易找到_user_host的定义是一个函数:

```shell
function _user_host() {
  if [[ -n $SSH_CONNECTION ]]; then
    me="%n@%m"                       # 如果是ssh连接，就显示username@host
  elif [[ $LOGNAME != $USER ]]; then
    me="%n@Macbookpro"                          # 如果不是$USER账户登陆，就显示username@Macbookpro
  fi
  if [[ $LOGNAME == $USER  ]]; then
    me="$USER@My-Macbookpro"         # 这一行是新加的，如果是$USER账户登陆，就显示$USER@My-Macbookpro
  fi
  if [[ -n $me ]]; then
    echo "%{$fg[cyan]%}[$me]:%{$reset_color%}" # 这里是函数的返回值，可以在这里自定义返回字符串显示的样式
  fi
}
```
利用这个例子可以学习一下shell中的函数设定，条件控制和echo返回等.

自定义后的最终样式如下：
<div align=center> <img src="/Z_Shell/zsh_config_Theme/Customized.png" width=100% /> </div>
<div align=center>
Final
</div>