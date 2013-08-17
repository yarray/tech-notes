# ubuntu下使用vim进行中文书写

## 输入法安装配置
1. 安装fcitx及google拼音输入法

        sudo apt-get install fcitx fcitx-config-common fcitx-googlepinyin
>此google输入法源自android版早期版本的移植版，与当下各版google拼音并非一个概念。

2. 扩充词库
下载搜狗输入法词库

        wget https://hslinuxextra.googlecode.com/files/fcitx-sougou-phrase-full.7z
运行需要安装fcitx-tools

        sudo apt-get install fcitx-tools
解压刚才的压缩包，执行

        ./run.sh

2. 安装云输入法

        sudo apt-get install fcitx-module-cloudpinyin
在fcitx-config里配置云输入模块，搜狗云似乎不管用，选择了百度云输入法，这里不会自动应用，注销用户重新登录可生效。

4. 备注：使用最新版fcitx - 慎用  
添加fcitx源

        sudo add-apt-repository ppa:fcitx-team/nightly
        
        sudo apt-get update
执行1到3步；  
这时fcitx是起不来的，需要手动更新fcitx-module-x11, fcitx-table, fcitx-module-dbus, 可以通过 `fcitx` 验证是否配置成功；  
新版的最大问题是开机启动无法进行，dbus-daemon报bad file descriptor，可能是与unity桌面的兼容性问题，简单查询无果。添加命令到rc.local中无用，最后在~/.xprofile中写
      
        export XMODIFIERS=@im=fcitx
        export QT_IM_MODULE=xim
        export GTK_IM_MODULE=xim
        fcitx -d
算是解决了这个问题；  
另最新版似乎可以配置皮肤，但config一直不正常从未成功，待进一步配置。
