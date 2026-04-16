使用方法

```
      {
        "tag": "site-📞 Talkatone",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/geosite-talkatone.srs",
        "download_detour": "☘️ 默认"
      },
      {
        "tag": "IP-📞 Talkatone",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/geoip-talkatone.srs",
        "download_detour": "☘️ 默认"
      }
```

基于sing-box-1.14.0-alpha.12参考配置。
因为开始倒腾正则表达式，规则量小到足以让我写进配置文件本身，挺好用的供参考。

```
{
  "log": {
    "level": "warn",
    "timestamp": true
  },
  "experimental": {
    "cache_file": {
      "enabled": true
    },
    "clash_api": {
      "external_controller": "127.0.0.1:9090",
      "external_ui": "WebUI",
      "default_mode": "🕊 规则分流"
    }
  },
  "ntp": {
    "enabled": true,
    "server": "cn.pool.ntp.org"
  },
  "dns": {
    "servers": [{
        "type": "tls",
        "tag": "🌱 代理DNS",
        "server": "dns.google",
        "detour": "☘️ 默认"
      },
      {
        "type": "local",
        "tag": "🧶 直连DNS"
      }
    ],
    "rules": [{
        "domain_suffix": "666.work",
        "action": "predefined",
        "answer": "*.666.work. IN A 66.666.666.666"
      },
      {
        "rule_set": "Site-🛑 Ads All",
        "action": "reject"
      },
      {
        "clash_mode": "🪡 全局直连",
        "server": "🧶 直连DNS"
      },
      {
        "clash_mode": "🍀 全局代理",
        "server": "🌱 代理DNS"
      },
      {
        "rule_set": ["APP-🇨🇳 China", "Site-🇨🇳 China"],
        "server": "🧶 直连DNS"
      },
      {
        "rule_set": "Site-🌐 !China",
        "invert": true,
        "action": "evaluate",
        "server": "🌱 代理DNS",
        "client_subnet": "1.80.0.0/13"
      },
      {
        "type": "logical",
        "mode": "and",
        "rules": [{
            "rule_set": "Site-🌐 !China",
            "invert": true
          },
          {
            "rule_set": "IP-🇨🇳 China",
            "match_response": true
          }
        ],
        "action": "respond"
      }
    ]
  },
  "inbounds": [{
    "type": "tun",
    "tag": "🚀 1-14",
    "interface_name": "🚀 1-14",
    "address": "172.18.0.1/30",
    "mtu": 1420,
    "auto_route": true,
    "loopback_address": "10.7.0.1",
    "strict_route": true,
    "route_address": ["0.0.0.0/1", "128.0.0.0/1", "::/1", "8000::/1"],
    "route_exclude_address": ["192.168.0.0/16", "fc00::/7"],
    "endpoint_independent_nat": true,
    "stack": "mixed"
  }],
  "outbounds": [{
      "type": "selector",
      "tag": "☘️ 默认",
      "default": "🇯🇵 日本",
      "outbounds": ["🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🪢 本地直连"]
    },
    {
      "type": "selector",
      "tag": "♻️ 中转选择",
      "default": "🇭🇰 TRI 九龙2🪢",
      "outbounds": ["🇭🇰 TRI 九龙1🪢", "🇭🇰 TRI 九龙2🪢"]
    },
    {
      "type": "selector",
      "tag": "🇨🇳 港澳台",
      "default": "🇭🇰 TRI 九龙1🪢",
      "outbounds": ["🇭🇰 TRI 九龙1🪢", "🇭🇰 TRI 九龙2🪢"]
    },
    {
      "type": "selector",
      "tag": "🇺🇸 美国",
      "default": "🇺🇸 4837 洛杉矶🪢",
      "outbounds": ["🇺🇸 4837 洛杉矶🪢", "🇺🇸 TRI 洛杉矶♻️"]
    },
    {
      "type": "selector",
      "tag": "🇯🇵 日本",
      "default": "🇯🇵 TRI 千叶♻️",
      "outbounds": ["🇯🇵 INTL 千叶🪢", "🇯🇵 TRI 千叶♻️"]
    },
    {
      "type": "selector",
      "tag": "💵 汇丰香港",
      "default": "🇨🇳 港澳台",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国"]
    },
    {
      "type": "selector",
      "tag": "🪙 日游币安SIM",
      "default": "🇯🇵 日本",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国"]
    },
    {
      "type": "selector",
      "tag": "✈️ 电报油管",
      "default": "🇺🇸 美国",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国"]
    },
    {
      "type": "urltest",
      "tag": "🐉 测速",
      "outbounds": ["🇭🇰 TRI 九龙1🪢", "🇭🇰 TRI 九龙2🪢", "🇯🇵 INTL 千叶🪢", "🇯🇵 TRI 千叶♻️", "🇺🇸 4837 洛杉矶🪢", "🇺🇸 TRI 洛杉矶♻️"]
    },
    {
      "tag": "🇭🇰 TRI 九龙1🪢",
      "type": "anytls"
    },
    {
      "tag": "🇭🇰 TRI 九龙2🪢",
      "type": "anytls"
    },
    {
      "tag": "🇺🇸 4837 洛杉矶🪢",
      "type": "anytls"
    },
    {
      "tag": "🇺🇸 TRI 洛杉矶♻️",
      "type": "shadowsocks",
      "detour": "♻️ 中转选择"
    },
    {
      "tag": "🇯🇵 INTL 千叶🪢",
      "type": "anytls",
    },
    {
      "tag": "🇯🇵 TRI 千叶♻️",
      "type": "shadowsocks",
      "detour": "♻️ 中转选择"
    },
    {
      "type": "direct",
      "tag": "🪢 本地直连"
    }
  ],
  "route": {
    "final": "☘️ 默认",
    "auto_detect_interface": true,
    "default_domain_resolver": "🌱 代理DNS",
    "rules": [{
        "action": "sniff"
      },
      {
        "type": "logical",
        "mode": "or",
        "rules": [{
            "protocol": "dns"
          },
          {
            "port": 53
          }
        ],
        "action": "hijack-dns"
      },
      {
        "type": "logical",
        "mode": "or",
        "rules": [{
            "network": "icmp"
          },
          {
            "ip_is_private": true
          }
        ],
        "outbound": "🪢 本地直连"
      },
      {
        "type": "logical",
        "mode": "or",
        "rules": [{
            "port": 853
          },
          {
            "network": "udp",
            "port": 443
          },
          {
            "protocol": "stun"
          }
        ],
        "action": "reject"
      },
      {
        "rule_set": "Site-🛑 Ads All",
        "action": "reject"
      },
      {
        "clash_mode": "🪡 全局直连",
        "outbound": "🪢 本地直连"
      },
      {
        "clash_mode": "🍀 全局代理",
        "outbound": "☘️ 默认"
      },
      {
        "domain_regex": "^(.*\\.)?(pool\\.ntp|storage\\.live|files\\.1drv)(\\..*)?$",
        "outbound": "🪢 本地直连"
      },
      {
        "rule_set": "APP-🇨🇳 China",
        "outbound": "🪢 本地直连"
      },
      {
        "rule_set": "Site-💵 HSBC",
        "outbound": "💵 汇丰香港"
      },
      {
        "rule_set": "Site-🪙 日游币安SIM",
        "outbound": "🪙 日游币安SIM"
      },
      {
        "rule_set": "Site-✈️ 电报油管",
        "outbound": "✈️ 电报油管"
      },
      {
        "rule_set": "Site-🇨🇳 China",
        "outbound": "🪢 本地直连"
      },
      {
        "type": "logical",
        "mode": "and",
        "rules": [{
            "rule_set": "IP-🇨🇳 China"
          },
          {
            "rule_set": "Site-🌐 !China",
            "invert": true
          }
        ],
        "outbound": "🪢 本地直连"
      }
    ],
    "rule_set": [{
        "tag": "Site-🛑 Ads All",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/217heidai/adblockfilters/main/rules/adblocksingbox.srs"
      },
      {
        "tag": "Site-🇨🇳 China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-geolocation-cn.srs"
      },
      {
        "tag": "IP-🇨🇳 China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geoip/rule-set/geoip-cn.srs"
      },
      {
        "tag": "Site-🌐 !China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-geolocation-!cn.srs"
      },
      {
        "type": "inline",
        "tag": "Site-💵 HSBC",
        "rules": [{
            "package_name_regex": "^(.*\\.)?hsbc[a-z-]*(\\..*)?$"
          },
          {
            "domain_regex": "^(?:.*\\.)?hsbc(?:[a-z-]*\\.[a-z.]+)?$"
          }
        ]
      },
      {
        "type": "inline",
        "tag": "Site-✈️ 电报油管",
        "rules": [{
            "package_name_regex": "^.+\\.(?:telegram\\..+|youtube)$"
          },
          {
            "domain_regex": [
              "^(?:.*\\.)?(?:cdn-telegram|telegram[a-z-]*|(?:wide-|with)?youtube[a-z-]*)\\.[a-z.]+$",
              "^(?:.*\\.)?(?:comments\\.app|contest\\.com|fragment\\.com|ggpht\\.[a-z.]+|googlevideo\\.com|graph\\.org|quiz\\.directory|t\\.me|tdesktop\\.com|telega\\.one|telegra\\.ph|telesco\\.pe|tg\\.dev|ton\\.org|tx\\.me|usercontent\\.dev|youtu\\.be|yt\\.be|yt3\\.googleusercontent\\.com|ytimg\\.com)$"
            ]
          }
        ]
      },
      {
        "type": "inline",
        "tag": "Site-🪙 日游币安SIM",
        "rules": [{
            "package_name_regex": [
              "^(.*\\.)?(talkatone|binance|konami|co\\.ponos)(\\..*)?$"
            ]
          },
          {
            "domain_regex": [
              "^(?:.*\\.)?(?:1inch|aave|arbitrum|arweave|avax|binance|bitcoin|bitget|bnb|bsc|bybit|cetus|coin|compound|crypto|curve|dapp|defi|deribit|dydx|eos|eth|filecoin|ftx|gate|gemini|heco|huobi|kraken|kucoin|maker|mexc|nft|okex|okx|optimism|pancake|poloniex|solana|sui|sushi|synthetix|tether|tron|uniswap|wallet|zksync)[a-z0-9-]*\\.[a-z.]+$",
              "^(?:.*\\.)?(?:block|chain|dex|pool|scan|swap|token|trade)[a-z0-9-]*\\.(?:com|io|net|org|cc|co|fi|xyz|app|pro|network|finance|exchange|zone)$",
              "^(?:.*\\.)?(?:ably|abs|acinq|aex|agkn|aimoon|alphafi|ans-stats|appsflayer|apy999|ardrive|asproex|bibox|bisq|cbeci|cex|chippay|circle|clearpool|cohere|crashlytics|crunchbase|cyberx|dcabtc|debank|digiconomist|dovemetrics|dropsearn|duneanalytics|earni|ewa|flashbots|fragment|glassnode|hbabit|icodrops|inmobi|inner-active|intotheblock|ip-api|ipfs|jaxx|kochava|korbit|liquid|llama|maple|masternodes|mdex|mobilefuse|nansen|navi|nexo|nexus|nonfungible|nyctale|onekey|osl|parity|paxful|phantom|raydium|save|siftscience|slush|sm|sns|stateofthedapps|sunswap|talkatone|tenor|theblock|thegraph|thetie|tktn|traderjoexyz|tradingview|trustwallet|unisat|vfat|viewbase|vitalik|volo|walrus|watchtheburn|wbtc|wynd|zapper|zb)\\.[a-z.]+$",
              "^(?:.*\\.)?konami(?:\\.[a-z.]+)?$",
              "^.*\\.(?:amazonaws\\.com|cloudfront\\.net|myqcloud\\.com|forter\\.com|amazontrust\\.com|codefi\\.network)$"
            ]
          }
        ]
      },
      {
        "type": "inline",
        "tag": "APP-🇨🇳 China",
        "rules": [{
            "package_name_regex": [
              "^(?:cn\\.com\\.|cn\\.gov\\.|cn\\.|com\\.|net\\.|tv\\.|space\\.|me\\.|andes\\.)(?:ai|alibaba|aliyun|amap|autonavi|baidu|bankcomm|benqu|bsp|bytedance|cebbank|chinamworld|chinatelecom|chinaums|chsi|cib|cmb|cmbc|cmbchina|cmcc|codoon|coloros|ct|cyberIdentity|danmaku|deepseek|duokan|easyinvoice|ecitic|eg|eusoft|evecom|fido|finshell|gacne|gov|greenpoint|hhbpay|hl|huaxiaozhu|icbc|idaodan|ifeng|intsig|jingdong|kuaishou|lalamove|larus|lbe|lemon|mfashiongallery|mi|miaotui|milink|mipay|miui|mobiletools|MobileTicket|mxtech|nearme|netease|oplus|opos|oppo|pa|pingan|qihoo|sankuai|sdu|sgcc|sina|smile|sohu|ss|st|taobao|ted|tmri|twx|unionpay|wapi|wps|xiaomi|ximalaya|xingin|xinzhi|xmgov|xunmeng|yitong|zhaopin|zhihu|zhouzhuo810)(?:\\..+)?$",
              "^com\\.tencent\\.(?:android|hunyuan|mm|mobileqq|soter|wemeet)(?:\\..+)?$",
              "^com\\.heytap\\.(?:accessory|cloud|htms|market|mcs|member|music|mydevices|openid|opluscarlink|pictorial|quicksearchbox|reader|speechassist|tas|themestore|yoli)$",
              "^(?:android|oplus|com\\.haixia|com\\.newcall|com\\.Qunar|com\\.unionpay|com\\.icbc|ctrip\\.android\\..+|miui\\..+)$",
              "^com\\.android\\.(?:bankabc|bips|bluetooth|calendar|camera|cellbroadcastservice|contacts|deskclock|DeviceAsWebcam|dynsystem|email|fileexplorer|htmlviewer|incallui|inputdevices|intentresolver|keychain|launcher|localtransport|location\\.fused|mms(?:\\.service)?|nfc|ons|packageinstaller|phone|photopicker|printspooler|providers\\.(?:calendar|settings|telephony)|provision|quicksearchbox|server\\.telecom|settings|soundrecorder|stk|systemui|thememanager|updater|wallpaper\\.livepicker)$",
              "^(?:com\\.qti\\.(?:dpmserviceapp|qualcomm\\..+)|com\\.qualcomm\\.(?:atfwd|location|qti\\.(?:dynamicddsservice|services\\.systemhelper|uceShimService|xrvd\\.service))|vendor\\.qti\\.(?:data\\.ntnsatapp|frameworks\\.utils|imsdatachannel))$"
            ]
          },
          {
            "process_path_regex": "(?i)^(.*[\\\\/])?(Tencent|Alibaba|Baidu|NetEase|ByteDance|Kingsoft|360|Xunlei|Thunder Network|Sogou|iQIYI|Bilibili|DingTalk|Youku|Kugou|Kuwo)([\\\\/].*)?$"
          }
        ]
      }
    ]
  }
}
```

Sub-Store 节点插入脚本

```
log(`🚀 开始`)

let type, name, outbound, includeUnsupportedProxy
type = "组合订阅"
name = "mofa"
outbound = "🕳ℹ️🇨🇳 港澳台🏷ℹ️🇭🇰|🇲🇴|🇹🇼🕳ℹ️🇯🇵 日本🏷ℹ️🇯🇵🕳ℹ️🇺🇸 美国🏷ℹ️🇺🇸🕳ℹ️🇺🇳 全部🕳ℹ️🐉 测速"

log(`传入参数 type: ${type}, name: ${name}, outbound: ${outbound}`)

type = /^1$|col|组合/i.test(type) ? 'collection' : 'subscription'

log(`① 解析配置文件`)
let config
try {
  config = JSON.parse($content ?? $files[0])
} catch (e) {
  log(`${e.message ?? e}`)
  throw new Error('配置文件不是合法的 JSON')
}
log(`② 获取订阅`)
log(`将读取名称为 ${name} 的 ${type === 'collection' ? '组合' : ''}订阅`)
let proxies = await produceArtifact({
  name,
  type,
  platform: 'sing-box',
  produceType: 'internal',
  produceOpts: {
    'include-unsupported-proxy': includeUnsupportedProxy,
  },
})
log(`③ outbound 规则解析`)
const outbounds = outbound
  .split('🕳')
  .filter(i => i)
  .map(i => {
    let [outboundPattern, tagPattern = '.*'] = i.split('🏷')
    const tagRegex = createTagRegExp(tagPattern)
    log(`匹配 🏷 ${tagRegex} 的节点将插入匹配 🕳 ${createOutboundRegExp(outboundPattern)} 的 outbound 中`)
    return [outboundPattern, tagRegex]
  })

log(`④ outbound 插入节点`)
config.outbounds.map(outbound => {
  outbounds.map(([outboundPattern, tagRegex]) => {
    const outboundRegex = createOutboundRegExp(outboundPattern)
    if (outboundRegex.test(outbound.tag)) {
      if (!Array.isArray(outbound.outbounds)) {
        outbound.outbounds = []
      }
      const tags = getTags(proxies, tagRegex)
      log(`🕳 ${outbound.tag} 匹配 ${outboundRegex}, 插入 ${tags.length} 个 🏷 匹配 ${tagRegex} 的节点`)
      outbound.outbounds.push(...tags)
    }
  })
})

const compatible_outbound = {
  tag: 'COMPATIBLE',
  type: 'direct',
}

let compatible
log(`⑤ 空 outbounds 检查`)
config.outbounds.map(outbound => {
  outbounds.map(([outboundPattern, tagRegex]) => {
    const outboundRegex = createOutboundRegExp(outboundPattern)
    if (outboundRegex.test(outbound.tag)) {
      if (!Array.isArray(outbound.outbounds)) {
        outbound.outbounds = []
      }
      if (outbound.outbounds.length === 0) {
        if (!compatible) {
          config.outbounds.push(compatible_outbound)
          compatible = true
        }
        log(`🕳 ${outbound.tag} 的 outbounds 为空, 自动插入 COMPATIBLE(direct)`)
        outbound.outbounds.push(compatible_outbound.tag)
      }
    }
  })
})

config.outbounds.push(...proxies)

$content = JSON.stringify(config, null, 2)

function getTags(proxies, regex) {
  return (regex ? proxies.filter(p => regex.test(p.tag)) : proxies).map(p => p.tag)
}

function log(v) {
  console.log(`[📦 sing-box 模板脚本] ${v}`)
}

function createTagRegExp(tagPattern) {
  return new RegExp(tagPattern.replace('ℹ️', ''), tagPattern.includes('ℹ️') ? 'i' : undefined)
}

function createOutboundRegExp(outboundPattern) {
  return new RegExp(outboundPattern.replace('ℹ️', ''), outboundPattern.includes('ℹ️') ? 'i' : undefined)
}

log(`🔚 结束`)
```

Sub-Store 脚本 非 ASCII 字符，强制替换为标准 JSON 转义符 (\uXXXX)

```
let text = $content ?? "";

try {
  let json = JSON.parse(text);
  let jsonString = JSON.stringify(json, null, 2);

  let asciiString = jsonString.replace(/[^\x00-\x7F]/g, function(char) {
    return "\\u" + ("0000" + char.charCodeAt(0).toString(16).toUpperCase()).slice(-4);
  });

  $content = asciiString;

} catch (error) {
  console.log("❌ 脚本执行失败: " + error);
  $content = text;
}
```
