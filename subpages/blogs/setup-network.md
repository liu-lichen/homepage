# Summary of how to setup personal network

## Setup virtual machine

- Basics
  - Navigate to https://portal.azure.com
  - Create virtual machine
  - Resource group: access_resource_group
  - Virtual machine name: access-resource-1
  - Region: (Asia Pacific) Japan East
  - Image: Ubuntu Server 20.04 LTS - x64 Gen2
  - Size: Standard_B1s - 1 vcpu, 1GiB memory (HK$77.04/month)
  - Authentication type: Password
  - Username: azureuser
  - Password: (something in cloud)
  - Select inbound ports: SSH, HTTP, HTTPS
- Disks
  - Follow default settings
- Networking
  - Follow default settings
- Management
  - Enable auto-shutdown: False
- Monitoring
  - Follow default settings
- Advanced
  - Follow default settings
- Tags
  - Follow default settings

## Configure network port rules

- Enter the page `Network settings` of the VM
- Click `+Create port rule`
- Change `Destination port ranges` to `18915-20000`
- Change `Name` to `SSR`
- Click `Add`

## Setup SSR network setting

### Install SSR server

- Get the public IP from the resource page
- Login the VM by `ssh azureuser@ipaddress` from the terminal
- Update packages: `sudo apt update`
- Install git: `sudo apt install git`
- Clone the shell script: `git clone -b master https://github.com/flyzy2005/ss-fly && cd ss-fly && sudo ./ss-fly.sh -ssr`
  - Password: (something in cloud)
  - Server port: 18915
  - Server encryption method: aes-256-cfb
  - Server protocol: auth_aes128_sha1
  - Obfuscation: tls1.2_ticket_auth
- Finally, get some thing like below:
```
Congratulations, ShadowsocksR server install completed!
Your Server IP        : ip
Your Server Port      : port
Your Password         : password
Your Protocol         : protocol
Your obfs             : obfuscation
Your Encryption Method: encryption_method
 
Welcome to visit:https://shadowsocks.be/9.html
Enjoy it!
```

### Launch BBR speedup

- Run command: `sudo ./ss-fly.sh -bbr`

### Some commands

- Start: `/etc/init.d/shadowsocks start`
- Stop: `/etc/init.d/shadowsocks stop`
- Restart: `/etc/init.d/shadowsocks restart`
- Status: `/etc/init.d/shadowsocks status`
- Uninstall: `sudo ./shadowsocksR.sh uninstall`

## Setup V2Ray network setting

### Install V2Ray server

- Login the VM by `ssh azureuser@ipaddress` from the terminal
- Install wget by `sudo apt-get -y install wget`
- Install curl by `apt install -y curl`
- Download script by `curl -sL https://raw.githubusercontent.com/daveleung/hijkpw-scripts-mod/main/xray_mod1.sh -o xray_mod1.sh`
- Install by `sudo bash xray_mod1.sh`
  - Question: need a domain here
- Uninstall by `sudo bash xray_mod1.sh uninstall`

### Usefull commands

- `service v2ray start|stop|status|reload|restart|force-reload`

## Use it in devices

- Download client
  - Windows: https://github.com/shadowsocks/shadowsocks-windows
  - Mac: https://github.com/shadowsocks/ShadowsocksX-NG
  - iOS: Search Shadowrocket in AppStore with an abroad accout
- Add server with above info
- Start

## Reference:
- https://portal.azure.com
- https://github.com/mku228/vpn-ss-ssr
- https://github.com/shadowsocks
- https://github.com/flyzy2005/ss-fly/wiki
- https://v2xtls.org/v2ray带伪装一键脚本ubuntu版/
