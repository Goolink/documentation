#结构定义

```C
typedef struct _GlnkDeviceInfo{
    int channels;
    char comid[32];
}GlnkDeviceInfo;
```

```C
typedef struct _GlnkStreamFormat{
    int dataType;	//流数据类型, 0:视频流, 1:音频流, 2:音视频流
	int videofmt;	//视频格式， 一般是h264
	int videoFramerate; //视频帧率
	int videoWidth;	//视频宽
	int videoHeight;	//视频高
	int videoIFrameInterval; //视频I帧间隔
	int audiofmt; //音频格式 , [G711 Alaw: 0x7A19], [G726: 0x7A20], [AMR_NB, 0x7A21], [AMR VBR: 0x7A22], [SPEEX nb: 0x7A23], [SPEEX wb, 0x7A24], [G711 ulaw: 0x7A25], [AMR_WB: 0xA104]
	int audioChannels; //音频通道数
	int audioSampleRate; //音频采样率
	int audioBitsPerSample; //每采样比特数, 一般为16.
}GlnkStreamFormat;
```

* 函数名： getGlnkStreamFormat
* 作用  ： 获取音视频流信息
* 参数  ： 
    *  fmt	： 音视频结构体
    *  data ： [onAVStreamFormat]返回的数据
    *  length ： [onAVStreamFormat]返回的数据大小
* 返回值： 无

```C
int getGlnkStreamFormat(GlnkStreamFormat *fmt, void *data, int length);
```


[onAVStreamFormat]: DataSourceListener.md


---


 ###云台控制码,取值范围为0~255
 ```C
enum PTZCMD {
	PTZ_MV_STOP				= 0, // 停止运动
	PTZ_ZOOM_DEC			= 5,
	PTZ_ZOOM_INC			= 6,
	PTZ_FOCUS_INC			= 7, // 焦距
	PTZ_FOCUS_DEC			= 8,
	PTZ_MV_UP				= 9, // 向上
	PTZ_MV_DOWN				= 10, // 向下
	PTZ_MV_LEFT				= 11, // 向左
	PTZ_MV_RIGHT			= 12, // 向右
	PTZ_IRIS_INC			= 13, // 光圈
	PTZ_IRIS_DEC			= 14, //
	PTZ_AUTO_CRUISE			= 15, // 自动巡航
	PTZ_GOTO_PRESET			= 16, // 跳转预置位
	PTZ_SET_PRESET			= 17, // 设置预置位点
	PTZ_CLEAR_PRESET		= 18, // 清除预置位点
	PTZ_ACTION_RESET		= 20, // PTZ复位
	PTZ_MV_LEFTUP			= 21,
	PTZ_MV_LEFTDOWN			= 22,
	PTZ_MV_RIGHTUP			= 23,
	PTZ_MV_RIGHTDOWN		= 24,
	PTZ_CLEAR_TOUR			= 25,
	PTZ_ADD_PRESET_TO_TOUR	= 26,
	PTZ_DEL_PRESET_TO_TOUR	= 27,
};

enum RecPlayCtrl {
	Play_Ctrl_Start  = 1, //播放
	Play_Ctrl_Pause  = 2, //暂停
	Play_Ctrl_Resume = 3, //继续
	Play_Ctrl_Stop   = 4, //停止
	Play_Ctrl_Plus   = 5, //快放
	Play_Ctrl_Minus  = 6, //慢放
	Play_Ctrl_SeekTo = 7, //seek
	Play_Ctrl_UpdateTime = 8
};
```

---

```C
/*******************************************
 * onAuthorized 错误码
 *******************************************/
#define GLNK_AUTH_LOGIN_FAILED    		-10 //登录失败
#define GLNK_AUTH_SUCC					1 // 成功
#define GLNK_AUTH_USER_PWD_ERROR   		2 // 用户名或密码错
#define GLNK_AUTH_PDA_VERSION_ERROR  	4 // 版本不一致
#define GLNK_AUTH_MAX_USER_ERROR   		5  // 超过最大用户数
#define GLNK_AUTH_DEVICE_OFFLINE   		6  // 设备已经离线
#define GLNK_AUTH_DEVICE_HAS_EXIST   	7  // 设备已经存在
#define GLNK_AUTH_DEVICE_OVERLOAD   	8  // 设备性能超载(设备忙)
#define GLNK_AUTH_INVALID_CHANNLE   	9  // 设备不支持的通道
#define GLNK_AUTH_PROTOCOL_ERROR   		10  // 协议解析出错
#define GLNK_AUTH_NOT_START_ENCODE   	11  // 未启动编码
#define GLNK_AUTH_TASK_DISPOSE_ERROR   	12  // 任务处理过程出错
#define GLNK_AUTH_CONFIG_ERROR   		13  // 配置失败
#define GLNK_AUTH_NOT_SUPPORT_TALK   	14  // 不支持双向语音
#define GLNK_AUTH_TIME_ERROR   			15  // 搜索时间跨天
#define GLNK_AUTH_OVER_INDEX_ERROR   	16  // 索引超出范围
#define GLNK_AUTH_MEMORY_ERROR   		17  // 内存分配失败
#define GLNK_AUTH_QUERY_ERROR   		18  // 搜索失败
#define GLNK_AUTH_NO_USER_ERROR   		19  // 没有此用户
#define GLNK_AUTH_NOW_EXITING   		20  // 用户正在退出
#define GLNK_AUTH_GET_DATA_FAIL   		21  // 获取数据失败
#define GLNK_AUTH_RIGHT_ERROR   		22  // 验证权限失败
#define GLNK_AUTH_OPEN_LOCK_PWD_ERROR   23  // 开锁验证失败
#define GLNK_AUTH_NO_VIDEO   			24  // 当前通道无视频
#define GLNK_AUTH_WIFI_CONFIG_FAILED   	25 //wifi配置失败

/*******************************************
 * onDisconnected 错误码
 *******************************************/
#define GLNK_CONN_NO_NETWORK		-5400 //No Network
#define GLNK_CONN_TO_DOMAIN			-5304 //域名解析超时
#define GLNK_CONN_GOO_NXDOMAIN		-5303 //服务器域名错误
#define GLNK_CONN_LBS_NXDOMAIN		-5300 //服务器域名错误
#define GLNK_CONN_LBS_ERR			-5299 //GID部署出错，请上报GID
#define GLNK_CONN_NO_FWDSVR			-5000 //无转发服务器
#define GLNK_CONN_SYS_ERRNO			-4000 //系统连接错误
#define GLNK_CONN_NET_UNREACH		-4101 //Network is unreachable，客户端网络未启用.
#define GLNK_CONN_TIMEDOUT			-4110 //连接超时
#define GLNK_CONN_REFUSED			-4111 //Connection refused，IP地址或端口错误
#define GLNK_CONN_HOST_UNREACH		-4113 //No route to host。指客户端在纯内网
#define GLNK_CONN_AUTH_FAILED		-20 //登录验证失败
#define GLNK_CONN_LOGIN_FAILED		-10 //登录失败
#define GLNK_CONN_COMPANLYID_INVALID	-3 //gid验证失败
#define GLNK_CONN_DEV_OFFLINE			-2 //设备离线
#define GLNK_CONN_GID_NOAUTH			-1 //非法gid
#define GLNK_CONN_OK					0 //连接已断开
#define GLNK_CONN_OPEN_ERR			5001 //打开连接出错
#define GLNK_CONN_ERR				5002 //连接时出错
#define GLNK_CONN_CLOSE_TOOFAST		5530 //客户端登录成功后，连接马上被断开。
#define GLNK_CONN_READ_TIMEOUT		5540 //读取超时
#define GLNK_CONN_DISCONNECTED		5550 //连接被断开
#define GLNK_CONN_LAN_TIMEOUT		5110 //内网连接超时
#define GLNK_CONN_FWD_TIMEOUT		6110 //外网连接超时
#define GLNK_CONN_DS_TIMEOUT		7110 //分发连接超时
```