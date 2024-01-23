Talkatone链接不支持UDP转发（比如HY2协议），往往在连接时需要采用ss这种TCP转发的协议，而本人平时喜用HY2低倍率节点，此规则可实现Talkatone在Sing-Box中分流设置。规则文件本身并不大，不做预编译，引用方式如下。
```
      {
        "tag": "geosite-Talkatone",
        "type": "remote",
        "format": "source",
        "url": "https://testingcf.jsdelivr.net/gh/PhantomSeaStars/Rule@main/Talkatone2.json",
        "download_detour": "direct"
      },
```
Copilot也写了规则，用于实现独立分流设置，需要可自取。

研究过程中解决了一个问题，就是挂代理后OneDrive同步时会消耗大量机场流量，不挂代理OneDrive的网页端进不去，就用不了文件分享的功能，引用OneDrive规则去切换它也比较麻烦。如果有遇见相同问题的朋友可以在路由规则顶部（规则匹配是从上到下扫描）加上
```
      {
        "domain_suffix": [
          "storage.live.com",
          "files.1drv.com"
        ],
        "outbound": "direct"
      }
```
第一条是客户端下载信道，第二条是网页下载信道，让其优先匹配为直接连接。
