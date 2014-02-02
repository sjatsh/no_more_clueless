Mozilla Firefox 使用profile文件夹来保存用户设置。但是遇到计算机崩溃等情况，再次安装Firefox，以前所做的设置就会丢失。还有一种情况是要在其他的计算机用相同的配置。

一个可行的方法就是利用同步网盘储存profile文件夹，然后令firefox启动时直接调用同步文件夹里的内容。

下面是详细的步骤：

1. 安装Skydrive。
     * 为什么是Skydrive？主要基于以下两个方面考虑：第一，Skydrive在中国大陆速度差强人意；第二，在可以预见的未来我不相信大陆当局会墙了微软的网站。
     * 下载Skydrive应用 http://windows.microsoft.com/zh-cn/skydrive/download 。
     * 安装，按照提示申请账号。
     * 设置同步文件夹，我设在了 D:\SkyDrive ，当然其他的文件夹都是合适的，空间够就行。新的Skydrive账号似乎是7G空间，这个年代的机器找出个盘有10G空间不是个难事。
2. 设置Firefox。
     * 刚才说了Skydrive的速度只能说是差强人意，所以我们要尽可能做到两点：
          * profile文件夹尽量小
          * profile 文件改动尽量少
     * 按<Win>+R，输入`%APPDATA%\Mozilla\Firefox\`，回车。
     * 备份这个文件夹（**这很重要**），所有没有做这一步最后失败了全是耍流氓！
     * 打开`profiles.ini`，把`Path=`后面那个文件夹把当前文件夹拷一份在同步文件夹里，命名为`default`
     * 修改文件`profiles.ini`,如果你也把D:\SkyDrive设为了同步文件夹，那么就改成这样的：
```
[General]
StartWithLastProfile=1

[Profile0]
Name=default
IsRelative=0
Path=D:\SkyDrive\default
Default=1

```
     * 打开Firefox，看看你的书签、附加组件什么的还在不在。如果还在，就好。不在了？还没有备份？…… 
     * 在地址栏中输入`about:config`。
     * 新建几个值：
| 编号 |  类型 |                    变量名称                   |          值         |
|:--:|:---:|:-----------------------------------------:|:------------------:|
|  1 | 字符串 |    browser.cache.disk.parent_directory    | C:\Mozilla\Firefox |
|  2 | 字符串 |   browser.cache.offline.parent_directory  | C:\Mozilla\Firefox |
|  3 | 布尔值 | browser.pagethumbnails.capturing_disabled |        true        |

这几个值的作用，是为了防止Firefox运行中在同步文件夹里写来写去，Skydrive就不停的同步，没有尽头。
