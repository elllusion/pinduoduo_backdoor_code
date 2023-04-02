# pinduoduo_backdoor_code

这里存放拼多多事件的脱壳后的部分代码

项目根目录下的 .c 和 .h 文件为客户端里的manwe和nvwa加壳虚拟机so库文件的ida pro反编译导出，方便分析和写脱壳工具。

漏洞的触发配置文件请前往我的 [pinduoduo_mango_preset_config_tools](https://github.com/poorjobless/pinduoduo_mango_preset_config_tools) 仓库提取

# 免责声明

注意：本仓库只是存放代码。若您使用本仓库代码作恶，那与本仓库所有者无关！

# 关于漏洞原理

有人已经分析了详见公众号文章：[当 App 有了系统权限，真的可以为所欲为？](https://mp.weixin.qq.com/s/kiLvnJSDZpYRHI_XiUx9gg)

以下内容摘至公众号

Android Framework 中一个核心的对象传递机制是 Parcel， 希望被通过 Parcel 传递的对象需要定义 readFromParcel 和 writeToParcel 接口函数，并实现 Parcelable 接口。 理论上来讲，匹配序列化和反序列化函数应当是自反等效的，但系统 ROM 的开发者在编程过程中可能会出现不匹配的情况，例如写入的时候使用了 writeLong， 读取的时候却使用了 readInt。 这类问题在运行过程中一般不会引起注意，也不会导致崩溃或错误，但在攻击者精心布局下，却可最终利用 Settings 和 system_server 进程，将这个微小的错误转化为 StartAnyWhere 提权。 Android 近年来累计已修复上百个这类漏洞，并在 Android 13 中对 Parcel 机制做了改革，彻底杜绝了大部分此类攻击面。

但对于鸿蒙和绝大部分未升级到 Android 13 的设备和用户来说，他们仍处于危险之中。

