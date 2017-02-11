---
layout     : post
title      : "Github Page and Jekyll"
subtitle   : "如何利用Github Page快速建立自己的部落格"
---

## Jekyll 簡介

簡單而言，Jekyll是利用Ruby所開發的「靜態網站產生器」。下面是[Jekyll中文站](http://jekyllcn.com)的介紹：

> 将纯文本转换为静态博客网站
> 
> * 不再需要数据库，不需要开发评论功能，不需要不断的更新版本——只用关心你的博客内容。
> 
> * Markdown（或 Textile）、Liquid 和 HTML & CSS 构建可发布的静态网站。
> 
> * 支持自定义地址、博客分类、页面、文章以及自定义的布局设计。

我們只要照著Jekyll的規範，用markdown撰寫自己的文章上傳到Github上，Github會自動進行編譯出靜態網站，簡單的步驟就能擁有排版優美的文章部落格。

## 到底什麼是靜態網頁？

如果沒有接觸過這類的東西，你八成看到這邊還是霧煞煞，事實上他就是直接將文章轉換成一份HTML檔案，過程中完全不需要Database，所以載入速度當然快上許多。

## 那為什麼選擇Jekyll呢？

最主要就是方便、快速，加上Github支援，不但完全免費，還可以順便享受Github的版本控制，也算是邊做邊學習。另外Jekyll可以相當自由的客製化自己的部落格樣式，不需要做冗長的設定，就可以簡單使用，應該夠吸引人了吧？

## 首先我們先註冊一個Github帳號

到[Github](https://github.com/join?source=header-home)註冊帳戶，請牢記自己的`Username`，將來會用到哦。

## 想唬我啊，網域名稱這些呢？

首先你必須先問自己，呃我是要用內建的github.io網域呢？還是想要用自己購買的網址？

	#### A. 我想要使用內建的github.io網域
 	
如果你想直接使用github.io網域，首先先在自己的Github建立新的Repositories。這邊名稱是有限制的，必須為`你的Username.github.io`。之後你部落格的URL就會試`https://你的Username.github.io/`。專案內容只要放在預設的master分支下，就能建置網站，要注意的是每個Github帳號只能擁有一個使用者網站。這樣大概就完成第一步了。

#### B. 我想要使用自己購買的網域名稱

想要使用自己購買的網域名稱就比較麻煩一點，首先要先將目前的branch設定為`gh-pages`，並在CNAME檔案中，填上你想要綁定的網址，並到網域供應商以`CNAME`類型將其綁定置`你的Username.github.io`。


## 我們來設定Github一些選項

呃，照道理，程式開發者都喜歡用原生的Git cmd，但我這邊介紹我喜歡用的免費Git GUI`SourceTree`來操作Git指令。

1. 首先下載[SourceTree](https://www.sourcetreeapp.com/)。
2. 打開SourceTree，點選選單列的`Tools`>`Options`。在`Default user information`欄位中輸入自己的`Full Name`與`Email address`。
3. 接著點選選單列的`Tools`>`Create or Import SSH Keys`。點選`Generate`產生金鑰，別傻傻的等進度條，這邊是要利用移動滑鼠來建立獨一無二的金鑰，所以動動滑鼠至進度條滿即完成金鑰的產生。
4. 分別點選`Save public key`與`Save private key`，將公私鑰存至你滿意的路徑中。
5. 用記事本開啟`Public key`並從**第三行**開始複製代碼存至剪貼簿。
6. 然後呢，來到[Github Setting](https://github.com/settings/profile)，在左邊選單中點選`SSH and GPG keys`，接著點`New SSH key`，`Title`隨意填入自己能理解的名稱，`Key`則先填入ssh-rsa，空一格貼上剛剛所存的代碼並儲存，像是這樣：

		ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAIBwT+f90QJlej81gB55bXxN/t8quZmmJREaZaon
		NcsMkTeh1aiO78zBDTKdVqz2STgss4+pLta/h8KbmSHBggMAL8/NqKkmKalL+CWX
		PNVJi0TXosJiUlwlG9ku/5NNOA0Lr3o4vXQGf32z6yQN5XhDyHW+0XcuaNaoouWV
		pZE5Bw==

7. 最後最後，點選工具列右下角通知的小電腦圖示(SSH agent)，若尚未啟動請到`Tools`>`Launch SSH agent`啟動，然後點選`Add key`把剛剛所存的`Private key`輸入進去即可完成連線加密的設定。

完成連線加密後，我們先到自己的Repositories，點選右上角的`Clone or download`，將視窗內那行網址複製起來，回到SourceTree點選`Clone / New`，在`Source Path / URL`貼上剛剛所複製的網址，`Destination Path`選擇自己想要儲存的本機儲存庫路徑，注意哦，這就會是一個固定的位置，以後就會利用git同步至Github之中，像我的習慣就是放在

    D:\workspace\morningdip.github.io

這樣就完成本機與Github的綁定，以後就可以利用commit與push完成上傳。

## 好啦好啦，接著來選個部落格樣式吧

接著你可以用Google搜尋看看樣式頁面，我在這邊遇到滿多問題的，原因是因為Jekyll不斷更新，很多網路上的樣式已經不支援最新版的Jekyll，我的部落個是選擇[Hyde](https://github.com/poole/hyde)樣式，教學就以它為介紹好了。

首先先到[Hyde](https://github.com/poole/hyde)，點選右上角的`Clone or download`選擇`Download ZIP`下載一份至電腦中，接著解壓縮到你本機儲存庫的路徑，

到這邊你必須要有一個概念，想要預覽網站，你必須把這整包的東西都上傳至Github，利用那邊的Jekyll來編譯自己的靜態網站，但若是你經常需要修改，每次都需要上傳然後等待更新這會是很頭痛的一件事情，為了方便我們編輯修改網站，通常我們都會在本機端也建好Jekyll的環境，方便我們在手邊先預覽好，等到修改完畢後才上傳至Github上完成建置。

由於先前所說的Jekyll是利用Ruby所開發的，所以理所當然我們必須先建好Windows的Ruby的開發環境。

1. 至[RubyInstaller for Windows](https://rubyinstaller.org/)下載自己電腦合適的版本安裝。安裝過程中注意要勾選`Add Ruby executables to your PATH`。
2. 安裝[RubyGems](https://rubygems.org/pages/download)，Windows下載ZIP格式比較好操作，解壓縮至任意路徑，打開cmd輸入以下命令：
		
		$ cd {unzip-path}
		$ ruby setup.rb

3. 安裝Jekyll，打開cmd輸入以下命令：

		$ gem install jekyll

4. 安裝jekyll-paginate，打開cmd輸入以下命令：

		$ gem install jekyll-paginate

好，理論上我們已經完成Jekyll本機端的環境建置，接著我們一樣操作cmd命令：

	$ cd {hyder-master-unzip-path}
	$ jekyll serve

對啊，你一定也出現一堆錯誤，這邊是因為版本的關係，必須修改目錄下`_config.yml`的內容：

1. 將`markdown`屬性改為`kramdown`
2. 將`highlighter`屬性改為`rouge`
3. 添加`gems: ["jekyll-paginate"]`
4. `CNAME`檔案刪除`hyde.getpoole.com`設為空白檔案儲存。

接著把`_posts`資料夾中的`2012-02-07-example-content.md`刪除，好啊搞得昏頭亂向的，我們再來執行一次cmd指令：

	$ jekyll serve

沒失智的話，嗯，我們應該完成本機端的建置，cmd別急著關掉，只要`jekyll serve`服務開著，我們打開瀏覽器網址欄輸入`http://localhost:4000/`，噹啷！是不是看到自己網站樣子啦。剛剛做那麼多奇怪事情，目的就是之後我們只要在這個目錄下編輯，開啟本地的`jekyll serve`，任何更新都可以即時預覽，待自己的文章修改到心滿意足之後，再上傳至Github發佈。

