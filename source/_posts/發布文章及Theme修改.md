---
title: "GitHub Page 發布文章及Theme修改"
catalog: true
date: 2018-04-17 13:10:24
subtitle: "快速、簡單且強大的網誌框架."
header-img:  "header.png"
tags:
- Hexo
- GitHub
- GitHub Page
catagories:
- 教學
---

# 發布第一篇文章
---

繼上一篇[打照個人部落格](http://techdiy.tk/2018/04/12/%E5%88%A9%E7%94%A8Hexo%E8%BC%95%E9%AC%86%E5%9C%A8GitHub%E4%B8%8A%E6%89%93%E9%80%A0%E5%80%8B%E4%BA%BA%E9%83%A8%E8%90%BD%E6%A0%BC/)成功架設了自己的部落格，是該來發布第一篇文章，打開本地端資料夾，依照路徑新增一個檔案，檔名為`.md`

>資料夾 → source→ _posts→ 新增檔案.md 

檔頭格式依照所下載的主題提供的方法做編寫，例如我的
```bash
title: "發布文章及Theme修改"
catalog: true
date: 2018-04-17 13:10:24
subtitle: "快速、簡單且強大的網誌框架."
header-img:  "header.png"
tags:
- Hexo
- GitHub
catagories:
- 教學
```

至於文章內容的話，在作者在Git上應該也會說明，如果沒有的話，其實也沒關係，因為Hexo 是使用[Markdown 標記語法](https://wastemobile.gitbooks.io/gitbook-chinese/content/format/markdown.html)，只要遵循語法寫就好了。

寫完文章後先在本地端測試
```yml
hexo g              //生成靜態文件
hexo s -p 8080     //開啟8080 port
```
確定沒問題後，再將靜態文件發布在GitHub，別忘了將原始文件檔也上傳到GitHub的分支上，避免換環境之後，想修改內容卻沒檔案。
```yml
hexo -d               //上傳靜態文件於GitHub
git add .              //添加文檔夾下的所有文檔
git commit -m "New"   //引號內為此次提交説明
git push -u origin hexo // 推送到Github，hexo為我所建的分支
```

完成！打開網頁去看看自己發的第一篇文章吧！


# 修改Theme
---
這部需要有點基礎，不過透過了解Hexo的基礎結構後，會比較好下手修改。
```
|-- _config.yml
|-- public
|-- source
   |-- _posts
|-- themes
   |-- layout
   |-- source
```
## _config.yml
很重要的一個檔案，這是配置整個部落格資訊的檔案，例如部落格名稱、作者、主題...等。
## public
生成的靜態網頁存放地方，不會對這個地方做修改，大略知道就好了。
## source
這目錄很重要，發布的文章需要放在 _posts目錄下，如果看不懂Code，只要知道在_posts底下新增`.md`就可以發文了。其他可能還會有一些像選單的資料夾，只要找到相對應的名稱，就可以做資訊上的修改。
## themes
主題資料夾，存放載下來的主題，並透過修改_config.yml裡的theme[更換主題](http://techdiy.tk/2018/04/12/%E5%88%A9%E7%94%A8Hexo%E8%BC%95%E9%AC%86%E5%9C%A8GitHub%E4%B8%8A%E6%89%93%E9%80%A0%E5%80%8B%E4%BA%BA%E9%83%A8%E8%90%BD%E6%A0%BC/#%E6%9B%B4%E6%8F%9BTheme)。
### layout
佈局資料夾。用於放置主題的模板檔案，決定了網站內容的呈現方式。
如果要修改Theme的模板就要在此資料夾下手。
### source
原始檔案資料夾，此資料夾是儲放模板以外的檔案，例如CSS、JavaScript檔案等，經過編譯後會自動存放在public資料夾

