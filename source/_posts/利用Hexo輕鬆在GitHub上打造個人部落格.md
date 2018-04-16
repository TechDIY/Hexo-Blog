---
title: "利用Hexo輕鬆在GitHub上打造個人部落格"
catalog: true
date: 2018-04-12 16:50:24
subtitle: "快速、簡單且強大的網誌框架."
header-img:  "/img/header_img/iot.jpg"
tags:
- Hexo
- GitHub
catagories:
- 教學
---


# 為什麼選用Hexo?
---
靜態網站產生器有 [Jekyll](https://jekyllrb.com/)、 [Hexo](https://hexo.io/zh-tw/index.html)，為什麼我選用Hexo呢？原因很簡單，因為我覺得Hexo提供的Theme比較好看(超任性)，至於還有像是WordPress之類的，考量還要租用空間，我只是想單純的當作筆記，順便分享出來我辛苦看英文的成果，廢話不多說，我們來開始吧

# 在GitHub上開啟專案
---
首先需要先擁有[GitHub]的帳號，註冊完成後可以看到下圖，點擊Start a project

![Start](https://techdiy.github.io/hexo-Blog/img/HexoBlog/startproject.png)


為自己的Project取個名稱，之後如果沒有購買自己的網域話，這個會變成你的網址

![Creat](https://techdiy.github.io/hexo-Blog/img/HexoBlog/creatblog.png)
看到這畫面代表開專案完成囉，先別關閉畫面，等等需要用到
![url](https://techdiy.github.io/hexo-Blog/img/HexoBlog/url.png)

# 安裝
---
## Node.js
Node.js介紹可以看[這裡](https://zh.wikipedia.org/wiki/Node.js)，為什麼要安裝Node.js呢？因為Hexo是由Node.js編寫而成。
首先[Node.js](https://nodejs.org/en/)官網下載安裝，一路下一步即可安裝完成。

接下來要檢查是否安裝，打開終端機輸入
```bash
node -v
```
如回覆類似以下，及代表安裝完成
>v6.10.3

## NPM 套件管理工具
npm 全名為 Node Package Manager，是 Node.js 的套件（package）管理工具，之後我們會需要用到npm來安裝Hexo，在安裝之前先檢查
```yml
npm -v
```
若 npm 正確安裝，將會看到類似回覆
>3.10.10

## 安裝Hexo
```yml
npm install hexo-cli -g
```

## 新增檔案夾
小技巧：可以將要儲存的資料夾，用滑鼠拉到終端機，自動帶入路徑。
```yml
mkdir /路徑/名稱
cd /路徑/名稱
```
>mkdir /Users/nwt_mac01/Desktop/Luke/Blog2
>cd /Users/nwt_mac01/Desktop/Luke/Blog2

## 初始化Hexo
現在你終端機的位置應該會在，剛新建的資料夾，輸入
```yml
hexo init
```

# 執行
快完成了，經過一番折騰，終於可以看到雛形了，在終端機輸入下面指令，在本地端開啟port來測試，數字可以隨便亂打，而我是開8080 port
```yml
hexo s -p 8080
```
輸入後會看到成功的開啟了8080 port，複製網址貼在網頁上就可以看到原始框架囉，要取消的話輸入Ctrl+C
![local](https://techdiy.github.io/hexo-Blog/img/HexoBlog/local.png)
# 挑選喜歡的Theme
[Hexo官網](https://hexo.io/themes/)提供了200種主題任君挑選，找一個自己喜歡的主題，下載到剛剛新增的資料夾
```yml
git clone 要載的主題Git網址 themes/Theme名稱 
```
# 更換Theme
打開資料夾，在根目錄下找到`_config.yml`檔案，找到theme，換成剛剛下載的名字
```yml
theme: 下載的Theme資料夾名稱  
```
# 上傳檔案到GitHub
## 安裝Git
```yml
npm install hexo-deployer-git --save
```
安裝完成後修改`_config.yml`檔案，再次找到deploy，輸入剛剛在GitHub創好的網址。
```yml
deploy:
  type: git
  repository: https://github.com/TechDIY/Blog.git //TechDIY/Blog修改成你的
  branch: master
```
在輸入以下指令，即可將檔案傳到GitHub上
```yml
hexo generate -d
```
終端機可能會跳出詢問你的帳號密碼，輸入即可開始上傳
![signin](https://techdiy.github.io/hexo-Blog/img/HexoBlog/sign.png)

# 部署部落格
在GitHub網頁上我們可以看到檔案都被傳上來了，在專案裡面選擇Settings
![update](https://techdiy.github.io/hexo-Blog/img/HexoBlog/update.png)
下拉找到GitHub ，選則master branch，並點選Save
![Pages](https://techdiy.github.io/hexo-Blog/img/HexoBlog/Pages.png)
再次往下拉會發現出現了網址，大功告成！！撒花啦，專屬部落格完成。如果你有自己的網域話，可以在Custom domin輸入自己的網域，網址開頭就不會有github.io這樣醜醜的網址拉。
![done](https://techdiy.github.io/hexo-Blog/img/HexoBlog/done.png)

