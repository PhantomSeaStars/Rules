Talkatone往往在连接时需要采用ss协议，而本人平时喜用HY2低倍率节点，此规则可实现Talkatone在Sing-Box中分流设置。
```
      {
        "tag": "<规则集的标签>",
        "type": "remote",
        "format": "source",
        "url": "https://testingcf.jsdelivr.net/gh/PhantomSeaStars/Rules@main/talkatoneAPKandEXE.srs",
        "download_detour": "<用来下载这个规则集的出站>"
      },
```

研究过程中解决了一个问题，就是挂代理后OneDrive同步时会消耗大量机场流量，不挂代理OneDrive的网页端进不去，就用不了文件分享的功能，引用OneDrive规则去切换它也比较麻烦。如果有遇见相同问题的朋友可以在的路由规则（微软和OneDrive的规则前）加上
```
      {
        "domain_suffix": [
          "storage.live.com",
          "files.1drv.com"
        ],
        "outbound": "direct"
      }
```
