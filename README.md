{
  "log": {
    "error": "",
    "loglevel": "info",
    "access": ""
  },
  "inbounds": [
    {
      "listen": "127.0.0.1",
      "protocol": "socks",
      "settings": {
        "ip": "",
        "userLevel": 0,
        "timeout": 360,
        "udp": false,
        "auth": "noauth"
      },
      "port": "1080"
    },
    {
      "listen": "127.0.0.1",
      "protocol": "http",
      "settings": {
        "timeout": 360
      },
      "port": "1081"
    }
  ],
  "outbounds": [
    {
      "mux": {
        "enabled": false,
        "concurrency": 8
      },
      "protocol": "vmess",
      "streamSettings": {
        "tcpSettings": {
          "header": {
            "type": "none"
          }
        },
        "tlsSettings": {
          "allowInsecure": false
        },
        "security": "tls",
        "network": "tcp"
      },
      "tag": "agentout",
      "settings": {
        "vnext": [
          {
            "address": "t.zhangjinshuai.com",
            "users": [
              {
                "id": "05595406-060e-4307-9fd9-fe7b01f005f4",
                "alterId": 64,
                "level": 1,
                "security": "auto"
              }
            ],
            "port": 443
          }
        ]
      }
    },
    {
      "tag": "direct",
      "protocol": "freedom",
      "settings": {
        "domainStrategy": "AsIs",
        "redirect": "",
        "userLevel": 0
      }
    },
    {
      "tag": "blockout",
      "protocol": "blackhole",
      "settings": {
        "response": {
          "type": "none"
        }
      }
    }
  ],
  "dns": {
    "servers": [
      ""
    ]
  },
  "routing": {
    "strategy": "rules",
    "settings": {
      "domainStrategy": "IPIfNonMatch",
      "rules": [
        {
          "outboundTag": "direct",
          "type": "field",
          "ip": [
            "geoip:cn",
            "geoip:private"
          ],
          "domain": [
            "geosite:cn",
            "geosite:speedtest"
          ]
        }
      ]
    }
  },
  "transport": {}
}
