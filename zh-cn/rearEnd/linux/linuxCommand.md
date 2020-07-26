## Linux 命令总结

- mkdir wzg：创建 wzg 目录
- touch wzg：创建 wzg 文件
- rm：移除文件或目录
- ls -l ：显示指定工作目录下之内容资讯详细
- pwd：显示目前的目录
- tar -zcf wzg.tar.gz wzg1：把 wzg1 打包成 wzg.tar.gz（源文件存在）
- tar -zxf wzg.tar.gz：把 wzg.tar.gz 解压（源文件存在）
- cat 由第一行开始显示文件内容
- more 一页一页的显示文件内容

- less 与 more 类似，但是比 more 更好的是，他可以往前翻页！
- head 只看头几行
- netstat -tlun 查看本机监听的端口
- netstat -ntulp |grep 80 //查看所有 80 端口使用情况\*
- netstat -an | grep 3306 //查看所有 3306 端口使用情况·\*
- ​ 查看当前所有监听端口·\*
