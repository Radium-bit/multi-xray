#multi-xray

V2ray/Xray multi-user management script, wizard management [Add|Delete|Modify] Transmission Protocol
![](https://img.shields.io/pypi/v/v2ray-util.svg)
![](https://img.shields.io/github/license/Jrohy/multi-v2ray.svg)

## [简体中文](README.md) |[English](README_EN.md) |[正體中文](README_TR.md)  

- [x] Modified from [Jrohy](https://github.com/Jrohy) project [multi-v2ray](https://github.com/Jrohy/multi-v2ray)

## feature

- [x] Support Xray management, v2ray and xray are independent of each other, different commands (v2ray/xray) enter different core management
- [x] Directly install v2ray (Author: [Jrohy](https://github.com/Jrohy))/xray (Modify: Radium-bit)
- [x] Call v2ray official api for traffic statistics
- [x] **Multi-user, multi-port management**, mixed transport protocol management is no longer a dream
- [x] Generate a random port when installing for the first time, the default configuration is mkcp + a random one (srtp | wechat-video | utp | dtls | wireguard) header masquerading;
  After the installation is complete, the configuration information is displayed;
- [x] View configuration information to display vmess/vless strings (v2rayN's share link format)
- [x] Generate **Telegram** socks5/MTProto share link, support socks5 + tls combination
- [x] support http/2, randomly generate fake h2 path
- [x] enable and disable tcpFastOpen
- [x] Directly open [CDN](https://github.com/Jrohy/multi-v2ray/wiki/CloudFlare-cdn%E4%BB%A3%E7%90%86v2ray%E6%B5%81%E9% 87% 8F)
- [x] enable and disable dynamic ports
- [x] Update v2ray regularly (requires manual activation)
- [x] Support new v2ray configuration file format (v4.1+)
- [x] support range port modification
- [x] Support program and **command line arguments** administrative control
- [x] support docker deployment
- [x] Support for VLESS and Trojan and XTLS (v4.31.0+)
- [x] support pure ipv6 vps
- [x] Ban BT

## Features

- One-click start/stop/restart V2ray server
- Traffic statistics (v2ray/xray && iptables)
- Command line mode to manage v2ray/xray
- Support multi-user, multi-port management
- Enable and disable dynamic ports
- Prohibition and release of bittorrent
- Modification of single port, range port
- Go directly to Cloudcflare cdn
- Turn on and off tcpFastOpen
- Quickly view server connection information, general configuration modification
- Freely change **Transport configuration**:
  - Regular TCP
  - HTTP header masquerading
  - WebSocket traffic
  - Regular mKCP flow
  - mKCP disguise FaceTime call traffic (srtp)
  - mKCP disguise BT download traffic (utp)
  - mKCP disguise WeChat video call traffic (wechat-video)
  - mKCP masquerading DTLS 1.2 traffic (dtls)
  - mKCP masquerades WireGuard traffic (wireguard)
  - HTTP/2 tls traffic (h2) (requires domain name)
  - Socks5
  - MTProto
  - Shadowsocks
  -Quic
  - VLESS_TCP
  - VLESS_TLS
  - VLESS_WS
  - VLESS_XTLS
  - Trojan

## install command

###### Before installing, please run

```shell
apt install -y curl
````

or

```shell
yum install -y curl
````

Then start executing the installation command, this script installs the more powerful xray-core by default
To install v2ray, change xray.sh in the link to v2ray.sh.

````
source <(curl -sL https://raw.githubusercontent.com/Radium-bit/multi-xray/main/xray.sh) --en
````

## Upgrade command (keep config file updated)

````
source <(curl -sL https://raw.githubusercontent.com/Radium-bit/multi-xray/main/xray.sh) -k
````

## uninstall command

````
source <(curl -sL https://raw.githubusercontent.com/Radium-bit/mulit-xray/main/xray.sh) --remove
````

## command line arguments

```bash
v2ray/xray [-h|help] [options]
    -h, help View help
    -v, version View version number
    start start V2Ray
    stop stop V2Ray
    restart restart V2Ray
    status View V2Ray running status
    new rebuild the new v2ray json configuration file
    update Update V2Ray to the latest Release version
    update [version] Update V2Ray to the specified version
    update.sh update multi-v2ray to the latest version
    add add new port group
    add [protocol] Add a new protocol group, the port is random, such as v2ray add utp to add utp protocol
    del delete port group
    info View configuration
    port Modify the port
    tls modify tls
    tfo Modify tcpFastOpen
    stream modifies the transport protocol
    cdn go cdn
    stats v2ray traffic statistics
    iptables iptables traffic statistics
    clean clean up logs
    log View log
    rm uninstall core
````

## Docker run

By default, mkcp + a random camouflage header configuration file is created (**if you use xray, replace it with mirror jrohy/xray**):

````
docker run -d --name v2ray --privileged --restart always --network host jrohy/v2ray
````

Custom v2ray configuration file:

````
docker run -d --name v2ray --privileged -v /path/config.json:/etc/v2ray/config.json --restart always --network host jrohy/v2ray
````

View v2ray configuration:

````
docker exec v2ray bash -c "v2ray info"
````

**warning**: If you use centos, you need to close the firewall first

````
systemctl stop firewalld.service
systemctl disable firewalld.service
````

## Suggest

After installing v2ray, it is strongly recommended to enable acceleration such as BBR: [Linux-NetSpeed](https://github.com/chiakge/Linux-NetSpeed)
Using the Trojan and VLESS protocols, it is recommended to install an nginx by yourself, so that v2ray can smoothly fallback to the default port 80

## dependencies

v2ray docker: https://hub.docker.com/r/jrohy/v2ray
xray docker: https://hub.docker.com/r/jrohy/xray
pip: https://pypi.org/project/v2ray-util/
python3: https://github.com/Jrohy/python3-install
acme: https://github.com/acmesh-official/acme.sh