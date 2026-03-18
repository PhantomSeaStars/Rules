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
      },
```

参考配置

```
{
  "log": {
    "disabled": false,
    "level": "warn",
    "timestamp": true
  },
  "experimental": {
    "cache_file": {
      "enabled": true,
      "store_fakeip": false,
      "store_rdrc": true
    },
    "clash_api": {
      "external_controller": "127.0.0.1:9090",
      "external_ui": "WebUI",
      "default_mode": "🕊 规则分流"
    }
  },
  "dns": {
    "strategy": "ipv4_only",
    "disable_cache": false,
    "disable_expire": false,
    "independent_cache": false,
    "cache_capacity": 0,
    "reverse_mapping": false,
    "servers": [{
        "type": "tls",
        "tag": "🌱 代理DNS",
        "server": "dns.google",
        "detour": "🐦‍🔥 代理DNS出口"
      },
      {
        "type": "quic",
        "tag": "🧶 直连DNS",
        "server": "dns.alidns.com",
        "domain_resolver": "local"
      },
      {
        "type": "local",
        "tag": "local"
      },
      {
        "type": "hosts",
        "tag": "🎭 Hosts",
        "predefined": {
          "git.web.work": "000.111.222.333",
          "openlist.web.work": "000.111.222.333",
          "sub-store.web.work": "000.111.222.333",
          "hkx-ui.web.work": "000.111.222.333",
          "jpx-ui.web.work": "000.111.222.333",
          "usx-ui.web.work": "000.111.222.333",
          
          "hkmagic.web.work": "000.111.222.333",
          "jpmagic.web.work": "111.222.333.444",
          "usmagic.web.work": "222.333.444.555"
        }
      }
    ],
    "rules": [{
        "ip_accept_any": true,
        "server": "🎭 Hosts"
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
        "rule_set": "APP-🌐 !China",
        "server": "🌱 代理DNS"
      },
      {
        "rule_set": "APP-🇨🇳 China",
        "server": "🧶 直连DNS"
      },
      {
        "rule_set": [
          "site-📞 Talkatone",
          "site-💵 HSBC",
          "site-🎮 Category Games",
          "site-🎮 Dmm",
          "site-📝 Bahamut",
          "site-🍎 Apple",
          "site-🛒 Amazon",
          "site-▶️ YouTube",
          "site-🔍 Google",
          "site-🎵 TikTok",
          "site-🪙 Binance",
          "site-✈️ Telegram",
          "site-𝕏 Twitter",
          "site-👤 Facebook",
          "site-🤖 Openai",
          "site-☁️ OneDrive",
          "site-⌨️ GitHub",
          "site-💠 Microsoft",
          "site-🇳 Netflix",
          "site-🐭 Disney+",
          "site-💻 HBO",
          "site-💻 PrimeVideo",
          "site-🎼 Spotify"
        ],
        "server": "🌱 代理DNS"
      },
      {
        "rule_set": [
          "site-🐧 Tencent",
          "site-💰 Alibaba",
          "site-📺 Bilibili"
        ],
        "server": "🧶 直连DNS"
      },
      {
        "rule_set": "site-🇨🇳 China",
        "server": "🧶 直连DNS"
      },
      {
        "type": "logical",
        "mode": "and",
        "rules": [{
            "rule_set": "site-🌐 !China",
            "invert": true
          },
          {
            "rule_set": "IP-🇨🇳 China"
          }
        ],
        "server": "🌱 代理DNS",
        "client_subnet": "1.80.0.0/13"
      }
    ]
  },
  "inbounds": [{
      "type": "tun",
      "tag": "🚀 1-13",
      "interface_name": "🚀 1-13",
      "address": [
        "172.18.0.1/30",
        "fdfe:dcba:9876::1/126"
      ],
      "mtu": 1500,
      "auto_route": true,
      "loopback_address": [
        "10.7.0.1"
      ],
      "strict_route": true,
      "route_address": [
        "0.0.0.0/1",
        "128.0.0.0/1"
      ],
      "route_exclude_address": [
        "192.168.0.0/16",
        "fc00::/7"
      ],
      "endpoint_independent_nat": false,
      "stack": "mixed"
    },
    {
      "type": "mixed",
      "tag": "♻️ 局域网流转",
      "listen": "0.0.0.0",
      "listen_port": 5353
    }
  ],
  "outbounds": [{
      "type": "selector",
      "tag": "☘️ 默认",
      "outbounds": ["🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇺🇸 美国"
    },
    {
      "type": "selector",
      "tag": "🎣 漏网之鱼",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🐦‍🔥 代理DNS出口",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🇨🇳 港澳台",
      "outbounds": ["🇭🇰 TRI 九龙🪢"]
    },
    {
      "type": "selector",
      "tag": "🇺🇸 美国",
      "outbounds": ["🇺🇸 4837 洛杉矶🪢"]
    },
    {
      "type": "selector",
      "tag": "🇯🇵 日本",
      "outbounds": ["🇯🇵 TRI 千叶♻️🇨🇳", "🇯🇵 INTL 千叶🪢"]
    },
    {
      "type": "selector",
      "tag": "🇺🇳 全部",
      "outbounds": ["🇭🇰 TRI 九龙🪢", "🇯🇵 TRI 千叶♻️🇨🇳", "🇯🇵 INTL 千叶🪢", "🇺🇸 4837 洛杉矶🪢"]
    },
    {
      "type": "selector",
      "tag": "🌕 云服务器",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🪢 直连"
    },
    {
      "type": "selector",
      "tag": "💵 汇丰香港",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇨🇳 港澳台"
    },
    {
      "type": "selector",
      "tag": "🎮 Games",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇯🇵 日本"
    },
    {
      "type": "selector",
      "tag": "📝 Bahamut",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇨🇳 港澳台"
    },
    {
      "type": "selector",
      "tag": "🪙 Binance",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇯🇵 日本"
    },
    {
      "type": "selector",
      "tag": "📞 Talkatone",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇯🇵 日本"
    },
    {
      "type": "selector",
      "tag": "🐧 Tencent",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🪢 直连"
    },
    {
      "type": "selector",
      "tag": "✈️ Telegram",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇺🇸 美国"
    },
    {
      "type": "selector",
      "tag": "𝕏 Twitter",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇺🇸 美国"
    },
    {
      "type": "selector",
      "tag": "👤 Facebook",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇺🇸 美国"
    },
    {
      "type": "selector",
      "tag": "🤖 Openai",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "💰 Alibaba",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🪢 直连"
    },
    {
      "type": "selector",
      "tag": "🍎 Apple",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🛒 Amazon",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "☁️ OneDrive",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "⌨️ GitHub",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "💠 Microsoft",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🍿 EMBY",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "📺 Bilibili",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🪢 直连"
    },
    {
      "type": "selector",
      "tag": "▶️ YouTube",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇺🇸 美国"
    },
    {
      "type": "selector",
      "tag": "🎵 TikTok",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🇳 Netflix",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🐭 Disney+",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "💻 Streaming",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "selector",
      "tag": "🔍 Google",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"],
      "default": "🇯🇵 日本"
    },
    {
      "type": "selector",
      "tag": "🎼 Spotify",
      "outbounds": ["☘️ 默认", "🇨🇳 港澳台", "🇯🇵 日本", "🇺🇸 美国", "🇺🇳 全部", "🪢 直连"]
    },
    {
      "type": "urltest",
      "tag": "🐉 测速",
      "outbounds": ["🇭🇰 TRI 九龙🪢", "🇯🇵 TRI 千叶♻️🇨🇳", "🇯🇵 INTL 千叶🪢", "🇺🇸 4837 洛杉矶🪢"],
      "interval": "1m"
    },
    {
      "type": "direct",
      "tag": "🪢 直连"
    },
    {
      "tag": "🇺🇸 4837 洛杉矶🪢",
      "type": "anytls",
      "server": "usmagic.web.work",
      "server_port": 443,
      "password": "EiRuU4dB5WXE",
      "tls": {
        "enabled": true,
        "server_name": "sni.com",
        "insecure": false,
        "reality": {
          "enabled": true,
          "public_key": "o9ufMePV5OcTKAeNnTXr26k8A1Xf7Ju8iSUDBW3Oxg",
          "short_id": "f2145df6455660"
        },
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        }
      },
      "domain_resolver": "🎭 Hosts"
    },
    {
      "tag": "🇯🇵 INTL 千叶🪢",
      "type": "anytls",
      "server": "jpmagic.web.work",
      "server_port": 443,
      "password": "EiRuU4dB5WXE",
      "tls": {
        "enabled": true,
        "server_name": "www.sni.jp",
        "insecure": false,
        "reality": {
          "enabled": true,
          "public_key": "o9ufMePV5OcTKAeNnTXr26k8A1Xf7Ju8iSUDBW3Oxg",
          "short_id": "f2145df6455660"
        },
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        }
      },
      "domain_resolver": "🎭 Hosts"
    },
    {
      "tag": "🇯🇵 TRI 千叶♻️🇨🇳",
      "type": "shadowsocks",
      "server": "111.222.333.444",
      "server_port": 10001,
      "method": "2022-blake3-chacha20-poly1305",
      "password": "3oDzoXlMK2Vr1zFc0ZfxMBsJPhmy2ukQQIeW1ypF6s=",
      "detour": "🇭🇰 TRI 九龙🪢"
    },
    {
      "tag": "🇭🇰 TRI 九龙🪢",
      "type": "anytls",
      "server": "hkmagic.web.work",
      "server_port": 443,
      "password": "EiRuU4dB5WXE",
      "tls": {
        "enabled": true,
        "server_name": "kuaileshe5.top",
        "insecure": false,
        "reality": {
          "enabled": true,
          "public_key": "o9ufMePV5OcTKAeNnTXr26k8A1Xf7Ju8iSUDBW3Oxg",
          "short_id": "f2145df6455660"
        },
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        }
      },
      "domain_resolver": "🎭 Hosts"
    }
  ],
  "route": {
    "final": "🎣 漏网之鱼",
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
        "ip_is_private": true,
        "outbound": "🪢 直连"
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
        "rule_set": "site-🛑 Ads All",
        "method": "drop",
        "action": "reject"
      },
      {
        "clash_mode": "🪡 全局直连",
        "outbound": "🪢 直连"
      },
      {
        "clash_mode": "🍀 全局代理",
        "outbound": "☘️ 默认"
      },
      {
        "package_name": "com.talkatone.android",
        "outbound": "📞 Talkatone"
      },
      {
        "domain_suffix": "web.work",
        "outbound": "🌕 云服务器"
      },
      {
        "ip_cidr": "154.44.21.0/24",
        "outbound": "🌕 云服务器"
      },
      {
        "ip_cidr": "163.61.207.0/24",
        "outbound": "🌕 云服务器"
      },
      {
        "ip_cidr": "38.175.193.0/24",
        "outbound": "🌕 云服务器"
      },
      {
        "package_name": "hk.com.hsbc.hsbchkmobilebanking",
        "outbound": "💵 汇丰香港"
      },
      {
        "domain_suffix": "storage.live.com",
        "outbound": "🪢 直连"
      },
      {
        "domain_suffix": "files.1drv.com",
        "outbound": "🪢 直连"
      },
      {
        "package_name": "jp.konami.masterduel",
        "outbound": "🎮 Games"
      },
      {
        "package_name": "jp.konami.YugiohOcgSupports",
        "outbound": "🎮 Games"
      },
      {
        "package_name": "jp.co.ponos.battlecatstw",
        "outbound": "🎮 Games"
      },
      {
        "process_name": "steamwebhelper.exe",
        "outbound": "🎮 Games"
      },
      {
        "process_name": "steam.exe",
        "outbound": "🎮 Games"
      },
      {
        "process_name": "steamservice.exe",
        "outbound": "🎮 Games"
      },
      {
        "process_name": "masterduel.exe",
        "outbound": "🎮 Games"
      },
      {
        "domain_suffix": "konami.com",
        "outbound": "🎮 Games"
      },
      {
        "domain_suffix": "konami.net",
        "outbound": "🎮 Games"
      },
      {
        "package_name": "com.tencent.mm",
        "outbound": "🐧 Tencent"
      },
      {
        "package_name": "com.tencent.mobileqq",
        "outbound": "🐧 Tencent"
      },
      {
        "package_name": "com.tencent.wework",
        "outbound": "🐧 Tencent"
      },
      {
        "process_name": "Weixin.exe",
        "outbound": "🐧 Tencent"
      },
      {
        "process_name": "QQ.exe",
        "outbound": "🐧 Tencent"
      },
      {
        "process_name": "WXWork.exe",
        "outbound": "🐧 Tencent"
      },
      {
        "package_name": "com.taobao.taobao",
        "outbound": "💰 Alibaba"
      },
      {
        "package_name": "com.eg.android.AlipayGphone",
        "outbound": "💰 Alibaba"
      },
      {
        "package_name": "com.amazon.mShop.android.shopping",
        "outbound": "🛒 Amazon"
      },
      {
        "package_name": "cn.amazon.mShop.android",
        "outbound": "🛒 Amazon"
      },
      {
        "process_name": "electron.exe",
        "outbound": "🍿 EMBY"
      },
      {
        "process_name": "TerminusPlayer.exe",
        "outbound": "🍿 EMBY"
      },
      {
        "process_name": "Emby.Theater.exe",
        "outbound": "🍿 EMBY"
      },
      {
        "process_name": "EmbyServer.exe",
        "outbound": "🍿 EMBY"
      },
      {
        "process_name": "embytray.exe",
        "outbound": "🍿 EMBY"
      },
      {
        "process_name": "QtWebEngineProcess.exe",
        "outbound": "🍿 EMBY"
      },
      {
        "package_name": "com.mb.android",
        "outbound": "🍿 EMBY"
      },
      {
        "package_name": "tv.danmaku.bili",
        "outbound": "📺 Bilibili"
      },
      {
        "package_name": "com.google.android.youtube",
        "outbound": "▶️ YouTube"
      },
      {
        "package_name": "com.google.android.apps.bard",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.apps.labs.language.tailwind",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.android.vending",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.gms",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.gsf",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.googlequicksearchbox",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.gm",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.apps.authenticator2",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.inputmethod.latin",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.apps.translate",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.google.android.apps.nbu.files",
        "outbound": "🔍 Google"
      },
      {
        "package_name": "com.zhiliaoapp.musically",
        "outbound": "🎵 TikTok"
      },
      {
        "package_name": "com.binance.dev",
        "outbound": "🪙 Binance"
      },
      {
        "package_name": "mega.privacy.android.app",
        "outbound": "✈️ Telegram"
      },
      {
        "package_name": "org.telegram.messenger",
        "outbound": "✈️ Telegram"
      },
      {
        "package_name": "com.twitter.android",
        "outbound": "𝕏 Twitter"
      },
      {
        "package_name": "com.facebook.katana",
        "outbound": "👤 Facebook"
      },
      {
        "package_name": "com.openai.chatgpt",
        "outbound": "🤖 Openai"
      },
      {
        "package_name": "com.microsoft.skydrive",
        "outbound": "☁️ OneDrive"
      },
      {
        "package_name": "com.microsoft.office.outlook",
        "outbound": "💠 Microsoft"
      },
      {
        "package_name": "com.microsoft.office.officehubrow",
        "outbound": "💠 Microsoft"
      },
      {
        "rule_set": "site-💵 HSBC",
        "outbound": "💵 汇丰香港"
      },
      {
        "rule_set": "site-📞 Talkatone",
        "outbound": "📞 Talkatone"
      },
      {
        "rule_set": "IP-📞 Talkatone",
        "outbound": "📞 Talkatone"
      },
      {
        "rule_set": "site-🎮 Category Games",
        "outbound": "🎮 Games"
      },
      {
        "rule_set": "site-🎮 Dmm",
        "outbound": "🎮 Games"
      },
      {
        "rule_set": "site-📝 Bahamut",
        "outbound": "📝 Bahamut"
      },
      {
        "rule_set": "site-🐧 Tencent",
        "outbound": "🐧 Tencent"
      },
      {
        "rule_set": "site-💰 Alibaba",
        "outbound": "💰 Alibaba"
      },
      {
        "rule_set": "site-🍎 Apple",
        "outbound": "🍎 Apple"
      },
      {
        "rule_set": "site-🛒 Amazon",
        "outbound": "🛒 Amazon"
      },
      {
        "rule_set": "site-📺 Bilibili",
        "outbound": "📺 Bilibili"
      },
      {
        "rule_set": "site-▶️ YouTube",
        "outbound": "▶️ YouTube"
      },
      {
        "rule_set": "site-🔍 Google",
        "outbound": "🔍 Google"
      },
      {
        "rule_set": "site-🎵 TikTok",
        "outbound": "🎵 TikTok"
      },
      {
        "rule_set": "site-🪙 Binance",
        "outbound": "🪙 Binance"
      },
      {
        "rule_set": "site-✈️ Telegram",
        "outbound": "✈️ Telegram"
      },
      {
        "rule_set": "site-𝕏 Twitter",
        "outbound": "𝕏 Twitter"
      },
      {
        "rule_set": "site-👤 Facebook",
        "outbound": "👤 Facebook"
      },
      {
        "rule_set": "site-🤖 Openai",
        "outbound": "🤖 Openai"
      },
      {
        "rule_set": "site-☁️ OneDrive",
        "outbound": "☁️ OneDrive"
      },
      {
        "rule_set": "site-⌨️ GitHub",
        "outbound": "⌨️ GitHub"
      },
      {
        "rule_set": "site-💠 Microsoft",
        "outbound": "💠 Microsoft"
      },
      {
        "rule_set": "site-🇳 Netflix",
        "outbound": "🇳 Netflix"
      },
      {
        "rule_set": "site-🐭 Disney+",
        "outbound": "🐭 Disney+"
      },
      {
        "rule_set": "site-💻 HBO",
        "outbound": "💻 Streaming"
      },
      {
        "rule_set": "site-💻 PrimeVideo",
        "outbound": "💻 Streaming"
      },
      {
        "rule_set": "site-🎼 Spotify",
        "outbound": "🎼 Spotify"
      },
      {
        "rule_set": "APP-🇨🇳 China",
        "outbound": "🪢 直连"
      },
      {
        "rule_set": "APP-🌐 !China",
        "outbound": "☘️ 默认"
      },
      {
        "rule_set": "site-🇨🇳 China",
        "outbound": "🪢 直连"
      },
      {
        "type": "logical",
        "mode": "and",
        "rules": [{
            "rule_set": "IP-🇨🇳 China"
          },
          {
            "rule_set": "site-🌐 !China",
            "invert": true
          }
        ],
        "outbound": "🪢 直连"
      }
    ],
    "rule_set": [{
        "tag": "site-🛑 Ads All",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-category-ads-all.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🎵 TikTok",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-tiktok.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🎮 Category Games",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-category-games.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🎮 Dmm",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-dmm.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-📝 Bahamut",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-bahamut.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🐧 Tencent",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-tencent.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-✈️ Telegram",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-telegram.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-𝕏 Twitter",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-twitter.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-👤 Facebook",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-facebook.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🤖 Openai",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-openai.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-💰 Alibaba",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-alibaba.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🍎 Apple",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-apple.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🛒 Amazon",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-amazon.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-☁️ OneDrive",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-onedrive.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-💠 Microsoft",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-microsoft.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-⌨️ GitHub",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-github.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-📺 Bilibili",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-bilibili.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-▶️ YouTube",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-youtube.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🇳 Netflix",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-netflix.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🐭 Disney+",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-disney.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-💻 HBO",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-hbo.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-💻 PrimeVideo",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-primevideo.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🔍 Google",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-google.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🎼 Spotify",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-spotify.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "IP-🇨🇳 China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geoip/rule-set/geoip-cn.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🇨🇳 China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-geolocation-cn.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🌐 !China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/SagerNet/sing-geosite/rule-set/geosite-geolocation-!cn.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-🪙 Binance",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/geosite-binance.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-💵 HSBC",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/geosite-hsbc.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "site-📞 Talkatone",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/geosite-talkatone.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "IP-📞 Talkatone",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/geoip-talkatone.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "APP-🇨🇳 China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/app-geolocation-cn.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
      },
      {
        "tag": "APP-🌐 !China",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/PhantomSeaStars/Rules/main/app-geolocation-!cn.srs",
        "download_detour": "🇭🇰 TRI 九龙🪢"
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
