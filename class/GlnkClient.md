GlnkClient
===


* 这个类负责设置SDK运行环境

---


class GlnkClient{


* 函数名： init
* 作用  ： 初始化[GlnkClient]实例
* 参数  ： 
    * clientName     ： 客户端名称
    * firstStartTime ： 客户端首次启用时间
    * clientUDID     ：	客户端的UDID
    * version    	 ：	客户端版本号
    * type		   	 ： 客户端类型
* 返回值： 成功：0；失败：-1

```C
int init(const char* clientName, const char* firstStartTime, const char* clientUDID, int version, int type);
```

* 函数名： setOnDeviceStatusChangedListener
* 作用  ： 设置设备状态通知类，当调用addGID函数后，会返回设备的在线状态
* 参数  ： 
    * l ： [DeviceStatusChangedListener]对象指针
* 返回值： 成功：0；失败：-1

```C
int setOnDeviceStatusChangedListener(DeviceStatusChangedListener* l);
```

* 函数名： addGID
* 作用  ： 添加预连接gid，可以知道设备的在线状态；需要在start()后调；可重复调用函数添加多个GID
* 参数  ： 
    * gid ： 设备gid
* 返回值： 成功：0；失败：-1

```C
int addGID(const char* gid);
```


* 函数名： start
* 作用  ： 启动GlnkClient
* 参数  ： 无
* 返回值： 成功：0；失败：-1

```C
int start();
```


* 函数名： release
* 作用  ： 释放GlnkClient
* 参数  ： 无
* 返回值： 无

```C
void release();
```

* 函数名： setStatusAutoUpdate
* 作用  ： 设备状态自动更新，当设备上下线时候，会调用[DeviceStatusChangedListener]进行回调通知
* 参数  ： 
    * sau ：  0-不更新；1-更新
* 返回值： 成功：0；失败：-1

```C
int setStatusAutoUpdate(int sau);
```


* 函数名： getGlnkCVersion
* 作用  ： 获取Glnk版本号,可不调用
* 参数  ：无
* 返回值： SDK版本号

```C
static char* getGlnkCVersion();
```

* 函数名： getGlnkBuildDate
* 作用  ： 获取Glnk版本Build时间,可不调用
* 参数  ：无
* 返回值： SDK版本Build时间

```C
static char* getGlnkBuildDate();
```


};



[DeviceStatusChangedListener]: DeviceStatusChangedListener.md
[GlnkClient]: GlnkClient.md

***
DEMO
---

```C
#include "GlnkClientMgr.h"
#include "glnk_client.h"
int main()
{
    const char* gid = {"abccxxxxxx","abccxxxxxx2"};
    
    GlnkClientMgr* clientMgr = GlnkClientMgr::getInstance();
    if(clientMgr)
    {
        GlnkClient* client = clientMgr->getGlnkClient();//获取唯一GlnkClient对象
        if(client)
        {
            if(-1 == client->init("Demo", "20150914", "1234567890", 1, 1))//设置环境
                goto err;
                
            if(-1 == client->setStatusAutoUpdate(1))
                goto err;
                
            if(-1 == client->start()) 
                goto err;
                
            int re = 0;
            for(int i = 0;i < 2; i++)
                re = client->addGID(gid[i]);
                
                
            ... 
            ...
            
        }
    }
    
err:
    if(client)
        client->release();
    if(clientMgr)
        clientMgr->release();
    return 0;
}
```
