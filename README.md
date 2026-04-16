使用方法

```
      {
        "tag": "site-📞 Talkatone",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/geosite-talkatone.srs",
        "download_detour": "☘️ 默认"
      },
      {
        "tag": "IP-📞 Talkatone",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/geoip-talkatone.srs",
        "download_detour": "☘️ 默认"
      }
```

基于sing-box-1.14.0-alpha.12的参考配置。

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
        "domain_suffix": "私有域名.work",
        "action": "predefined",
        "answer": "*.私有域名.work. IN A 私有IP"
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
        "rule_set": "V5-🇨🇳 ChinaAPP",
        "server": "🧶 直连DNS"
      },
      {
        "rule_set": "Site-🇨🇳 China",
        "server": "🧶 直连DNS"
      },
      {
        "rule_set": "Site-🌐 Global",
        "invert": true,
        "action": "evaluate",
        "server": "🌱 代理DNS",
        "client_subnet": "1.80.0.0/13"
      },
      {
        "type": "logical",
        "mode": "and",
        "rules": [{
            "rule_set": "Site-🌐 Global",
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
      "type": "anytls",
      "server": "私有IP",
      "min_idle_session": 4,
      "udp_fragment": true,
      "server_port": 443,
      "password": "用户名",
      "tls": {
        "enabled": true,
        "server_name": "SNI",
        "alpn": ["h2", "http/1.1"],
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        },
        "reality": {
          "enabled": true,
          "public_key": "密钥",
          "short_id": "ID"
        }
      }
    },
    {
      "tag": "🇭🇰 TRI 九龙2🪢",
      "type": "anytls",
      "server": "私有IP",
      "min_idle_session": 4,
      "udp_fragment": true,
      "server_port": 443,
      "password": "用户名",
      "tls": {
        "enabled": true,
        "server_name": "SNI",
        "alpn": ["h2", "http/1.1"],
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        },
        "reality": {
          "enabled": true,
          "public_key": "密钥",
          "short_id": "ID"
        }
      }
    },
    {
      "tag": "🇺🇸 4837 洛杉矶🪢",
      "type": "anytls",
      "server": "私有IP",
      "min_idle_session": 4,
      "udp_fragment": true,
      "server_port": 443,
      "password": "用户名",
      "tls": {
        "enabled": true,
        "server_name": "SNI",
        "alpn": ["h2", "http/1.1"],
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        },
        "reality": {
          "enabled": true,
          "public_key": "密钥",
          "short_id": "ID"
        }
      }
    },
    {
      "tag": "🇺🇸 TRI 洛杉矶♻️",
      "type": "shadowsocks",
      "server": "私有IP",
      "server_port": 20000,
      "method": "2022-blake3-aes-128-gcm",
      "password": "密钥",
      "tcp_fast_open": true,
      "udp_fragment": true,
      "multiplex": {
        "enabled": true,
        "max_connections": 4,
        "min_streams": 4
      },
      "detour": "♻️ 中转选择"
    },
    {
      "tag": "🇯🇵 INTL 千叶🪢",
      "type": "anytls",
      "server": "私有IP",
      "min_idle_session": 4,
      "udp_fragment": true,
      "server_port": 443,
      "password": "用户名",
      "tls": {
        "enabled": true,
        "server_name": "SNI",
        "alpn": ["h2", "http/1.1"],
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        },
        "reality": {
          "enabled": true,
          "public_key": "密钥",
          "short_id": "ID"
        }
      }
    },
    {
      "tag": "🇯🇵 TRI 千叶♻️",
      "type": "shadowsocks",
      "server": "私有IP",
      "server_port": 20000,
      "method": "2022-blake3-aes-128-gcm",
      "password": "密钥",
      "tcp_fast_open": true,
      "udp_fragment": true,
      "multiplex": {
        "enabled": true,
        "max_connections": 4,
        "min_streams": 4
      },
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
        "clash_mode": "🪡 全局直连",
        "outbound": "🪢 本地直连"
      },
      {
        "clash_mode": "🍀 全局代理",
        "outbound": "☘️ 默认"
      },
      {
        "domain_regex": "^(.*\\.)?(pool\\.ntp|私有域名|storage\\.live|files\\.1drv)(\\..*)?$",
        "outbound": "🪢 本地直连"
      },
      {
        "rule_set": "V5-🎮 K社",
        "outbound": "🪙 日游币安SIM"
      },
      {
        "rule_set": "V5-💵 HSBC",
        "outbound": "💵 汇丰香港"
      },
      {
        "rule_set": "V5-📞 虚拟SIM",
        "outbound": "🪙 日游币安SIM"
      },
      {
        "rule_set": "V5-✈️ 电报",
        "outbound": "✈️ 电报油管"
      },
      {
        "rule_set": "V5-▶️ 油管",
        "outbound": "✈️ 电报油管"
      },
      {
        "rule_set": "V5-🪙 币安",
        "outbound": "🪙 日游币安SIM"
      },
      {
        "rule_set": "V5-🇨🇳 ChinaAPP",
        "outbound": "🪢 本地直连"
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
            "rule_set": "Site-🌐 Global",
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
        "tag": "Site-🌐 Global",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-geolocation-!cn.srs"
      },
      {
        "tag": "V5-💵 HSBC",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-hsbc.srs"
      },
      {
        "tag": "V5-▶️ 油管",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-youtube.srs"
      },
      {
        "tag": "V5-✈️ 电报",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-telegram.srs"
      },
      {
        "tag": "V5-📞 虚拟SIM",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-talkatone.srs"
      },
      {
        "tag": "V5-🪙 币安",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-binance.srs"
      },
      {
        "tag": "V5-🎮 K社",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-konami.srs"
      },
      {
        "tag": "V5-🇨🇳 ChinaAPP",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/私有域名/Rules/main/V5-ChinaAPP.srs"
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
