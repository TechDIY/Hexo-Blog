---
title: "HomeKit 控制樹莓派 GPIO"
catalog: true
date: 2018-05-22 19:10:24
subtitle: "玩轉語音控制，智慧您的家園."
header-img:  ""
tags:
- Smart Home
- HomeKit
- Homebridge
- Raspberry Pi
catagories:
- 教學
---


# HomeKit
---
&ensp;&ensp;&ensp;&ensp;HomeKit 為 Apple 所主導的智慧家庭 App ，可以從 iPhone 或 iWatch 上，要求 Siri 開關家中的智慧家電，甚或是現在火紅的智慧喇叭 HomePod ，但 Apple 陣營一直以來都有一種特性：『封閉』，要加入 HomeKit 取得那迷樣的貼紙，你必須要付錢成為 Apple 開發的公司，之後 Apple 會提供刻有公司名稱的文件，並禁止外流，再來就是家電本身需要使用 Apple 指定的晶片及加密方式，並提供樣品寄送到檢測中心做檢測，最終才能取得 MFI認證。

![](http://www.hallsteninnovations.com/wp-content/uploads/2015/12/Works-with-Apple-HomeKit-badge-medium.png)

![](https://www.ningselect.com/wp-content/uploads/2016/09/Incipio-%E9%A3%9B%E7%91%9E%E9%81%94_0005-1024x683.jpg)


由於蘋果的「囉唆」，雖然開發難度變高，但相對於使用者卻是及好上手，我很喜歡廠商站在消費者立場想，而不是一昧的追求低成本高效益的模式，掃一下條碼及配對完成（什麼這麼簡單！），相較於其他廠商，這配對堪稱完美。 但也因蘋果的囉唆，使用者必需要更有信仰，HomeKit 需透過 Apple TV 或 iPad 遠端取用你所有的家庭智慧配件，像是關上車庫門、查看出入口攝影機的即時畫面。
![](https://images.apple.com/tw/ios/home/images/overview/home_autopilot_medium.jpg)

這也就是這篇誕生的原因，印象中的 HomeKit 就是很封閉，偶然發現有 [Homebridge](https://github.com/nfarina/homebridge) 這東西，來達到用 HomeKit 做語音控制，而且還可以加入其他家智慧家電產品，像小米之類的，真是令人太興奮了，我們來看一下怎麼做吧！


# Homebridge
---
&ensp;&ensp;&ensp;&ensp;Homebridge 是個輕量級的 NodeJS 伺服器，可以用以模擬 HomeKit 的 API，且支援其他插件，你可以挑選一個喜歡的工具並修改 JSON 檔，就可完成想要的服務，而且重點『好上手』

在開始之前你必須準備：
1. 樹莓派
2. 繼電器模組

# 安裝
---
樹莓派的作業系統安裝這裡就跳過了，直接從 Node 開始，在安裝 Node 之前可以用 ssh 指令連到樹莓派 `ssh pi@192.168.xx.xxx`， 密碼預設為 raspberry

## NodeJS
1. 首先在終端機輸入 `node -v` ，應該版本為 4.x.x
2. 輸入 `wget https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-armv6l.tar.xz` 可以選擇你要的版本
3. 解壓縮 `tar -xvf node-v8.9.4-linux-armv6l.tar.xz`
4. `cd node-v8.9.4-linux-armv6l/`
5. 輸入 `whereis node` ，應該會輸出 `/usr/bin/node  /usr/local/bin/node  /usr/share/man/man1/node.1.gz` ，注意第一個結果
6. 如果是`/usr/bin/node` 輸入 `sudo cp -R * /usr/` ，如果是 `/usr/local/bin/node` 則輸入 `cp -R * /usr/local/`
7. 輸入 `node -v` ，應該會為 v8.9.4

## Homebridge

GPIO 控制我選用 [homebridge-gpio-wpi2](https://github.com/rsg98/homebridge-gpio-wpi2) 工具，直接來開始吧

1. 安裝 `sudo apt-get install libavahi-compat-libdnssd-dev`
2. 安裝 Homebridge `sudo npm install -g --unsafe-perm homebridge`
3. 安裝 wiringpi `sudo apt-get install wiringpi`
4. 安裝 GPIO `sudo npm install homebridge-gpio-wpi2`
5. 設定好次要群組 `sudo usermod -G gpio homebridge`


安裝完 Homebridge 之後 需要來新增及修改一些檔案

1. `ip address show eth0 | grep link/ether | cut -c16-32 | tr a-z A-Z` ， 複製 MAC 碼
2. 修改檔案`sudo nano ~/.homebridge/config.json` ， 填入 MAC 、port 及 pin 碼，並指定 GPIO 腳位。
```JSON
{
    "bridge": {
        "name": "Homebridge",
        "username": "B8:27:EB:0F:45:9F",
        "port": 51826,
        "pin": "123-45-678"
    },

    "description": "This is an example configuration file with one fake accesso$

    "platforms": [
        {
                    {
            "platform" : "WiringPiPlatform",
            "name" : "Pi GPIO (WiringPi)",
            "overrideCache" : "true",
            "autoExport" : "true",
            "gpiopins" : [{
                "type":"Switch",
                "name" : "GPIO0.1",
                "pin"  : 18,
                "enabled" : "true",
                "mode" : "out",
                "pull" : "down",
                "inverted" : "true",
                "duration" : 0,
                "polling" : "true"
                }]
        }
    ]
}
```
3. Control + X ，點擊 y 和 enter 作儲存
4. `homebridge` 即可運行及配對囉

## 配對
上一步輸入完畢後會看到類似的文字 
![](https://blog.encoredevlabs.com/assets/article_images/2017-12-25/qr-code.png)

打開 iPhone 的 Wi-Fi 連同一個分享器，開啟 HomeKit(臺灣應該是『家庭』)，用相機掃描 QRcode 即可配對完成




