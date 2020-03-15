# kNginx Nginx-1.0.14源码学习

### 目录

+ [Nginx命令](#cmd)
+ [obj目录说明](#obj)
+ [参考书籍](#book)

### Nginx命令 <span id="cmd"/>
+ 常用命令
```
nginx                                       #启动Nginx
nginx -c /tmp/nginx.conf                    #指定配置文件
nginx -p /usr/local/nginx                   #另行指定安装目录
nginx -g "pid /var/nginx/test.pid;"         #另行指定全局配置项
nginx -g "pid /var/nginx/test.pid;" -s stop #另行指定全局配置项
nginx -t                                    #测试配置文件是否有错误
nginx -t -q                                 #测试配置选项不把error级别以下的信息输出到屏幕
nginx -v                                    #显示Nginx的版本信息
nginx -V                                    #显示Nginx的版本信息,还会显示配置编译阶段的信息,如GCC编译器版本,操作系统版本,执行configure参数等
nginx -s top                                #快速停止服务
nginx -s quit                               #优雅停止服务
nginx -s reload                             #使运行中的Nginx重读配置项并生效
nginx -s reopen                             #日志文件回滚
```
+ Nginx平滑升级
    - 通知正在运行的旧版本Nginx准备升级.通过向master进程发送USER2信号可达到目的
    ```
    kill -s SIGUSER2 <nginx master pid>
    ```
    - 启动新版本的Nginx,可以使用以上介绍过的任意一种启动方法.这是通过ps命令可以发现新旧版本的Nginx在同时运行
    - 通过kill命令向旧版本的master进程发送SIGQUIT信号,以优雅的方式关闭旧版本的Nginx.随后将只有新版本的Nginx服务运行,此时平滑升级完毕

### obj目录说明 <span id="obj"/>
+ obj目录结构
```
|---ngx_auto_headers.h   #保存些宏定义,会被src/core/ngx_config.h及src/os/unix/ngx_linux_config.h
|---autoconf.err         #autoconf.err 保存configure执行过程中产生的结果
|---ngx_auto_config.h    #保存些宏定义,会被src/core/ngx_config.h及src/os/unix/ngx_linux_config.h
|---ngx_modules.c        #配置模块信息
|---src                  #src目录用于存放编译时产生的目标文件
|   |---core
|   |---event
|   |   |---modules
|   |---os
|   |   |---unix
|   |   |---win32
|   |---http
|   |   |---modules
|   |   |   |---perl
|   |---mail
|   |---misc
|---Makefile            #Makefile文件用于编译Nginx工程以及在加入install参数后安装Nginx
```

### 参考书籍 <span id="book"/>
+ [深入理解Nginx 提取码：uoxd](https://pan.baidu.com/s/1B9Nz81xfZta9m6Ip-eOmAA)