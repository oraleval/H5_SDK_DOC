# 云知声口语评测服务H5 SDK API文档

* [可设参数](#params)
* [函数列表](#functions)
    * [function EvalSDK](#EvalSDK)
    * [function start](#start)
    * [function stop](#stop)
    * [function setServerAddr](#setServerAddr)
    * [function setAudioFormat](#setAudioFormat)
    * [function setScoreCoefficient](#setScoreCoefficient)
    * [function setMode](#setMode)
    * [function evaluate](#evaluate)
    * [function getBlob](#getBlob)
    * [function getSoundUrl](#getSoundUrl)
    * [function getResultUrl](#getResultUrl)
    * [function playLocal](#playLocal)
    * [function stopPlayLocal](#stopPlayLocal)
* [回调函数](#callback)
    * [function onReady](#onReady)
    * [function onStart](#onStart)
    * [function onStop](#onStop)
    * [function onError](#onError)
    * [function onResult](#onResult)
    * [function onPlayLocal](#onPlayLocal)
    * [function onStopPlayLocal](#onStopPlayLocal)
* [示例demo](#create)

#### <a name="params"></a> 可设置参数（[]中是可选参数）
* option 配置选项
* option.userId  用户Id
* [option.host]    评测服务器地址 default edu.hivoice.cn
* [option.port]    评测服务器端口号 default ''
* [opt.hostCn]  评测服务器地址 default cn-edu.hivoice.cn
* [opt.portCn]  评测服务器端口号 default ''
* [option.useFlash]  启用flash录音
* [option.mode]    评测模式（包含A B C D E G H，A B D H 是常用模式） default  A
* [option.scoreCoefficient]  分数调整定制参数，可以对同样质量的语音调整得分高低，范围是0.6~1.9，默认情况下是1.0，设置越低，打分越严格，
* [option.audioFormat]  //上传的音频格式 16k16bit 32kpbs 单声道opus格式
* [option.useSelfAudio]  如果设置为true, 将不使用内置录音(不加载录音相关组件), 调用evaluate接口进行文件评测
* [option.autoStop]  根据文本长度自动停止 可选值true/(1~6之间的整数或小数)  默认:false  (true等价于3)  当文本长度小于60时autoStop秒后停止，大于60时根据文本长度计算停止时间，autoStop数字越大录音时间越长
* [option.debug]  开启日志打印

#### <a name="functions"></a> 函数列表

*  <a name="EvalSDK"></a> function EvalSDK(option)

|  |  |
| ----- | ----- |
| 说明 | 创建评测对象 |
| 参数addr | 以上@param中可设置参数 | 

<br/>

*  <a name="start"></a> function start(text, mode, language)

|  |  |
| ----- | ----- |
| 说明 | 开始录音方法 |
| 参数text | 评测文本 | 
| 参数mode | 评测模式 | 
| 参数language | 语言种类 有效值[en/cn] | 

<br/>

*  <a name="stop"></a> function stop()

|  |  |
| ----- | ----- |
| 说明 | 停止录音并开始评测 |
| 参数 | --- | 
| 返回值 | Promise  data  //{text, mode, sessionId, mp3},函数返回可以忽略 | 

<br/>

*  <a name="setServerAddr"></a> function setServerAddr(host)

|  |  |
| ----- | ----- |
| 说明 | 设置评测服务器地址 |
| 参数addr | 评测服务器地址，如: http://edu.hivoice.cn:8085/eval/opus | 

<br/>

*  <a name="setAudioFormat"></a> function setAudioFormat(format)

|  |  |
| ----- | ----- |
| 说明 | 上传的音频格式 |
| 参数format | 音频格式，可选值为:  mp3 , opus , amrnb | 

<br/>

*  <a name="setScoreCoefficient"></a> function setScoreCoefficient(score)

|  |  |
| ----- | ----- |
| 说明 | 分数调整定制参数，可以对同样质量的语音调整得分高低 |
| 参数score | 范围是0.6~1.9，默认情况下是1.0,设置越低，打分越严格，设置系数越高 | 

<br/>

*  <a name="setMode"></a> function setMode(mode)

|  |  |
| ----- | ----- |
| 说明 | 评测模式 |
| 参数mode | 包含A B C D E G H，A B D H 是常用模式<br>A：最简单模式，结果只有单词打分没有音素信息；<br>B：有音素信息，但是没有音素打分；<br>C：跟A一样，区别是最外层有Score总分;<br>D：在B的基础上，有音素打分;<br>E：返回words字段里的值，有空格和标点符号，但是没有音素打分(针对个别客户需求);<br>G：跟D一样;<br>H：选择题打分模式 | 

<br/>

*  <a name="evaluate"></a> function evaluate(text, voice, mode, language)

|  |  |
| ----- | ----- |
| 说明 | 进行评测 | 
| 参数text | 评测文本 | 
| 参数voice | 评测音频, SDK录音只支持opus,如果使用本地音频评测请注意设置setAudioFormat | 
| 参数mode | 评测模式 | 
| 参数language | 语言种类 有效值[en/cn]|
| 返回值 | json格式评测结果 | 

<br/>

*  <a name="getBlob"></a> function getBlob()

|  |  |
| ----- | ----- |
| 说明 | 获取本地Mp3 (废弃)|
| 参数 | --- | 
| 返回值 | 二进制mp3文件 | 

<br/>

*  <a name="getSoundUrl"></a> function getSoundUrl()

|  |  |
| ----- | ----- |
| 说明 | 获取音频地址 |
| 参数 | --- | 
| 返回值 | 音频URL地址 | 

<br/>

*  <a name="getResultUrl"></a> function getResultUrl()

|  |  |
| ----- | ----- |
| 说明 | 获取评测结果地址 |
| 参数 | --- | 
| 返回值 | 评测结果地址 | 

<br/>

*  <a name="playLocal"></a> function playLocal()

|  |  |
| ----- | ----- |
| 说明 | 播放本地音频 |
| 参数 | --- | 
| 返回值 | --- | 

<br/>

*  <a name="stopPlayLocal"></a> function stopPlayLocal()

|  |  |
| ----- | ----- |
| 说明 | 停止播放 |
| 参数 | --- | 
| 返回值 | --- | 

<br/>

#### <a name="callback"></a> 回调函数

*  <a name="onReady"></a> function onReady()

|  |  |
| ----- | ----- |
| 说明 | jsSDK 准备好后回调函数 |
| 参数 | --- | 
| 返回值 | --- | 

<br/>

*  <a name="onStart"></a> function onStart(sessionId)

|  |  |
| ----- | ----- |
| 说明 | 开始录音回调函数 |
| 参数sessionId | 表示该次评测的唯一标识 | 
| 返回值 | --- | 

<br/>

*  <a name="onStop"></a> function onStop(e)

|  |  |
| ----- | ----- |
| 说明 | 停止录音回调函数 |
| 参数e | 回调事件 | 
| 返回值 | {"text":"评测文本", "mode": "评测模式", "sessionId": "sessionId" | 

<br/>


*  <a name="onError"></a> function onError(err)

|  |  |
| ----- | ----- |
| 说明 | 错误回调 |
| 参数err | 获取错误码 | 
| 返回值 | 错误码 | 

<br/>

*  <a name="onResult"></a> function onResult(result)

|  |  |
| ----- | ----- |
| 说明 | 评测成功返回 |
| 参数result | 获取结果 | 
| 返回值 | result和url | 

<br/>

*  <a name="onPlayLocal"></a> function onPlayLocal()

|  |  |
| ----- | ----- |
| 说明 | 播放本地音频回调函数 |
| 参数 | --- | 

<br/>

*  <a name="onStopPlayLocal"></a> function onStopPlayLocal()

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
