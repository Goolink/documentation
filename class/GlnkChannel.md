GlnkChannel
===


* 这个类负责设备操作（如：实时预览、回放、透明通道等）
* **注意：每一个GlnkChannel对象只能用于一种操作，不能重复使用；如：stop()后就不能再start()了，否则会出现莫明其妙的错误**

---


class GlnkChannel{

* 函数名： Create
* 作用  ： 创建GlnkChannel的对象
* 参数  ： 
    * client     ： [GlnkClient]指针
    * l ： [DataSourceListener]指针
* 返回值： 成功-GlnkChannel指针;失败-NULL

```C
static GlnkChannel* Create(GlnkClient *client, DataSourceListener* l);
```


* 函数名： setMetaData
* 作用  ： 设置连接参数,设置此GlnkChannel是用于实时预览/回放/透明通道
* 参数  ： 
    * gid        ： 设备gid
    * uname      ： 设备账号用户名，不能为null, 没有则填空字符串
    * passwd     ： 设备账号密码，不能为null, 没有则填空字符串
    * channelNO  ： 通道号，从0开始
    * streamType ： 码流类型， 0-主码流； 1-次码流； 2-回放录像； 3-透明通道
    * dataType   ： 流数据类型,  0-视频流, 1-音频流, 2-音视频流
* 返回值： 成功-0；失败-负数

```C
int setMetaData(const char* gid, const char* uname, const char* passwd,
			int channelNO, int streamType, int dataType);
```


* 函数名： setMetaData2
* 作用  ： 设置连接参数,用于直接ip进行连接,设置此GlnkChannel是用于实时预览/回放/透明通道
* 参数  ： 
    * ip         ： 设备ip
    * port       ： 设备端口
    * uname      ： 设备账号用户名，不能为null, 没有则填空字符串
    * passwd     ： 设备账号密码，不能为null, 没有则填空字符串
    * channelNO  ： 通道号，从0开始
    * streamType ： 码流类型， 0-主码流； 1-次码流； 2-回放录像； 3-透明通道
    * dataType   ： 流数据类型,  0-视频流, 1-音频流, 2-音视频流
* 返回值： 成功-0；失败-负数

```C
int setMetaData2(const char *ip, unsigned short port, const char* uname, int unameLen, const char* passwd, int pwdLen,
			int channelNO, int streamType, int dataType);
```

* 函数名： setReconnectable
* 作用  ： 设定若设备断线后可否自动重连
* 参数  ： reconn ：1- 可重连, 0- 不重连
* 返回值： 无

```C
void setReconnectable(int reconn);
```

* 函数名： setModeChangeable
* 作用  ： 设定连接模式可否切换，如从P2P连接切换为服务器转发
* 参数  ： chg ：1- 切换, 0- 不切换
* 返回值： 无

```C
void setModeChangeable(int chg);
```


* 函数名： setAuthMode
* 作用  ： 认证模式
* 参数  ： mode ：0- 不认证(不登录)；1-认证并登录（**默认**）
* 返回值： 无

```C
void setAuthMode(int mode);
```


* 函数名： start
* 作用  ： 开始连接设备
* 参数  ： 无
* 返回值： 成功-0；失败- 负数；

```C
int start();
```


* 函数名： sendData
* 作用  ： 发送透明通道数据，**优先使用此函数**
* 参数  ： 
    * data ： 发送的数据内容
    * length ： 发送的数据的长度
* 返回值： 成功-0；失败-负数；

```C
int sendData(const void *data, unsigned int length);
```


* 函数名： sendData
* 作用  ： 发送透明通道数据，需要调用者按照OWSP协议封装数据
* 参数  ： 
    * type ： 发送透明通道类型
    * data ： 发送的数据内容（已按照OWSP协议封装好）
    * length ：发送的数据的长度
* 返回值： 成功-0；失败-负数；

```C
int sendData(unsigned short type, const void *data, unsigned int length);
```


* 函数名： sendManuData
* 作用  ： 发送透明通道数据，需要调用者按照OWSP协议封装数据
* 参数  ： 
    * data ： 发送的数据内容（已按照OWSP协议封装好）
    * length ：发送的数据的长度
* 返回值： 成功-0；失败-负数；

```C
int sendManuData(const void *data, unsigned int length);
```


* 函数名： keepliveReq
* 作用  ： 发送心跳包，保持与设备的连接；**默认不发送**，则如果长时间不操作，SDK会自动断开连接，若调用此函数，则不会主动断开与设备的连接，建议在连接设备后，每10秒调用一次
* 参数  ： 无
* 返回值： 成功-0；失败-负数；

```C
int keepliveReq();
```

* 函数名： stop
* 作用  ： 主动断开与设备的连接
* 参数  ： 无
* 返回值： 无

```C
void stop();
```


* 函数名： release
* 作用  ： 释放GlnkChannel的对象
* 参数  ： 无
* 返回值： 无

```C
void release();
```

* 函数名： startTalking
* 作用  ： 开始对讲
* 参数  ： 无
* 返回值： 成功-0；失败-负数；

```C
int startTalking();
```

* 函数名： stopTalking
* 作用  ： 停止对讲
* 参数  ： 无
* 返回值： 成功-0；失败-负数；

```C
int stopTalking();
```


* 函数名： sendAudioData
* 作用  ： 发送音频数据
* 参数  ： 
    * time_ms ： 时间戳
    * data ： 音频帧
    * length ： 音频帧大小
* 返回值： 成功-0；失败-负数；

```C
int sendAudioData(int time_ms, const void *data, unsigned int length);
```


* 函数名： sendAudioDataByManu
* 作用  ： 发送音频数据，需要调用者按照OWSP协议封装数据
* 参数  ： 
    * frameInfo ： 音频帧信息
    * infoLength ：音频帧信息大小
    * data ： 音频帧
    * dataLength ： 音频帧大小
* 返回值： 成功-0；失败-负数；

```C
int sendAudioDataByManu(const void * frameInfo, unsigned int infoLength, const void * data, unsigned int dataLength);
```


* 函数名： sendPTZCmd
* 作用  ： 云台操作
* 参数  ： 
    * cmd ： [PTZCMD]云台操作
    * arg ：步长, 默认为4
* 返回值： 成功-0；失败-负数；

```C
int sendPTZCmd(PTZCMD cmd, int arg = 4);
```


* 函数名： getDeviceInfo
* 作用  ： 获取设备信息
* 参数  ： 
    * devinfo ： [GlnkDeviceInfo]返回的设备信息
* 返回值： 成功-0；失败-负数；

```C
int getDeviceInfo(GlnkDeviceInfo *devinfo);
```


* 函数名： searchRemoteFile
* 作用  ： 远程录像文件搜索
* 参数  ： 
    * channelMask ： 通道，按位表示对应的通道号（如：0x3 代表搜索通道0和1）
    * typeMask ： 录像类型 ： 0x01 = 开关量告警录像, 0x02 = 移动侦测录像, 0x04 = 常规录像, 0x08 = 手动录像, 0xFF = 全部录像
	* startYear ：查询起始时间
	* startMonth
	* startDay
	* startHour
	* endYear ：查询终止时间
	* endMonth
	* endDay
	* endHour
* 返回值： 成功-0；失败-负数；

```C
int searchRemoteFile(unsigned long long int channelMask, int typeMask, int startYear, int startMonth, int startDay, int startHour,
			int endYear, int endMonth, int endDay, int endHour);
```


* 函数名： remoteFileRequest
* 作用  ： 请求播放远程录像文件
* 参数  ： 
    * filename ： 需要播放的文件名
* 返回值： 成功-0；失败-负数；

```C
int remoteFileRequest(const char *filename);
```


* 函数名： remoteFileCtrlRequest
* 作用  ： 远程录像文件播放控制，该方法仅支持录像回放新协议。
* 参数  ： 
    * ctrlCmd ： [RecPlayCtrl]
    * cmdValue ： 不同RecPlayCtrl代表不同含义，见备注
    * reqStartime ：开始时间，单位ms
    * reqEndtime ： 结束时间，单位ms
* 返回值： 成功-0；失败-负数；
* **备注**
     * ** e.g.**
	 * **1, 播放: remoteFileCtrlRequest(Play_Ctrl_Start, 0, 0, 0);**
	 * **2, 暂停: remoteFileCtrlRequest(Play_Ctrl_Pause, 0, 0, 0);**
	 * **3, 继续: remoteFileCtrlRequest(Play_Ctrl_Resume, 0, 0, 0);**
	 * **4, 停止: remoteFileCtrlRequest(Play_Ctrl_Stop, 0, 0, 0);**
	 *
	 * **5, 快放，cmdValue表示是倍数，2，4，8表示是以2倍，4倍，8倍播放。remoteFileCtrlRequest(Play_Ctrl_Plus, 2, 0, 0);**
	 * **6, 慢放， cmdValue表示是分数，2，表示是以二分之一的速度播放。remoteFileCtrlRequest(Play_Ctrl_Minus, 2, 0, 0);**
	 * **7, 拖放，cmdValue表示时间，5000表示拖到5000ms处播放。remoteFileCtrlRequest(Play_Ctrl_SeekTo, 5000, 0, 0);**
	 * **8, 请求一段时间的视频流，cmdValue在此无意义。remoteFileCtrlRequest(Play_Ctrl_UpdateTime, 0, 1000, 10000);//请求从第1000ms到第10000ms的视频流。**

```C
int remoteFileCtrlRequest(RecPlayCtrl ctrlCmd, int cmdValue, int reqStartime, int reqEndtime);
```

[PTZCMD]: unit.md
[GlnkDeviceInfo]: unit.md
[RecPlayCtrl]: unit.md
[GlnkClient]: GlnkClient.md
[DataSourceListener]: DataSourceListener.md

***
DEMO
---
[实时预览&&云台控制](../demo/realplay.md)  
[录像查找&&录像回放](../demo/playback.md)  
[通明通道](../demo/manul.md)  
[实时对讲](../demo/talk.md)  
[内网搜索](../demo/search.md)  