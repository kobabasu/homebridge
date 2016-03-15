# homebridge

## install
1. sudo apt-get update
2. sudo apt-get upgrade
3. sudo npm install -g homebridge
4. sudo npm install -g homebridge-irkit

## config.json
1. `/usr/local/lib/node_modules/homebridge_irkit/config.json.sample`から
   `/home/pi/.homebridge/config.json`にコピー
2. IRKitで赤外線信号を取る
3. dataに記述

## 起動
homebridge

## 自動起動
touch /etc/default/homebridge
一行目はconfig.jsonの場所
```
HOMEBRIDGE_OPTS=-U /home/pi/.homebridge
DEBUG=*
```

touch /etc/systemd/system/homebridge.service
```
[Unit]
Description=Homebridge
After=syslog.target

[Service]
Type=simple
#User=pi
EnvironmentFile=/etc/default/homebridge
ExecStart=/usr/local/bin/homebridge $HOMEBRIDGE_OPTS
Restart=on-failure
RestartSec=10
KillMode=process

[Install]
WantedBy=multi-user.target
```

1. sudo systemctl enable homebridge
2. sudo systemctl start homebridge
3. sudo systemctl status homebridge

正しく起動していればOK
再起動して試してみる
