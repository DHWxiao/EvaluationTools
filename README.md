# 网络安全等级保护测评辅助系统

### 免责声明
工具仅供安全研究，不建议在正式测评环境中使用，非法用途后果自负



#### 介绍

1.  将网络安全等级保护测评工作中一些繁琐的功能进行了自动化实现

2.  主机等级保护合规性检查（支持以下操作系统版本）
    - 通过 ssh 连接对 linux 系统进行检查（支持远程、本地检查），支持以下操作系统版本：
        - Ubuntu 16/18/20、Centos 6/7/8、RedHat 6/7/8、中标麒麟 5/6/7
    - 通过 Powershell 对 Windows 系统进行检查（仅支持本地检查），支持以下操作系统版本：
        - Windows 7/8/10 、Windows Server 2008/2012/2016 R2
    - 若有需要支撑的操作系统，可以提供测评所需的作业指导书用以添加

3.  差距分析
    - 现场测评阶段使用，可以根据不同的测评对象生成作业指导书（默认已添加一部分），内置结果记录、问题描述、整改建议模版
    - 根据实际测评结果生成现场测评记录表、差距分析报告，可联动高风险判定模块，关联每一个测评指标，在测评过程中不遗漏掉任意一个高风险

4.  高风险判定
    - 将《网络安全等级保护测评高风险判定指引》中的相关标准进行整理，可快速浏览标准，能够及时找到相关内容

5.  过程文档
    - 将测评所需签署的一些文档进行快速填写、打印，每家测评机构使用的模版不同，若有需要，请提供模版文件进行添加

6.  自定义作业指导书
    - 联动差距分析模块，可以根据模版文件将作业指导书填写后，在差距分析模块中生成相对应测评对象的作业指导书，方便现场测评使用（若添加了
    - 非安全计算环境的作业指导书，系统会自动将自定义的作业指导书覆盖默认自带的作业指导书，若需还原系统默认作业指导书，将  **/userDefine**  下相应文件删除即可）

7.  数据库项目导入
    - 联动主机等级保护合规性检查，在执行完合规性检查后，在软件执行目录下会生成 db.sqlite3 文件，文件中仅能记录上一次检查结果记录。
    - 使用场景：
        - Linux 系统环境下执行本地、远程检查，无法自动跳转至 HTML 结果页面，需导出路径下 db.sqlite3 文件至 Windows 系统上，在 Windows 上可通过命令行或GUI版本进行导入 db.sqlite3 文件即可自动跳转至 HTML 结果页面。
        - Windows 系统环境下执行命令行版本检查，默认不会自动跳转至 HTML 结果页面，需手动执行数据库项目导入功能模块进行跳转HTML 结果页面主要面向的是测评人员，所以最初设计的时候，在被测系统上执行合规性检查是不会自动启用 HTML 生成模块的

#### 软件架构

1.  开发语言：Go、Shell、Html、Powershell
2.  GUI框架：fyne
3.  数据库：Sqlite3

#### 安装教程

1.  无需安装，将程序下载至本地后可直接使用

#### 使用说明
    
    
1.  EvaluationTools_winGui_version.exe
    - 视频演示：[EvaluationTools_winGui 在线完整演示视频](https://www.bilibili.com/video/BV1JU4y1m7Br/)
    - 版本介绍：桌面版本
    - 适用场景：现场测评、差距分析阶段
    - 使用环境：Windows 7/8/10 等非 Server/虚拟机 版本的 Windows 系统
    - 注意事项：
        - 在现场测评阶段中，可以使用 GUI 版本中的差距分析模块进行记录填写，在完成现场记录的同时，系统将会生成相应的现场记录表、差距分析报告
        - 当完成主机操作系统合规性检查后，可以将对应生成的 .sqlite3 文件拷贝至测评主机上，在测评主机上执行 GUI 版本，通过数据库导入功能模块生成 HTML 结果页，可查看、下载生成的现场记录表以及差距分析报告。
        - GUI 版本可以执行 Linux 远程合规性检查与 Windows 本地自检，若被测系统是 Windows 系统，建议使用 cmd 版本。
        - WinGui 版本合规性检查会生成 HTML 结果页面，所以需要确保项目路径下有 tempate 项目文件夹
![image](https://github.com/user-attachments/assets/f1e4ee02-7881-49d3-bf1e-f77cb2eead90)

    
    
   
2.  EvaluationTools_winCmd_version.exe
    - 视频演示：[EvaluationTools_winCMd 在线完整演示视频](https://www.bilibili.com/video/BV19Y4y147KC)
    - 版本介绍：Windows 命令行版本
    - 适用场景：现场测评
    - 使用环境：Windows 7/8/10/11 、Windows Server 2008/2012/2016
    - 命令解析
        - linux
            - 执行 linux 远程合规性检查任务
            - --help 查看 linux 命令子命令说明
                - 例子:   ` EvaluationTools_winCmd_version.exe linux --help `
            - --ip, -i ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤ目标系统 ip 地址
            - --user, -u ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤ目标系统用户名（非 root 用户需结合 --superPassword root密码  使用）
            - --pass, -p ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤ目标系统用户名对应密码
            - --port ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤㅤ目标系统 ssh 协议对应端口，默认为 22
            - --dir ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤㅤ 项目结果文件保存地址，默认为当前程序所在路径
            - --level ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤ 目标系统网络安全保护等级保护等级，默认为三级
            - --linuxRelease, --release ㅤ   目标 linux 系统发型版本，如：Centos_7
            - --superPassword ㅤㅤㅤㅤㅤ ㅤ   目标系统超级管理员 root 密码（解决 root 用户不能远程登录）
            - 例子:   ` EvaluationTools_winCmd_version.exe linux --ip 192.168.1.1 --user root --pass 123456 --release  Centos_7 ` (部分版本不支持普通用户远程开展合规性检测，以实际为准)
    
        - windows
            - 执行 Windows 本地合规性检查任务
            - 例子:   ` EvaluationTools_winCmd_version.exe windows `
        - dataBase
            - 执行数据库项目导入
            -   --dbFile ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤ 数据库文件路径地址，默认在项目根目录下./db.sqlite3
            - 例子:   ` EvaluationTools_winCmd_version.exe dataBase db.sqlite3 `     
        - help
            - 查看帮助说明
            - 例子:   ` EvaluationTools_winCmd_version.exe help `
    - 注意事项：
        - 命令行版本主要用于对 Windows 系列操作系统进行合规性检查
![image](https://github.com/user-attachments/assets/fab6709e-4b65-47ab-9c46-53faa37d3a76)




3.  EvaluationTools_linuxCmd_version.exe
    - 视频演示：[EvaluationTools_linuxCMd 在线完整演示视频](https://www.bilibili.com/video/BV13v4y1N7dM)
    - 版本介绍：Linux 命令行版本
    - 适用场景：现场测评
    - 使用环境：Ubuntu 16/18/20、Centos 6/7/8、RedHat 6/7/8、中标麒麟 5/6/7
    - 命令解析
        - linux
            - 执行 linux 远程合规性检查任务
            - --help 查看 linux 命令子命令说明
                - 例子:   ` EvaluationTools_winCmd_version.sh linux --help `
            - --ip, -i ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤ目标系统 ip 地址
            - --user, -u ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤ目标系统用户名（非 root 用户需结合 --superPassword root密码  使用）
            - --pass, -p ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤ目标系统用户名对应密码
            - --port ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤㅤ目标系统 ssh 协议对应端口，默认为 22
            - --dir ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤㅤ 项目结果文件保存地址，默认为当前程序所在路径
            - --level ㅤㅤㅤㅤㅤ ㅤ   ㅤㅤㅤㅤ 目标系统网络安全保护等级保护等级，默认为三级
            - --linuxRelease, --release ㅤ   目标 linux 系统发型版本，如：Centos_7
            - --superPassword ㅤㅤㅤㅤㅤ ㅤ  目标系统超级管理员 root 密码（解决 root 用户不能远程登录）
            - 例子：` 远程检查 EvaluationTools_winCmd_version.sh linux --ip 192.168.1.1 --user root --pass 123456 --release  Centos_7 ` (部分版本不支持普通用户远程开展合规性检测，以实际为准)
            - 例子：` 本地自检 EvaluationTools_winCmd_version.sh linux --ip 127.0.0.1 --release  Centos_7 （需 root 用户执行）`
        - windows
            - linux 上不能执行 windows 合规性检查任务
        - help
            - 查看帮助说明
            - 例子:   ` EvaluationTools_winCmd_version.sh help `
    - 注意事项：
        - 命令行版本主要用于对 Linux 系列操作系统进行合规性检查
![image](https://github.com/user-attachments/assets/24e1b1d1-4dcb-4494-b001-0b574250a00a)


#### 备注
使用之前，请根据发布版本自行校验文件 Hash 值，确保文件完整性未受到破坏

1. 为了工具不被滥用，系统使用需导入专业授权文件，授权申请过程：
    - 双击 EvaluationTools_winGui_version.exe （确保同目录下有下载自带的 EvaluationTools-license.lic 文件）
    - 软件路径下会生成	EvaluationTools-license.lic.txt 授权申请码
    - 添加微信:xhuSoul 
    - 将 EvaluationTools-license.lic.txt 文件中的授权申请码通过 VX 发送给作者进行授权申请
    - ![image](https://github.com/user-attachments/assets/6e36610a-dfbc-4ad1-9f83-3076b5713c5b)

