---
title: "快速上手 React Native"
catalog: true
date: 2018-06-02 13:10:24
subtitle: ""
header-img:  ""
tags:
- React Native
- Expo
catagories:
- 教學
---


# 原生? 混合? 網頁?
---
&ensp;&ensp;&ensp;&ensp; 原生 App (Native App)一直以來都存有一個問題，依賴官方提供的 SDK ,以及不同平台需要投入更多開發人員,但好處是原生擁有更快的執行速度，且對硬體支援度較好，雖然如此,成本與投入時間還是個問題,之後衍生出 混合式 App (Hybrid App) 及 Web App 的選擇. Web APP 即用網頁方式呈現,實現了跨平台且低成本,但效能最差且受限於網路,因此出現了混合式開發，算是將兩者綜合,以半原生半網頁模式,但效能即功能性還是低於原生‧ 

# React Native
&ensp;&ensp;&ensp;&ensp; 上面一段簡單介紹了三種,那 React Native 屬於哪種? 答案是:...都不是. React Native的App是Native(原生)的App，只是JavaScript程式碼是在一層JavaScriptCore上面執行。

React Native 由 Facebook 推出,開發使用 Javascript、視圖元件(很像Html)及樣式風格(類似CSS),它的優點:
* 跨平台: Android 與 iOS 
* Learn once，write any where
* 應用範圍 : Facebook、Instagram、Skype、Uber [...等](https://facebook.github.io/react-native/showcase.html)
* 擴充性:能然可以用 Obj-C、Swift 或 Java(Android) 新增應用

還有許多優點為列出，但也並非沒缺點:
* 新寫法、新技術需要花時間練習
* 支援需加強
* 待補充

# 實作
&ensp;&ensp;&ensp;&ensp; 現在開發有兩種選擇,一種直接使用 [Expo](https://expo.io/) 來執行程式,或者走比較傳統的安裝 IDE ( Xcode or Android Studio ),這篇會分別教學個別方式

##  Expo
打開終端鍵入
1. `npm install -g create-react-native-app` ,安裝 React Native
2. `create-react-native-app HelloWorld` ,新增資料夾
3. `cd HelloWorld` , 移動到新增的資料夾
4. `npm start` , 開始

這時候手機就必須要安裝 [Expo](https://expo.io/) App ,並且在同一個網路環境 , Android 掃描終端出現的 QR code 即可運行 .

##  一般
每種開發平台不一樣, Windows 如果之前有跟我run過 ,應該電腦都會安裝 [Node](https://nodejs.org/en/) ,這裡就不教學 Android Studio 安裝了,照[官網](https://facebook.github.io/react-native/docs/getting-started.html)


1. `npm install -g react-native-cli`
2. `react-native init HelloWorld`
3. `cd HelloWorld`
4. `react-native run-android` 或 `react-native run-ios` ,這步驟可以省略,可以直接進 IDE 執行 (檔案夾有 android 或 ios )

> 如果出現 unable to load script from assets index.android.bundle 
> 1. (在資料夾內) mkdir android\app\src\main\assets 
> 2. react-native bundle --platform android --dev false --entry-file index.js --bundle-output android\app\src\main\assets\index.android.bundle --assets-dest android\app\src\main\res
> 3. react-native run-android
