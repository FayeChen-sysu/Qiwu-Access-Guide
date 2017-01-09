# 使用 Socket.IO 接入齐悟机器人
Author: Feliciano.Long

## 概述
使用 Socket.IO 接入齐悟机器人，您需要按照如下步骤完成：  
1. 实现一个 **Socket.IO 客户端**
2. 实现 **登录事件**
3. 实现 **文字提问事件**
4. 处理服务器返回的 **回答事件**
5. *（可选）*实现 **语音提问事件**

使用 Socket.IO 的优势：
1. 响应速度比传统http调用快2倍
2. 不需要轮询，降低网络占用
3. 支持一个问题多句回复
4. 支持自动断线重连
5. 支持人工干预对话

## 实现一个 Socket.IO 客户端
由于 Socket.IO 已有许多现成的成熟解决方案，在此不再赘述。您可以参考以下链接：  

Socket.IO 官方网站：http://socket.io/

几个客户端样例：  
[C++ 客户端](http://socket.io/blog/socket-io-cpp/)  
[Java 客户端](https://github.com/Gottox/socket.io-java-client)  
[Python 客户端](https://pypi.python.org/pypi/socketIO-client)  
[Quick-Cocos2dx 客户端](https://github.com/u0u0/Quick-Cocos2dx-Community/blob/master/cocos/network/SocketIO.h)  
[网页客户端 (Javascript)](http://socket.io/docs/)

## 实现 登录事件
向服务器发送以下事件来进行登录

| 事件名     | 参数一    |
| --------- |:---------:|
| login     | 业务key   |

## 实现 提问事件
向服务器发送以下事件来进行提问

| 事件名     | 参数一          |
| --------- |:---------------:|
| ask       | 提问的文字字符串 |


## 处理服务器返回的 回答事件
当机器人进行回复时，服务器会发送以下事件

| 事件名     | 参数一        |
| --------- |:-------------:|
| answer    | 回答的字符串   |

## *（可选）* 实现 语音提问事件
处理服务器发送的以下事件

| 事件名     | 参数一        |
| --------- |:-------------:|
| voice     | 语音文件      |

+ 语音文件格式暂时只支持 amr
+ 文件大小不能超过 5MB
+ 请使用 *二进制* 方式传输文件

Javascript 代码样例：
```
var data = e.originalEvent.target.files[0];
var reader = new FileReader();
reader.onload = function(evt){
    var file = evt.target.result;
    socket.emit('voice', file);
};
reader.readAsArrayBuffer(data);
```
