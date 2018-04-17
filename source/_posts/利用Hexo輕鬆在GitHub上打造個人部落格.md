---
title: "利用Hexo輕鬆在GitHub上打造個人部落格"
catalog: true
date: 2018-04-12 16:50:24
subtitle: "快速、簡單且強大的網誌框架."
header-img:  "header.png"
tags:
- Hexo
- GitHub
catagories:
- 教學
---


# 為什麼選用Hexo?
---
靜態網站產生器有 [Jekyll](https://jekyllrb.com/)、 [Hexo](https://hexo.io/zh-tw/index.html)，為什麼我選用Hexo呢？原因很簡單，因為我覺得Hexo提供的Theme比較好看，至於還有像是WordPress之類的，考量還要租用空間，我只是想單純的當作筆記，順便分享，所以窮人方案比較適合我。

# 在GitHub上開啟專案
---
首先需要先擁有[GitHub]的帳號，註冊完成後可以看到下圖，點擊Start a project

![Start](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/startproject.png)


為自己的Project取個名稱

![Creat](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/creatblog.png)
看到這畫面代表開專案完成囉，先別關閉畫面，等等需要用到
![url](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/url.png)

# 安裝
---
## Node.js
Node.js介紹可以看[這裡](https://zh.wikipedia.org/wiki/Node.js)，為什麼要安裝Node.js呢？因為Hexo是由Node.js編寫而成。
首先[Node.js](https://nodejs.org/en/)官網下載安裝，一路下一步即可安裝完成。

接下來要檢查是否安裝，打開終端機輸入
```yml
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

Mac:
```yml
mkdir /路徑/名稱
cd /路徑/名稱
```
>mkdir /Users/nwt_mac01/Desktop/Luke/Blog2
>cd /Users/nwt_mac01/Desktop/Luke/Blog2

Windows:
```yml
mkdir /路徑/名稱
pushd /路徑/名稱
```

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
![local](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/local.png)
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
利用GitHub的不同分支來分别保存原始文件與編譯完後的檔案，會這樣做是因為Hexo只會上傳編譯後的靜態網頁檔案到github，當換環境寫Blog時會發現根本沒有原始文件可以編輯，所以必須建立分支來儲存我們的原始檔案。
## 安裝Git
首先電腦要先安裝[Git](https://git-scm.com/book/zh-tw/v2/%E9%96%8B%E5%A7%8B-Git-%E5%AE%89%E8%A3%9D%E6%95%99%E5%AD%B8)，然後初始化，並上傳檔案到GitHub專案上
```yml
git init
git add —all 
git commit -m “你要記錄的文字"
git remote add origin https://github.com/你的名稱/專案名稱.git 
git push -u origin master 
```
## 建立分支
在Code點擊Branch:master，在Find or creat a branch...處，輸入branch名稱，即可建立完成。
![newbranch](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/newbranch.png)
之後上傳原始檔的話就切換到剛創建的branch
```yml
git add . 
git commit -m "你要記錄的文字" 
git push -u origin hexo 
```
## 發布靜態檔案
Hexo 提供了快速方便的一鍵佈署功能，讓您只需一個指令就能將網站佈署到伺服器上 
```yml
npm install hexo-deployer-git --save
```
安裝完成後修改`_config.yml`檔案，找到deploy，輸入剛剛在GitHub創好的網址。
```yml
deploy:
  type: git
  repository: https://github.com/TechDIY/Blog.git //TechDIY/Blog修改成你的
  branch: master
```
在輸入以下指令，即可將檔案傳到GitHub上
```yml
hexo g -d
```


# 部署部落格
在GitHub網頁上我們可以看到檔案都被傳上來了，在專案裡面選擇Settings
![update](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/update.png)
下拉找到GitHub ，選則master branch，並點選Save
![Pages](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/Pages.png)
再次往下拉會發現出現了網址，大功告成！！撒花啦，專屬部落格完成。如果你有自己的網域話，可以在Custom domin輸入自己的網域，網址開頭就不會有github.io這樣醜醜的網址拉。
![done](https://techdiy.github.io/Hexo-Blog/img/HexoBlog/done.png)

