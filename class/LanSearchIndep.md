LanSearchIndep
===


* 这个类负责启动内网搜索操作

---


class LanSearchIndep{

* 函数名： Create
* 作用  ： 创建LanSearchIndep的对象
* 参数  ： 
    * l     ： [OnLanSearchListener]
* 返回值： 成功-LanSearchIndep指针;失败-NULL

```C
static LanSearchIndep* Create(OnLanSearchListener* l);
```

* 函数名： start
* 作用  ： 内网搜索开始
* 参数  ： 无
* 返回值： 成功-0;失败-负数

```C
int start();
```

* 函数名： start
* 作用  ： 内网搜索开始
* 参数  ： 
    * searchingTime  ：  搜索总时间, 单位毫秒
    * interval ： 搜索时间间隔, 单位毫秒
* 返回值： 成功-0;失败- -1：已退出搜索， -3：使用移动无线网络或无网络。

```C
int start(int searchingTime, int interval);
```

* 函数名： stop
* 作用  ： 停止内网搜索
* 参数  ： 无
* 返回值： 无

```C
void stop();
```

* 函数名： release
* 作用  ： 释放LanSearchIndep对象
* 参数  ： 无
* 返回值： 无

```C
void release();
```



[OnLanSearchListener]: OnLanSearchListener.md

***
DEMO
---
[实时预览&&云台控制](../demo/realplay.md)  
[录像查找&&录像回放](../demo/playback.md)  
[通明通道](../demo/manul.md)  
[实时对讲](../demo/talk.md)  
[内网搜索](../demo/search.md)  