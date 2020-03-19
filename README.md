#  内核主要是老版本的shadowsocksR，支持ssr. 新版本已经不行了，只能简单的ss,很容易被封禁。故此此版本是基于历史保存的收藏版做简单修改和部署一键化。

# ShadowServerSSR
建立代理服务器，可设置混淆算法、混淆参数、多用户、多种协议。重点：不被aliyun检测到。（Setting up proxy server can set up obfuscation algorithm, obfuscation parameter, multi-user and multi protocol. tips: can not detected by aliyun.）

# 方法：
 1.首先这是一个python代码，基于python3.6, 不懂的如何建立python项目环境的请自行脑补；
 
 2.安装openSSL, windows安装OpenSSL（下载完成一路安装即可），区分32位和64位（下述路径都为安装路径，每个人的略微有差别）：
http://slproweb.com/products/Win32OpenSSL.html
请按照默认目录安装两个软件，安装两个软件之后，修改：C:program files\OpenSSL-Win32、C:program files\\OpenSSL-Win32\bin中，把libcrypto-1_1.dll和libssl-1_1.dll后面的-1.1删掉，删掉之后文件为:libcrypto.dll、libssl.dll。

3.配置openssl系统环境变量：我的电脑 — 属性 — 高级系统设置 — 高级 选项卡 — 环境变量 按钮 —第二个框里面的： 系统变量 Path
点击编辑，前面填上：C:program files\OpenSSL-Win32\bin\;

4. 项目的python环境可以用pycharm结合配置python-envs运行最好, 对于普通的执行方法可能会遇到各种路径环境问题，如要激活环境、配置项目路径到python域内等，懂python的应该很了解。

# 运行
执行 python3 ShadowServerSSR/shadowSSR/shadowsocks/server.py -c config-user.json
执行方法有很多种，上面提供了执行的main和参数，细节需要自己修改。

# 配置config
 我设计的文件在config_user.json中:
 {
    "server": "0.0.0.0",
    "server_ipv6": "::",
    "server_port": 8401, // 开放的端口，如果是aliyun,还要放行你自己设置的端口
    "local_address": "127.0.0.1",
    "local_port": 1080,

    "password": "114827", // 客户端登录时用的密码
    "method": "rc4-md5",
    "protocol": "auth_sha1_v4",
    "protocol_param": "",
    "obfs": "tls1.2_ticket_auth", # 混淆方案
    "obfs_param": "intl.aliyun.com", # 混淆参数，经测试用这个参数可以骗过aliyun
    "speed_limit_per_con": 0,
    "speed_limit_per_user": 0,

    "additional_ports" : {}, // only works under multi-user mode
    "additional_ports_only" : false, // only works under multi-user mode
    "timeout": 120,
    "udp_timeout": 60,
    "dns_ipv6": false,
    "connect_verbose_info": 0,
    "redirect": "",
    "fast_open": false
}
