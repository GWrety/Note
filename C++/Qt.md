# Qt打包问题
1. 首先将release版本的exe单独放到一个文件夹中
2. 然后从开始菜单打开 Qt 命令行(区分qtcreater和vs)，输入命令 
	- cd /d 目标文件夹
	- 然后使用 windeployqt 工具命令：windeployqt 目标exe
3. 在加载完成后，使用virtual box封装：
    1. 添加附加文件时选按递归方式添加，同时删除文件夹中的exe
	2.  同时在文件选项中压缩文件
	3. 点击执行，完成封包。
# VS+Qt配置问题：
1. 解决在vs中新建qt工程，无法打开qt 设计师界面的问题：
	- Qt Tools - > options -> General把Qt Designer的false 改成True就行了！
# Qt中版本兼容问题
在Qt中，版本向下兼容。Qt6可以通过添加Qt5补充库来兼容Qt5

