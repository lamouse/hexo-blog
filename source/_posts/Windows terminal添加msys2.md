1. 打开Windows terminal 添加新的配置文件
1. 新建空配置文件
1. 在命令行中选择msys2的安装目录中的msys2_shell.cmd
1. 确认之后在后面添加 
```-defterm -no-start -use-full-path -here -mingw64```
1. 添加完成之后打开的msys2就会在当前目录打开了
1. 如果msys2想使用zsh那么修改msys2_shell.cmd中的
```set "LOGINSHELL=zsh"```
1. 为了解决utf-8乱码问题需要在.zshrc（或者其他sh中的配置文件）中添加chcp.com 65001