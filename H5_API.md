# 云知声口语评测服务H5 SDK API文档

* [可设参数](#params)
* [函数列表](#functions)
* [回调函数](#callback)
* [示例demo](#create)

#### <a name="params"></a> 可设置参数（[]中是可选参数）
* option 配置选项
* option.userId  用户Id
* [option.host]    评测服务器地址 default https://edu.hivoice.cn
* [option.port]    评测服务器端口号 default 4443
* [option.mode]    评测模式（包含A B C D E G H，A B D H 是常用模式） default  A
* [option.scoreCoefficient]  分数调整定制参数，可以对同样质量的语音调整得分高低，范围是0.6~1.9，默认情况下是1.0，设置越低，打分越严格，
* [option.audioFormat]  //上传的音频格式 16k16bit 32kpbs 单声道mp3格式
* [option.useSelfAudio]  如果设置为true, 将不使用内置录音(不加载录音相关组件), 调用evaluate接口进行评测
* [option.debug]  开启日志打印

#### <a name="functions"></a> 函数列表

*  function EvalSDK(option)

|  |  |
| ----- | ----- |
| 说明 | 创建评测对象 |
| 参数addr | 以上@param中可设置参数 | 

<br/>

*  function start(text, mode)

|  |  |
| ----- | ----- |
| 说明 | 开始录音方法 |
| 参数text | 评测文本 | 
| 参数mode | 评测模式 | 

<br/>

*  function stop()

|  |  |
| ----- | ----- |
| 说明 | 停止录音并开始评测 |
| 参数 | --- | 
| 返回值 | Promise  data  //{text, mode, sessionId, mp3},函数返回可以忽略 | 

<br/>

*  function setServerAddr(addr)

|  |  |
| ----- | ----- |
| 说明 | 设置评测服务器地址 |
| 参数addr | 评测服务器地址，如: http://edu.hivoice.cn:8085/eval/opus | 

<br/>

*  function setAudioFormat(format)

|  |  |
| ----- | ----- |
| 说明 | 上传的音频格式 |
| 参数format | 音频格式，可选值为:  mp3 , opus , amrnb | 

<br/>

*  function setScoreCoefficient(score)

|  |  |
| ----- | ----- |
| 说明 | 分数调整定制参数，可以对同样质量的语音调整得分高低 |
| 参数score | 范围是0.6~1.9，默认情况下是1.0,设置越低，打分越严格，设置系数越高 | 

<br/>

*  function setMode(mode)

|  |  |
| ----- | ----- |
| 说明 | 评测模式 |
| 参数mode | 包含A B C D E G H，A B D H 是常用模式<br>A：最简单模式，结果只有单词打分没有音素信息；<br>B：有音素信息，但是没有音素打分；<br>C：跟A一样，区别是最外层有Score总分;<br>D：在B的基础上，有音素打分;<br>E：返回words字段里的值，有空格和标点符号，但是没有音素打分(针对个别客户需求);<br>G：跟D一样;<br>H：选择题打分模式 | 

<br/>

*  function evaluate(text, voice, mode)

|  |  |
| ----- | ----- |
| 说明 | 进行评测 |
| 参数text | 评测文本 | 
| 参数voice | 评测音频 | 
| 参数mode | 评测模式 | 
| 返回值 | json格式评测结果 | 

<br/>

*  function getBlob()

|  |  |
| ----- | ----- |
| 说明 | 获取本地Mp3 |
| 参数 | --- | 
| 返回值 | 二进制mp3文件 | 

<br/>

*  function playLocal()

|  |  |
| ----- | ----- |
| 说明 | 播放本地Mp3 |
| 参数 | --- | 
| 返回值 | --- | 

<br/>

*  function stopPlayLocal()

|  |  |
| ----- | ----- |
| 说明 | 停止播放 |
| 参数 | --- | 
| 返回值 | --- | 

<br/>

#### <a name="callback"></a> 回调函数

*  function onReady()

|  |  |
| ----- | ----- |
| 说明 | jsSDK 准备好后回调函数 |
| 参数 | --- | 
| 返回值 | --- | 

<br/>

*  function onStart(sessionId)

|  |  |
| ----- | ----- |
| 说明 | 开始录音回调函数 |
| 参数sessionId | 表示该次评测的唯一表示，必须上传，可使用 uuid | 
| 返回值 | --- | 

<br/>

*  function onStop(e)

|  |  |
| ----- | ----- |
| 说明 | 停止录音回调函数 |
| 参数e | 回调事件 | 
| 返回值 | {"text":"评测文本", "mode": "评测模式", "sessionId": "sessionId" | 

<br/>


*  function onError(err)

|  |  |
| ----- | ----- |
| 说明 | 错误回调 |
| 参数err | 获取错误码 | 
| 返回值 | 错误码 | 

<br/>

*  function onResult(result)

|  |  |
| ----- | ----- |
| 说明 | 评测成功返回 |
| 参数result | 获取结果 | 
| 返回值 | result和url | 

<br/>

*  function onPlayLocal()

|  |  |
| ----- | ----- |
| 说明 | 播放本地音频回调函数 |
| 参数 | --- | 

<br/>

*  function onStopPlayLocal()

|  |  |
| ----- | ----- |
| 说明 | 本地音频播放结束回调函数 |
| 参数 | --- | 

<br/>

#### <a name="create"></a> 示例demo

```
    var recorder    = new EvalSDK({
      userId          :  "AE8F62A7-DDAE-4FD3-ADD4-D0280CEA3EDE";
      scoreCoefficient:  "1.0";
      mode            :  "G";
      debug           :  true
    })
```
