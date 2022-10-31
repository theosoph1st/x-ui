# x-ui

Multi-protocol, multi-user xray panel support
Features

# System status monitoring
- Support multi-user and multi-protocol, web visualization operation
- Supported protocols: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Support configuration of more transmission configurations
- Traffic statistics, limit traffic, limit expiration time
- Customizable xray configuration templates
- Support https access panel (self-provided domain name + ssl certificate)
- Support one-key SSL certificate application and automatic renewal
- More advanced configuration items, see panel for details


# Installation & Upgrade

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

## Manual Installation & Upgrade

1. First download the latest package from https://github.com/vaxilu/x-ui/releases, usually choose amd64 architecture
2. Then upload the tarball to the /root/ directory of the server and log in to the server with the root user

> If your server cpu architecture is not amd64, replace amd64 in the command with another architecture

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Installing with docker

> This docker tutorial and docker image is provided by
[Chasing66](https://github.com/Chasing66)

1. Installing docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Installing x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build your own image

```shell
docker build -t x-ui .
```

## SSL certificate request

> This feature and tutorial are provided by [FranzKafkaYu](https://github.com/FranzKafkaYu)提供

The script has a built-in SSL certificate application function. To apply for a certificate using this script, the following conditions must be met:

- Know the Cloudflare registered email address
- Know the Cloudflare Global API Key
- The domain name has been resolved to the current server through Cloudflare

How to get the Cloudflare Global API Key:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

To use the Cloudflare Global API Key, you only need to enter your domain name, email address and API KEY.
        ![](media/2022-04-04_141259.png)


Caution:

- The script uses DNS API for certificate application
- Default use Let'sEncrypt as CA party
- The certificate installation directory is /root/cert directory
- The application certificate of this script is all pan-domain certificate

## Tg robot use (under development, not available for now)

> This feature and tutorial are provided by [FranzKafkaYu](https://github.com/FranzKafkaYu)提供

X-UI supports daily traffic notifications and panel login reminders via Tg bot. To use Tg bot, you need to apply for it yourself. You can refer to the [blog link](https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html) for the specific application tutorial. Instructions for use: Set the bot-related parameters in the panel background, including

- Tg bot Token
- Tg bot ChatId
- Tg robot cycle running time, using crontab syntax

Reference syntax:
- 30 * * * * * //每一分的第30s进行通知
- 30 * * * * * * //notify on the 30ths of every minute
- @hourly // hourly notification
- @daily //daily notification (at 00:00 am sharp)
- @every 8h //notify every 8 hours

TG notification content：
- Node traffic usage
- Panel login reminder
- Node expiration reminder
- Traffic alert reminder

More features are being planned...

## Recommended Systems

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# Frequently Asked Questions

## Migrating from v2-ui

First install the latest version of x-ui on the server where v2-ui is installed, and then use the following command to migrate all inbound account data from v2-ui to x-ui, the panel settings and username and password will not be migrated

After successful migration, please shut down v2-ui and restart x-ui, otherwise the inbound of v2-ui will have a port conflict with the inbound of x-ui

```
x-ui v2-ui
```

## issue 关闭

Various white-knuckle problems that make your blood pressure very high
Stargazers over time

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
