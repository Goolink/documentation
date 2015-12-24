GlnkClientMgr
===


* 这个类负责生成GlnkClientMgr唯一实例  

---

```C
class GlnkClientMgr
{
```

* 函数名： getInstance
* 作用  ： 获取[GlnkClientMgr]实例
* 参数  ： 无
* 返回值： 成功：[GlnkClientMgr]实例指针；失败：NULL


```C
static GlnkClientMgr *getInstance();
```


* 函数名： release
* 作用  ： 释放[GlnkClientMgr]实例
* 参数  ： 无
* 返回值： 无

```C
static void release();
```
   
   
* 函数名： getGlnkClient
* 作用  ： 获取[GlnkClient]唯一实例
* 参数  ： 无
* 返回值： 成功：[GlnkClient]实例指针；失败：NULL

```C
GlnkClient* getGlnkClient();
```

**以下函数不需调用**
```C
GlnkClientMgr();
~GlnkClientMgr();
};

```

[GlnkClientMgr]: GlnkClientMgr.md
[GlnkClient]: GlnkClient.md

***
DEMO
---

```C
#include "GlnkClientMgr.h"
int main()
{
    GlnkClientMgr* clientMgr = GlnkClientMgr::getInstance();
    if(clientMgr)
    {
        GlnkClient* client = clientMgr->getGlnkClient();
        if(client)
            ...
            ...
    }
    return 0;
}
```
