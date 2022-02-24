port: 7890
socks-port: 7891
allow-lan: false
mode: Rule
log-level: info
external-controller: :9090
proxies:
  - {name: 1, server: 172.99.190.188, port: 2375, type: ss, cipher: aes-256-gcm, password: faBAoD54k87UJG7, udp: true}
  - {name: 2, server: 134.195.196.193, port: 7307, type: ss, cipher: aes-256-gcm, password: FoOiGlkAA9yPEGP, udp: true}
  - {name: 3, server: 169.197.141.91, port: 6379, type: ss, cipher: aes-256-gcm, password: zDNVedRFPQexG9v, udp: true}
  - {name: 4, server: 172.99.190.188, port: 7306, type: ss, cipher: aes-256-gcm, password: FoOiGlkAA9yPEGP, udp: true}
proxy-groups:
  - name: 节点选择
    type: select
    proxies:
      - 自动选择
      - 不使用代理(直连)
      - 1
      - 2
      - 3
      - 4
  - name: 自动选择
    type: url-test
    url: http://www.gstatic.com/generate_204
    interval: 1000
    proxies:
      - 1
      - 2
      - 3
      - 4
  - name: 不使用代理(直连)
    type: select
    proxies:
      - DIRECT
      
rules:
 - DOMAIN-SUFFIX,bilibili.com,DIRECT
 - DOMAIN-SUFFIX,yuketang.cn,DIRECT
 - GEOIP,CN,DIRECT
 - MATCH,节点选择

    
