# multi-xray

V2ray/Xray多用戶管理腳本，嚮導式管理[新增|刪除|修改]傳輸協議  
![](https://img.shields.io/pypi/v/v2ray-util.svg) 
![](https://img.shields.io/github/license/Jrohy/multi-v2ray.svg)

## [简体中文](README.md) |[English](README_EN.md) |[正體中文](README_TR.md)

- [x] 修改自[Jrohy](https://github.com/Jrohy)的項目[multi-v2ray](https://github.com/Jrohy/multi-v2ray)

## 特色

- [x] 支持Xray管理, v2ray和xray相互獨立, 不同命令(v2ray/xray)進入不同的core管理
- [x] 直接安裝v2ray（Author:[Jrohy](https://github.com/Jrohy)）/xray（Modify: Radium-bit）
- [x] 調用v2ray官方api進行流量統計
- [x] **多用戶, 多端口管理**, 混合傳輸協議管理不再是夢
- [x] 首次安裝時產生隨機端口，默認配置mkcp + 隨機一種 (srtp | wechat-video | utp | dtls | wireguard) header偽裝;  
   安裝完成顯示配置信息;
- [x] 查看配置信息顯示vmess/vless字符串(v2rayN的分享鏈接格式)
- [x] 生成**Telegram**的socks5/MTProto分享鏈接, 支持socks5 + tls組合
- [x] 支持http/2, 隨機生成偽裝h2 path
- [x] 開啟關閉tcpFastOpen
- [x] 直接開啟[CDN](https://github.com/Jrohy/multi-v2ray/wiki/CloudFlare-cdn%E4%BB%A3%E7%90%86v2ray%E6%B5%81%E9%87%8F)
- [x] 開啟關閉動態端口
- [x] 定時更新v2ray(需手動開啟)
- [x] 支持新版v2ray配置文件格式(v4.1+)
- [x] 支持範圍端口修改
- [x] 支持程序和**命令行參數**管理控制
- [x] 支持docker部署
- [x] 支持VLESS和Trojan以及XTLS(v4.31.0+)
- [x] 支持純ipv6 vps
- [x] 禁止BT

## 功能

- 一鍵 啟動 / 停止 / 重啟 V2ray 服務端
- 流量統計(v2ray/xray && iptables)
- 命令行模式管理v2ray/xray
- 支持多用戶， 多端口管理
- 開啟關閉動態端口
- bittorrent的禁止與放行
- 單端口, 範圍端口的修改
- 直接走Cloudcflare cdn
- 開啟關閉tcpFastOpen
- 快速查看服務器連接信息, 常規配置修改
- 自由更改**傳輸配置**：
  - 常規TCP
  - HTTP頭部偽裝
  - WebSocket流量
  - 常規mKCP流量
  - mKCP 偽裝 FaceTime通話流量(srtp)
  - mKCP 偽裝 BT下載流量(utp)
  - mKCP 偽裝 微信視頻通話流量(wechat-video)
  - mKCP 偽裝 DTLS 1.2流量(dtls)
  - mKCP 偽裝 WireGuard流量(wireguard)
  - HTTP/2的tls流量(h2)(需備域名) 
  - Socks5
  - MTProto
  - Shadowsocks
  - Quic
  - VLESS_TCP
  - VLESS_TLS
  - VLESS_WS
  - VLESS_XTLS
  - Trojan

## 安裝命令

###### 安裝之前，請先運行

```shell
apt install -y curl
```

或者

```shell
yum install -y curl
```

再開始執行安裝命令，本腳本默認安裝更強大的xray-core  
要安裝v2ray把鏈接中xray.sh改成v2ray.sh即可。

```
source <(curl -sL https://raw.githubusercontent.com/Radium-bit/multi-xray/main/xray.sh) --zh
```

## 升級命令(保留配置文件更新)

```
source <(curl -sL https://raw.githubusercontent.com/Radium-bit/multi-xray/main/xray.sh) -k
```

## 卸載命令

```
source <(curl -sL https://raw.githubusercontent.com/Radium-bit/mulit-xray/main/xray.sh) --remove
```

## 命令行參數

```bash
v2ray/xray [-h|help] [options]
    -h, help             查看幫助
    -v, version          查看版本號
    start                啟動 V2Ray
    stop                 停止 V2Ray
    restart              重啟 V2Ray
    status               查看 V2Ray 運行狀態
    new                  重建新的v2ray json配置文件
    update               更新 V2Ray 到最新Release版本
    update [version]     更新 V2Ray 到指定版本
    update.sh            更新 multi-v2ray 到最新版本
    add                  新增端口組
    add [protocol]       新增一種協議的組, 端口隨機, 如 v2ray add utp 為新增utp協議
    del                  刪除端口組
    info                 查看配置
    port                 修改端口
    tls                  修改tls
    tfo                  修改tcpFastOpen
    stream               修改傳輸協議
    cdn                  走cdn
    stats                v2ray流量統計
    iptables             iptables流量統計
    clean                清理日誌
    log                  查看日誌
    rm                   卸載core
```

## Docker運行

默認創建mkcp + 隨機一種偽裝頭配置文件(**如果使用xray則換成鏡像jrohy/xray**)：

```
docker run -d --name v2ray --privileged --restart always --network host jrohy/v2ray
```

自定義v2ray配置文件:

```
docker run -d --name v2ray --privileged -v /path/config.json:/etc/v2ray/config.json --restart always --network host jrohy/v2ray
```

查看v2ray配置:

```
docker exec v2ray bash -c "v2ray info"
```

**warning**: 如果用centos，需要先關閉防火牆

```
systemctl stop firewalld.service
systemctl disable firewalld.service
```

## 建議

安裝完v2ray後強烈建議開啟BBR等加速: [Linux-NetSpeed](https://github.com/chiakge/Linux-NetSpeed)  
使用Trojan和VLESS協議建議自行安裝個nginx, 能讓v2ray順利Fallback到默認的80端口

## 依賴

v2ray docker: https://hub.docker.com/r/jrohy/v2ray  
xray docker: https://hub.docker.com/r/jrohy/xray  
pip: https://pypi.org/project/v2ray-util/  
python3: https://github.com/Jrohy/python3-install  
acme: https://github.com/acmesh-official/acme.sh