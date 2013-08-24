# ubuntu下使用vim进行中文书写

## 输入法安装配置
1. 安装fcitx及google拼音输入法

        ``` Shell
        sudo apt-get install fcitx fcitx-config-common fcitx-googlepinyin
        ```
>此google输入法源自android版早期版本的移植版，与当下各版google拼音并非一个概念。

2. 扩充词库
下载搜狗输入法词库

        ``` Shell
        wget https://hslinuxextra.googlecode.com/files/fcitx-sougou-phrase-full.7z
        ```

运行需要安装fcitx-tools

        ``` Shell
        sudo apt-get install fcitx-tools
        ```
解压刚才的压缩包，执行

        ``` Shell
        ./run.sh
        ```

2. 安装云输入法

        ``` Shell
        sudo apt-get install fcitx-module-cloudpinyin
        ```
在fcitx-config里配置云输入模块，搜狗云似乎不管用，选择了百度云输入法，这里不会自动应用，注销用户重新登录可生效。

3. 备注：使用最新版fcitx - 慎用  
添加fcitx源

        
        ``` Shell
        sudo add-apt-repository ppa:fcitx-team/nightly
        sudo apt-get update
        ```
执行1到3步；  
这时fcitx是起不来的，需要手动更新fcitx-module-x11, fcitx-table, fcitx-module-dbus, 可以通过 `fcitx` 验证是否配置成功；  
新版的最大问题是开机启动无法进行，dbus-daemon报bad file descriptor，可能是与unity桌面的兼容性问题，简单查询无果。添加命令到rc.local中无用，最后在~/.xprofile中写
      
        ``` Shell
        export XMODIFIERS=@im=fcitx
        export QT_IM_MODULE=xim
        export GTK_IM_MODULE=xim
        fcitx -d
        ```
算是解决了这个问题；  
另最新版似乎可以配置皮肤，但config一直不正常从未成功，待进一步配置。

## 安装vim插件
1. 安装fcitx.vim，此插件可以在退回normal模式时自动切为英文输入法。地址 https://github.com/vim-scripts/fcitx.vim

2. 安装PinyinSearch，方便进行中文搜索。地址 https://github.com/ppwwyyxx/vim-PinyinSearch，~/.vimrc中配置如下：

        ``` VimL
        let g:PinyinSearch_Dict = $HOME . '/.vim/bundle/vim-PinyinSearch/PinyinSearch.dict'
        noremap ? :call PinyinSearch()<CR>
        noremap <leader>n :call PinyinNext()<CR>
        ```

此后可以用`?`加上词的首字母拼音来搜索中文词，如az可以搜索“安装”，之后可按惯常搜索用`n`跳到下一个词；也可用`/`进行正常搜索，回车后用<leader>用当前搜索词作为中文词首字母，激发中文搜索。此外推荐在~/.vimrc中添加`set hlsearch`以高亮选中词。
