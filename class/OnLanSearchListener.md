OnLanSearchListener
===


* 这个类负责接受内网搜索回调

---


class OnLanSearchListener{


* 函数名： onSearched
* 作用  ： 搜索结果回调，子类需实现此函数
* 参数  ： 
    * gid     ： 设备gid
    * ip  ： 设备内网ip
* 返回值： 无

```C
virtual void onSearched(const char* gid, const char* ip) = 0;
```


* 函数名： onSearchFinish
* 作用  ： 当搜索完后调用此函数，子类需实现此函数
* 参数  ： 无  
* 返回值： 无

```C
virtual void onSearchFinish() = 0;
```


***
DEMO
---
[实时预览&&云台控制](../demo/realplay.md)  
[录像查找&&录像回放](../demo/playback.md)  
[通明通道](../demo/manul.md)  
[实时对讲](../demo/talk.md)  
[内网搜索](../demo/search.md)  