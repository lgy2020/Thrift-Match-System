## 一、项目描述

### 游戏匹配服务
[](https://git.acwing.com/ycr2022/thrift/-/raw/master/game.jpg)

- 服务分为三部分：分别是game，match_system，save_server
- game为match_client端，通过match.thrift接口向match_system完成添加用户和删除用户的操作
- match_system由两部分组成，分别为match_server端和save_client端。match_server端负责接收match_client端的操作，将用户添加进匹配池，并且在匹配结束之后通过save.thrift接口将用户数据上传至另一个服务器
- save_server用于接收match_system上传的匹配成功的用户信息

### 游戏匹配服务项目流程

- 构建match.thrift接口
- 通过match.thrift接口构建服务端和客户端
- 先将服务端和客户端跑通，能完成基本的连接通信
- 完成match.thrift的客户端需求
- 构建save.thrift接口
- 通过save.thrift接口构建服务端和客户端
- 将客户端业务添加到match_system当中，将save.thrift服务端完成（本项目save.thrift服务端已经完成）
- 根据业务需求完善match_system


## 二、项目完成过程

1. 在github上创建项目，在teminal中创建thrift文件并将当前文件初始化为仓库
2. 根据项目需求创建文件夹本项目中一共分为三个模块game，match_system，thrift 
3. 在thrift文件夹中创建match.thrift文件，登录thrift官方网站查看tutorial.thrift官方文档根据项目需求完成match.thrift，本项目需要定义三个部分

4. 由thrift接口生成服务端，进入match_system文件夹中（最好多创建一个src文件夹）在src文件夹下执行thrift官方文档中thrift -r --gen <language> <Thrift filename>直接生成服务端，生成的文件为gen.cpp将其改名为match_server，进入match_server文件夹查看Match_server.skeleton.cpp为服务端代码，将其copy到src目录下并重命名为main.cpp
5. 打开main.cpp，先在函数后面加上返回值，并编译文件（在工程中一般先将文件编译成功再加具体的逻辑），cpp文件编译包括两步，编译和链接
6. 由thrift接口生成客户端，在game文件夹中创建src文件夹，执行thrift -r --gen py tutorial.thrift生成gen.py将其改名为match_client，查看文件中有服务器端文件Match-remote将其删除，因为目前只需要生成客户端（注意：在cpp中生成客户端此文件必须删除，因为cpp编译文件中只能有一个main函数）
7. 在src目录下创建client.py，将官方文档中的client端代码复制到client.py中，注意修改头文件，执行python3 <filename>看看编译成功。如果编译成功则在代码中加上用户信息并调用服务端的函数，先启动服务端的main.cpp，再运行client.py看看服务端和客户端是否连接成功。修改代码使其能够读取终端中输入用户，编译运行如成功运行则match客户端完成
8. 修改服务端，具体修改逻辑参考https://git.acwing.com/lgy2020/thrift_lesson/-/blob/master/match_system/src/main.cpp 
9. 在thrift文件夹目录下新建save.thrift，在y总目录中将内容复制过来，在src目录下同样执行thrift -r --gen py tutorial.thrift生成gen.cpp文件将其改名为save.client，进入文件夹将里面的.skeleton.cpp删除
10. 在main.cpp中实现save_client的功能，查看thrift官方文档，具体修改逻辑参考https://git.acwing.com/lgy2020/thrift_lesson/-/blob/master/match_system/src/main.cpp
11. 实现具体业务需求

- 将消费者模型升级为多线程4.0
- 将匹配机制完善5.0，等待时间越长，阈值越大


