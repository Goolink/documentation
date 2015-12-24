DataSourceListener
===


* 这个类负责[GlnkChannel]操作的回调（如：实时预览、回放、透明通道等）

---


class DataSourceListener{

* 函数名： onConnecting
* 作用  ： 提示正在连接设备
* 参数  ： 无
* 返回值： 无

```C
virtual void onConnecting(){}
```

* 函数名： onConnected
* 作用  ： 提示已连接设备，**需实现此函数**
* 参数  ： 
	*  mode	： 当前设备的连接模式: 1-p2p; 2-relay; 3-服务器分发模式
	*  ip   ： 连接设备的内网IP
	*  port	： 连接设备的端口
* 返回值： 无

```C
virtual void onConnected(int mode, const char* ip, unsigned short port) = 0;
```

* 函数名： onModeChanged
* 作用  ： 提示连接模式改变
* 参数  ： 
	*  mode	： 当前设备的连接模式: =1: p2p, 2: relay, 3: 服务器分发模式
	*  ip   ： 连接设备的内网IP
	*  port	： 连接设备的端口
* 返回值： 无

```C
virtual void onModeChanged(int mode, const char* ip, unsigned short port) {}
```

* 函数名： onDisconnected
* 作用  ： 提示设备非正常断开，**需实现此函数**
* 参数  ： 
	*  errcode	： [errcode]错误码
* 返回值： 无

```C
virtual void onDisconnected(int errcode) = 0;
```
	
* 函数名： onReConnecting
* 作用  ： 提示正在重连开始
* 参数  ： 无
* 返回值： 无

```C
virtual void onReConnecting(){}
```


* 函数名： onAuthorized
* 作用  ： 提示正在重连开始，**需实现此函数**
* 参数  ： 
	*  result	： [result]登录结果
* 返回值： 无

```C
virtual void onAuthorized(int result) = 0;
```


* 函数名： onDataRate
* 作用  ： 每秒的数据流量
* 参数  ： 
	*  bytesPersecond	： 字节数
* 返回值： 无

```C
virtual void onDataRate(unsigned int bytesPersecond) {}
```


* 函数名： onAVStreamFormat
* 作用  ： 音视频参数信息, 使用 getGlnkStreamFormat()获取详细参数信息[GlnkStreamFormat]；在第一次音视频数据来之前，此函数会调用一次
* 参数  ： 
	*  data	： 数据内容
	*  length ： 数据大小
* 返回值： 无

```C
virtual void onAVStreamFormat(void *data, unsigned int length) {}
```

* 函数名： onVideoData
* 作用  ： 视频数据回调，一般来说，每次来的视频数据都是一个完整的I帧或P帧
* 参数  ： 
	*  data	： 视频帧
	*  length ： 数据大小
	*  frameIndex ： 数据帧索引
	*  timestamp ： 时间戳
	*  isIFrame ： 1 - I帧；0 - P帧
* 返回值： 无

```C
virtual void onVideoData(const void *data, unsigned int length, unsigned int frameIndex, unsigned int timestamp, int isIFrame) {}
```


* 函数名： onAudioData
* 作用  ： 音频数据回调
* 参数  ： 
	*  data	： 音频帧
	*  length ： 数据大小
	*  timestamp ： 时间戳
* 返回值： 无

```C
virtual void onAudioData(const void *data, unsigned int length, unsigned int timestamp) {}
```


* 函数名： onIOCtrl
* 作用  ： Setting数据
* 参数  ： 
	*  type ： 数据类型
	*  data	： 数据
	*  length ： 数据大小
* 返回值： 无

```C
virtual void onIOCtrl(unsigned short type, const void *data, unsigned short length) {}
```


* 函数名： onKeepliveResp
* 作用  ： 心跳回复
* 参数  ： 
	*  result ： 暂无意义
* 返回值： 无

```C
virtual void onKeepliveResp(int result){}
```	

* 函数名： onTalkingResp
* 作用  ： 对讲响应，[GlnkChannel]调用startTalking后，此函数返回设备响应状态，若成功之后才能调用[GlnkChannel].sendAudioData发送音频数据
* 参数  ： 
	* result ： 操作返回值，成功 - 1；失败 - 0； 
	* audiofmt ： 设备接受的音频格式 , [G711 Alaw: 0x7A19], [G726: 0x7A20], [AMR_NB, 0x7A21], [AMR VBR: 0x7A22], [SPEEX nb: 0x7A23], [SPEEX wb, 0x7A24], [G711 ulaw: 0x7A25], [AMR_WB: 0xA104]
	* audioChannels ： 音频通道数
	* audioSampleRate ： 音频采样率
	* audioBitsPerSample ： 每采样比特数, 一般为16
* 返回值： 无

```C
virtual void onTalkingResp(int result, int audiofmt, int audioChannels, int audioSampleRate, int audioBitsPerSample){}
```


* 函数名： onVideoDataManu
* 作用  ： 视频帧和用户自定义信息，**除非特殊情况，否则一般不使用此函数，此函数需要与设备端配合**
* 参数  ： 
	*  data ： 视频帧
	*  length ： 视频帧长度
	*  frameInfo ： 帧信息
	*  infoLength ： 帧信息长度
* 返回值： 无

```C
virtual void onVideoDataManu(const void *data, unsigned int length, const void *frameInfo, unsigned int infoLength) {}
```

* 函数名： onAudioDataManu
* 作用  ： 音频帧和用户自定义信息，**除非特殊情况，否则一般不使用此函数，此函数需要与设备端配合**
* 参数  ： 
	*  data ： 音频帧
	*  length ： 音频帧长度
	*  frameInfo ： 帧信息
	*  infoLength ： 帧信息长度
* 返回值： 无

```C
virtual void onAudioDataManu(const void *data, unsigned int length, const void *frameInfo, unsigned int infoLength) {}
```

* 函数名： onIOCtrlByManu
* 作用  ： 设备端返回的透明通道数据
* 参数  ： 
	*  data ： 透明通道数据
	*  length ： 数据长度
* 返回值： 无

```C
virtual void onIOCtrlByManu(const void *data, unsigned short length){}
```


* 函数名： onRemoteFileSearchResp
* 作用  ： 响应远程录像文件搜索[GlnkChannel].searchRemoteFile
* 参数  ： 
	*  result ： 搜索成功 - 1;失败 - 0;
	*  count ： 录像文件数量
* 返回值： 无

```C
virtual void onRemoteFileSearchResp(int result, int count){}
```


* 函数名： onRemoteFileSearchItem
* 作用  ： 具体搜索到的录像文件
* 参数  ： 
	*  framename ： 文件名称
	*  recordType ： 录像类型 ，0x01 = 开关量告警录像, 0x02 = 移动侦测录像, 0x04 = 常规录像, 0x08 = 手动录像, 0xFF = 全部录像
	*  start  ： 起始时间
	*  end  ： 终止时间
* 返回值： 无

```C
virtual void onRemoteFileSearchItem(const char *framename, int recordType,
int startYear, int startMonth, int startDay, int startHour, int startMinute, int startSecond, int startMs,
int endYear, int endMonth, int endDay, int endHour, int endMinute, int endSecond, int endMs) {}
```

* 函数名： onRemoteFileResp
* 作用  ： 响应播放远程录像文件请求[GlnkChannel].remoteFileRequest , **新协议需要再发播放命令(再调用remoteFileCtrlRequest(Play_Ctrl_Start, 0, 0, 0);)**
* 参数  ： 
	*  version ： 录像回放协议版本， 1为旧协议，2为新协议
	*  result ： 设备响应结果，成功 - 1;失败 - 0;
	*  fileDuration  ： 文件时长, 单位ms
* 返回值： 无

```C
virtual void onRemoteFileResp(int version, int result, int fileDuration) {}
```

* 函数名： onRemoteFileEOF
* 作用  ： 远程录像文件播放结束
* 参数  ： 无
* 返回值： 无

```C
virtual void onRemoteFileEOF(){}
```


* 函数名： onRemoteFileCtrlResp
* 作用  ： 响应远程录像文件播放控制remoteFileCtrlRequest,例如快进、慢放、暂停等操作的响应
* 参数  ： 
	* result ： 成功 - 1;失败 - 0;
	* ctrlCmd ： [RecPlayCtrl]类型
* 返回值： 无

```C
virtual void onRemoteFileCtrlResp(int result, int ctrlCmd) {}
```

[result]: unit.md
[GlnkStreamFormat]: unit.md
[PTZCMD]: unit.md
[GlnkDeviceInfo]: unit.md
[RecPlayCtrl]: unit.md
[GlnkClient]: GlnkClient.md
[DataSourceListener]: DataSourceListener.md
[GlnkChannel]: GlnkChannel.md


***
DEMO
---
[实时预览&&云台控制](../demo/realplay.md)  
[录像查找&&录像回放](../demo/playback.md)  
[通明通道](../demo/manul.md)  
[实时对讲](../demo/talk.md)  
[内网搜索](../demo/search.md)  