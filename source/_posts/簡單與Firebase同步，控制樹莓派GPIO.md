---
title: "簡單與Firebase同步，控制樹莓派GPIO"
catalog: true
date: 2018-04-24 14:10:24
subtitle: "玩轉語音控制，智慧您的家園."
header-img:  ""
tags:
- Google Assistant
- Firebase
- Dialogflow
- Raspberry Pi
- JavaScript
catagories:
- 教學
---


![firebase](firebaseL.png)
# Firebase 是什麼？
---
Firebase 簡單來說就是個NoSQL資料庫，可以跨平台應用在 iOS、Android 和 Web上，資料使用 JSON 格式存儲並同步到每個連接的客戶端，即使設備離線也會繼續激活狀態，當設備重新連線時，數據庫資料將更新於設備中。NoSQL 資料庫官方稱為 Realtime Database，相較於傳統資料庫，數據取得變為更加快速，也因為 Firebase 這樣的設計，大大的減低開發時間，而不用大費周章去搞個後台。

# 架構圖
---
這次我要介紹第二部分，將樹莓派與 Firebase 做同步，透過修改 Realtime Database 裡的數值，來達到遠程控制的概念。 如果不曉得怎麼透過JavaScript 控制樹莓派GPIO可以[跳到](/2018/04/21/應用%20Google%20Assistant%20打造智慧家居)。
![Structure](Structure.png)
# 建立專案
---
首先需要登入 [Firebase](https://firebase.google.com/)，點擊GET STARTED 新增一個專案。
![New project](Newproject.png)

輸入你專案想取的名稱，輸入完畢後點擊建立專案。
![New project2](Newproject2.png)

點擊剛剛建立的專案會看到，點擊Database
![New project3](Newproject3.png)

選取 Realtime Database 的開始使用
![New project4](Newproject4.png)

選擇以鎖定模式啟動，點擊啟用
![New project5](Newproject5.png)

之後會看到空白的資料庫，複製下面代碼，存成`.json`檔案後，點擊紅框，選擇匯入JSON
![New project6](Newproject6.png)

```json
{
  "auto" : {
    "light" : {
      "value" : "off"
    }
  }
}
```

成功匯入後可以看到資料庫變成這樣了。目前 Firebase 到這裡告一個段落，先別急著把網頁關閉，等等測試時候會用到。
![New project7](Newproject7.png)

# 樹莓派連上Firebase
---
這個步驟相對地簡單，只需要將上一篇的`.js`檔案，再加幾行程式碼而已，首先我們先打開終端機安裝 Firebase Library
```bash
npm install firebase
```

## apiKey、databaseURL的取得
打開Firebase網頁，點擊 Project OverView 旁的設定→專案設定。
![New project8](Newproject8.png)
紅框處為等等`.js`檔案所需要填入的資訊。
![New project9](Newproject9.png)

## JavaScript程式碼
複製以下代碼，覆蓋上一篇的`.js`檔案。填入 apiKey、databaseURL 讓程式知道要去哪裡取得資料庫，ref可以想像作為資料庫裡的auto資料夾。
ref.on是同步，如果只需要抓取一次後就不更新可以改為ref.once。
```javascript
var firebase = require("firebase");
var config = {
  apiKey: "網路 API 金鑰",
  databaseURL: "https://專案 ID.firebaseio.com",
};
firebase.initializeApp(config);



var db  = firebase.database();
var ref = db.ref("/auto");
ref.on("value", function(snapshot) {
  console.log(snapshot.val().light);
  console.log(snapshot.val().light.value);
  var LED_value = snapshot.val().light.value;
  blinkLED(LED_value);
});


var gpio = require("onoff").Gpio;

const LEDR = new gpio(18, 'out');

function blinkLED(State) {
  if (State === 'on') {
    LED.writeSync(0);
  }else{
    LED.writeSync(1);
  }
}
```

## 執行
儲存完畢後是該來測試結果了，打開終端機
```bash
node xxx.js //xxx為路徑＋檔案名稱
```
修改 Firebase 上 light 的 value (on開、off關) ，你可以看到樹莓派上面的燈會因為輸入不同值而變化。
![run](run.png)

**下一篇將會介紹用Dialogflow為Google Assistant打造專屬App**