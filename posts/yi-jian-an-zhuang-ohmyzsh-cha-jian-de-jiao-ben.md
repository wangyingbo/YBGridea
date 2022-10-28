---
title: '一键安装ohmyzsh常用插件的脚本'
date: 2021-11-29 14:02:45
tags: [Linux,shell]
published: true
hideInList: false
feature: /post-images/yi-jian-an-zhuang-ohmyzsh-cha-jian-de-jiao-ben.png
isTop: false
---
## 功能

脚本实现了下载安装`ohmyzsh`的常用插件功能，并替换`~/.zshrc`文件的plugins字段配置；
安装的plugins分别为：

- `zsh-autosuggestions`：[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) 此插件实现了自动补全语法功能，会自动缓存敲过一次的终端命令，并且在下次输入同样命令的前几个字符时，联想出命令；

![](https://hiwyb.github.io/post-images/1638166049959.png)

- `zsh-syntax-highlighting`：[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) 此插件可以自动分析输入的Linux 及常用命令是否正确；

![](https://hiwyb.github.io/post-images/1638167911169.gif)

- `z`：[z](https://github.com/rupa/z) 此插件实现了自动跳转目录功能，插件会以哈希表的形式自动记录你访问过的路径，在下次访问时，直接输入文件目录的最后一级，按`tab`即可联想出；

![](https://hiwyb.github.io/post-images/1638166661179.gif)

## 使用

使用前本地需安装 [ohmyzsh](https://github.com/ohmyzsh/ohmyzsh) ，因GitHub国内访问环境不稳定，因此通过gitee 镜像安装；
```
sh -c "$(curl -fsSL https://gitee.com/xrxiao/ohmyzsh/raw/master/tools/install.sh)"
```

使用`upgrade_oh_my_zsh`命令可以手动更新升级ohmyzsh。

使用以下脚本自动安装`ohmyzsh`的常用plugins。脚本自动检测本地是否安装`ohmyzsh`，如果没安装过，会直接退出；

```
#! /bin/bash
# author: wangyingbo
# date: 2021-11-26 13:00

# zshrc文件路径
file_zshrc=~/.zshrc;

echo -e "\n"

files=$(ls ~/.oh-my-zsh 2> /dev/null | wc -l) # 判断目录下是否存在已知后缀名文件
if [ $files -ne 0 ] ; then 
	echo -e "\033[32;40m congratulations, the terminal has oh-my-zsh! \033[0m"
else
	echo -e "\033[31;40m warning: no oh-my-zsh，please install oh-my-zsh first!!! \033[0m"
	exit 1
fi

echo -e "\n"
echo -e "\033[33;40m will begin install oh-my-zsh plugins，please wait a minute \033[0m"
echo -e "\n"

# z is exist:方法不可用
isExistZ() {
	para=0
	file=`command -v _z | grep "_z"`
	echo $file
	if [[ $file =~ "_z" ]] ; then
		para=1
	else
		echo ""
	fi
	return $para
}

# isExistZ
# resZ=`echo $?`
# echo $resZ
# if [[ $resZ -eq 1 ]]; then
# 	echo -e "\033[32;40m have installed the plugin z \033[0m"
# else
# 	echo -e "\033[33;40m will begin install plugin z \033[0m"
# fi


newPlugins=""
# 安装 plugin z
if [[ -d ~/.oh-my-zsh/custom/plugins/z ]]; then
	echo -e "\033[32;40m have installed the plugin z \033[0m"
	echo -e "\n"
else	
	echo -e "\033[33;40m will begin install plugin z \033[0m"
	echo -e "\n"
	git clone https://github.com/rupa/z.git $ZSH_CUSTOM/plugins/z
	newPlugins+=" z"
	echo -e "\033[32;40m have installed the plugin z \033[0m"
fi
if [[ ! -d ~/.oh-my-zsh/custom/plugins/z ]]; then
	echo -e "\033[31;40m error:install plugin zerror! \033[0m"
	exit 1
fi

# 安装 plugin zsh-autosuggestions
if [[ -d ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions ]]; then
	echo -e "\033[32;40m have installed the plugin zsh-autosuggestions \033[0m"
	echo -e "\n"
else	
	echo -e "\033[33;40m will begin install plugin zsh-autosuggestions \033[0m"
	echo -e "\n"
	git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
	newPlugins+=" zsh-autosuggestions"
	echo -e "\033[32;40m have installed the plugin zsh-autosuggestions \033[0m"
fi
if [[ ! -d ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions ]]; then
	echo -e "\033[31;40m error:install plugin zsh-autosuggestionserror! \033[0m"
	exit 1
fi

# 安装 zsh-syntax-highlighting
if [[ -d ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting ]]; then
	echo -e "\033[32;40m have installed the plugin zsh-syntax-highlighting \033[0m"
	echo -e "\n"
else	
	echo -e "\033[33;40m will begin install plugin zsh-syntax-highlighting \033[0m"
	echo -e "\n"
	git clone git://github.com/zsh-users/zsh-syntax-highlighting $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
	newPlugins+=" zsh-syntax-highlighting"
	echo -e "\033[32;40m have installed the plugin zsh-syntax-highlighting \033[0m"
fi
if [[ ! -d ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting ]]; then
	echo -e "\033[31;40m error:install plugin zsh-syntax-highlightingerror! \033[0m"
	exit 1
fi

# 匹配以plugin开头，以)结尾的字符串
plugins=`grep "^plugin.*)$" $file_zshrc`
echo "current plugins: $plugins"
echo -e "\n"

# newPlugins+=" z"
# newPlugins+=" zsh-autosuggestions"
# newPlugins+=" zsh-syntax-highlighting"
echo "new plugins：$newPlugins"
echo -e "\n"

# 获取已有的plugin的长度
oriLength=${#plugins}
# echo "原来plugins字符串长度是：$oriLength"
# echo -e "\n"
replaceIndex=$oriLength-1

# 合并为新的plugins
replacePlugins=${plugins:0:$replaceIndex}$newPlugins${plugins:$replaceIndex}
echo "merged plugins：$replacePlugins"
echo -e "\n"

# 将某个文件中的字符串替换为新字符串 mac环境和linux环境 sed -i 使用不同
# Mac使用：https://www.cnblogs.com/chunzhulovefeiyue/p/6561497.html
# Linux使用：https://www.cnblogs.com/A121/p/10621152.html

# eg:把文件中的jack替换成tom，并给源文件添加.backup后缀并备份；添加/g是全部替换，默认每行只替换一次。
# sed -i ".backup" 's/jack/tom/g' $file_zshrc

sed -i ".backup" "s/$plugins/$replacePlugins/" $file_zshrc

totalPlugins=`grep "^plugin.*)$" $file_zshrc`
echo "total end plugin: $totalPlugins"
echo -e "\n"

# 更新 .zshrc 文件
source $file_zshrc

# 输出脚本执行用时
echo -e "\n"
echo -e "\033[32;40m this shell script execution duration(脚本执行时长): ${SECONDS}s  \033[0m"

```