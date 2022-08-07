---
title:   vscode中git失效的问题(window环境)
---
### 背景是vscode(版本是1.67)中的git找不到了，查阅资料得出以下解决方法
1.在vscode中找到setting.json文件

2.在文件中输入terminal.integrated.profiles.windows,会自动给出配置属性

3.默认上Git Bash，改为GitBash，或者Git-Bash

4.在GitBash中配置path，打开git bash，输入 where bash，将路径复制过去，记得要用\转义，将args配置为空

5.一开始我以为到第四步就结束了,当我重新打开vscode， 在终端输入git的时候发现报git not commend，查阅后得到需要配置git.enabled，和git.path，配置完成后重新打开vscode即可

6.最终配置如下所示：

```
"terminal.integrated.profiles.windows":{ 
"PowerShell":{
 "source": "PowerShell", 
 "icon":"terminal-powershell" 
"Command Prompt": {
 "path":[ 
“${env:windir}llSysnativellcmd.exe",I
 "${env:windir}1lsystem32\\cmd.exe" 
"args":[], 
 "icon":"terminal-cmd" 
 "GitBash":{ 
 "path":["c:\\tools\\git\\usr\\bin\\bash.exe"], 
 "args": [] }

 "git.enabled":true, 
 "git.path": "c:\\tools\\git\\mingw64\\bin\lgit.exe", 
 "terminal.integrated.defaultProfile.windows":"GitBash",
```

7.注意点。GitBash中的path是git bash路径，git.path中的配置是git的路径