# mac系统出现软件损坏/无法验证开发者

### 首先在安全与隐私中，允许从【任何来源】下载的app

如果这个页面没有 任何来源 这个选项，采用下列方法：
* 打开「终端」：应用程序->实用工具->终端；
* 复制粘贴下面的命令后，按回车，输入你的系统密码（注意密码不会显示，直接输入后回车就行）；<br>
sudo spctl --master-disable （注意master前面是两个 - -）
* 再次打开安全设置选项，就会发现「任何来源」选项出来了！

如图：![](https://github.com/oldhand/images/raw/master/others/macOpenAnySource.png)
	
	
### 如果前面两步仍有问题，请打开终端， 
在终端中粘贴下面命令：sudo xattr -r -d com.apple.quarantine,然后输入个空格，再将应用程序目录中的软件拖拽到命令后面(命令行会自动插入路径)，按回车后输入密码执行。<br>
如果是MindNode的命令对应就是 sudo xattr -r -d com.apple.quarantine /Applications/MindNode.app/<br>
