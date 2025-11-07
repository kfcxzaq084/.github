{
  "policy": {
    "levels": {
      "0": {
        "handshake": 5,
        "connIdle": 60,
        "uplinkOnly": 5,
        "downlinkOnly": 5,
        "bufferSize": 0
      }
    }
  },
  "inbounds": [
    {
      "port": 1080,
      "listen": "103.234.236.224",
      "protocol": "socks",
      "settings": {
        "udp": false
      },
      "sniffing": {
        "enabled": false,
        "destOverride": []
      },
      "tag": "socks"
    }
  ],
  "outbounds": [
    {
      "protocol": "socks",
      "settings": {
        "servers": [
          {
            "address": "103.234.236.224",
            "port": 80
          }
        ]
      },
      "streamSettings": {
        "security": "tls",
        "tlsSettings": {
          "allowInsecure": true,
          "allowInsecureCiphers": true,
          "serverName": "103-234-236-1.static.bangmod.cloud",
          "fingerprint": "unsafe"
        }
      },
      "tag": "proxy",
      "mux": {
        "enabled": false,
        "concurrency": 8,
        "xudpConcurrency": 8,
        "xudpProxyUDP443": "reject"
      }
    },
    {
      "protocol": "freedom",
      "settings": {
        "domainStrategy": "UseIP"
      },
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "settings": {
        "response": {
          "type": "http"
        }
      },
      "tag": "block"
    }
  ],
  "routing": {
    "domainMatcher": "mph",
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "type": "field",
        "ip": [
          "127.0.0.1"
        ],
        "port": "7300",
        "outboundTag": "proxy"
      }
    ]
  },
  "log": {
    "loglevel": "none",
    "dnsLog": true
  }
}.github