# Robot_LiteLoader
一个为BDS定制的LL机器人

>功能列表
1. MC聊天->QQ的转发
2. list查在线玩家
3. QQ中chat 发送消息到mc
4. QQ中管理员以上级别“sudo 命令”控制台执行“命令”
5. QQ新群员自动增加白名单，群员退群取消白名单,"重置个人绑定"来重置
6. 自定义指令

>安装指南
1. 在Release或Action中下载LL_Robot.zip，并解压在BDS\plugins文件夹中，dll要在plugins中，json要在LL_Robot文件夹
2. 在[[Mrs4s/go-cqhttp]](https://github.com/Mrs4s/go-cqhttp)中下载go-cqhttp，并开启http通信
3. 打开go-cqhttp配置文件，http通信设置为
```
  - http: # HTTP 通信设置
      host: 127.0.0.1 # 服务端监听地址
      port: 5700      # 服务端监听端口
      timeout: 5      # 反向 HTTP 超时时间, 单位秒，<5 时将被忽略
      long-polling:   # 长轮询拓展
        enabled: false       # 是否开启
        max-queue-size: 2000 # 消息队列大小，0 表示不限制队列大小，谨慎使用
      middlewares:
        <<: *default # 引用默认中间件
      post:           # 反向HTTP POST地址列表
      #- url: ''                # 地址
      #  secret: ''             # 密钥
      #  max-retries: 3         # 最大重试，0 时禁用
      #  retries-interval: 1500 # 重试时间，单位毫秒，0 时立即
      - url: http://127.0.0.1:5701 # 地址
        secret: ''                  # 密钥
        max-retries: 0             # 最大重试，0 时禁用
        retries-interval: 0      # 重试时间，单位毫秒，0 时立即
```
4. 启动go-cqhttp
5. 打开BDS根目录下的RobotInfo.json
6. 将"QQ_group_id"的值改为要转发的QQ群号，将"serverName"的值改成你自己的服务器名
7. 调整控制台编码为UTF-8
8. 启动BDS见到“Websocket Loaded”则已启动完成，QQ群发送“服务器已启动”

>自定义指令功能
1. 打开插件中的Message文件
2. 根据范例，依次往后排序号0，1，2...
3. 其中的QQ表示QQ收到的信息，mc表示QQ收到信息后在mc聊天板发送的东西，cmd表示QQ收到消息后控制台执行的命令
4. 这是一个范例，执行效果为清理掉落物
```
{
  "0": {
    "cmd": "help",
    "mc": "test report",
    "QQ": "自定义命令范例"
  },
  "1": {
    "QQ": "清理掉落物",
    "mc": "开始清理掉落物",
    "cmd": "kill @e[type=item]"
}
```
5. 注意，自定义指令为实时加载，编辑完后保存，无需重启服务器直接就能使用
6. 注意，若不需要执行指令或发消息，写为
```
  "mc": ""
  "cmd": ""
```

>使用第三方软件列表
* [[Mrs4s/go-cqhttp]](https://github.com/Mrs4s/go-cqhttp)
* [[yhirose/cpp-httplib]](https://github.com/yhirose/cpp-httplib)
* [[nlohmann/json]](https://github.com/nlohmann/json)

>鸣谢
* 感谢go-cqhttp,cpp-httplib,json三个项目的支持
* 感谢LL中大佬的指教
* 感谢Tenderbear服务器全体成员的测试
