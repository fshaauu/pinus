
#### 1.4.x

1. 更新 package.json,转移不需要的包到dev依赖. d58657d523c6ca1782dba1ec4c7d7d5cc62e5e22

2. [pinus]: manualReloadCrons 添加重载前清除选项. 8c1708ee74f68a9ef583827882a36cb0e59ead28



#### 1.4.4

修复NPM没有编译dist的问题.

#### 1.4.3

**pinus-rpc** 修复mqtt调用延迟40～80ms的bug   https://github.com/NetEase/pomelo-rpc/pull/33

分布式部署时，servers 配置有 args参数时，自动添加空格。

Merge pull request #125 from lowkeywx/master
 Modify the log description in the application.start function

Merge pull request #126 from wjt382063576/fix_dict
 fix(dict): Fix the problem of duplicate handler routing in the dictio…


**pinus-protobuf** Encoder可选性能优化，添加Encoder缓存选项。
不优化时的逻辑是，对msg进行JSON.stringify 获取长度*2，再分配Buffer。
使用优化时的逻辑是，使用指定大小的预分配Buffer。

```js
// 指定 pinus-protobuf encode使用 buffer缓存大小
// 使用方法  在 connector配置参数
 app.set('protobufConfig', {
    // protobuf Encoder 使用 5m 的缓存 需要保证每个消息不会超过指定的缓存大小，超过了就会抛出异常
    encoderCacheSize: 5 * 1024 * 1024
 });
// 如果缓存大小不够就会有错误日志
// 缓存大小不够 日志示例
 [2020-03-27T10:44:48.752] [ERROR] pinus - [chat-server-1 channelService.js] [pushMessage] fail to dispatch msg to serverId: connector-server-1, err:RangeError [ERR_OUT_OF_RANGE]: The value of "offset" is out of range. It must be >= 0 and <= 0. Received 1
 at boundsError (internal/buffer.js:53:9)
 at writeU_Int8 (internal/buffer.js:562:5)
 at Buffer.writeUInt8 (internal/buffer.js:569:10)
 at Encoder.writeBytes (F:\develop\gong4-server\logicServer\pinus\packages\pinus-protobuf\lib\encoder.ts:195:20)

```


**pinus-protobuf** protobufConfig 配置添加一个选项 decodeCheckMsg.

解析客户端消息时校验客户端消息字段是否符合protobuf定义

因为目前发现,有的客户端encode消息没有校验消息字段是否完整,导致服务端收到消息以后字段缺失,会出现逻辑问题.

所以添加了这个选项.


**examples/websocket-chat-ts-run** 添加开启 选项 `decodeCheckMsg` 的示例. 并使用 `globalBefore` 进行捕获.


#### 1.4.2

修复web-server  更新express依赖出现的`configure`问题。

fix  #118  #119

回退 web-server express版本

fix pinus-cli lost dependency.



#### 1.4.1
try fix [#63](https://github.com/node-pinus/pinus/issues/65)  运行目录问题，先与pomelo的代码行为保持一致。

添加 error handler 和 globalfilter示例 [examples/websocket-chat-ts-run/game-server/app.ts](examples/websocket-chat-ts-run/game-server/app.ts)

修复 因为修复  [#110](https://github.com/node-pinus/pinus/issues/110) 导致的 所有日志级别都变为INFO的问题。 

#### 1.4.0

更新所有依赖库版本，并修复编译错误。
typescript 版本 3.7.2

fix [#110](https://github.com/node-pinus/pinus/issues/110)  pinus-logger 的logger对象换成原始的 log4js 对象。

#### 1.3.14

fix [#104](https://github.com/node-pinus/pinus/issues/104)

