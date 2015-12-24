DeviceStatusChangedListener
===


* 这个类负责接受设备在线状态改变回调

---


class DeviceStatusChangedListener{


* 函数名： onChanged
* 作用  ： 接受设备在线状态改变回调，子类需实现此函数
* 参数  ： 
    * gid     ： 设备gid
    * status  ： 设备状态码，数值如下
        *   -5400: No Network
        *   -5303: 服务器域名错误
        *   -5300: 服务器域名错误
        *   -5299:  GID部署出错，请上报GID
        *   -5000:  无转发服务器
        *   -4113: 	No route to host。指客户端在纯网络
        *   -4111: 	Connection refused，IP地址或端口错误
        *   -4110: 	连接超时
        *   -4101: 	Network is unreachable，客户端网络未启用
        *   -4000: 	系统连接错误
        *      -2: 设备离线
        *   -1: 非法gid
        *   大于0: 在线
        *     1: 在内网
        *    2: 在外网
        * 3: 同时在内,外网
  
* 返回值： 无

```C
virtual void onChanged(const char* gid, int status) = 0;
```



***
DEMO
---
[实时预览&&云台控制](../demo/realplay.md)  
[录像查找&&录像回放](../demo/playback.md)  
[通明通道](../demo/manul.md)  
[实时对讲](../demo/talk.md)  
[内网搜索](../demo/search.md)  