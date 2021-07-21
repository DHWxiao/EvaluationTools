# EvaluationTools
等级保护测评工具

声明: 工具仅供安全研究，不建议在正式测评环境中使用，非法用途后果自负。

使用说明：

1、Windows 本地自检
	1)管理员权限打开 cmder.exe
	2)切换至脚本所在目录
	3)执行 EvaluationTools_windows.exe windows

2、Windows 检查远程 Linux 服务器 (允许root用户远程登录)
	1)管理员权限打开 cmder.exe
	2)切换至脚本所在目录
	3)执行 
	EvaluationTools_windows.exe linux --ip x.x.x.x(远程服务器IP地址) --user root --pass x(root用户密码) --linuxRelease Centos（Linux发行版）

3、Windows 检查远程 Linux 服务器 (不允许root用户远程登录)
	1)管理员权限打开 cmder.exe
	2)切换至脚本所在目录
	3)执行
	EvaluationTools_windows.exe linux --ip x.x.x.x(远程服务器IP地址) --user xx(普通用户) --pass x(普通用户密码) --linuxRelease Centos（Linux发行版） --superPassword xx(root 用户密码)

4、Linux 本地自检
	1)切换至脚本所在目录
	2)添加脚本可执行权限 chmod +x EvaluationTools_linux.sh
	3)执行
	./EvaluationTools_linux.sh linux --ip 127.0.0.1 --linuxRelease Centos(linux 发行版)
	
5、Linux 检查远程 Linux 服务器 (同 Windows，仅更换可执行文件名即可)

注意事项：项目文件均有中药作用，切勿修改名字或移动其名字，否则程序不能正常使用。
