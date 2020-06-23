# 連結 Runner 跟 GitLab 專案

### 新建一個 GitLab 專案
---
作法就跟 GitHub 一樣，但是功能多出很多，先不管其他的，在左手邊的 DashBoard 裡找到 Setting - CI/CD

![setting](/step2/1.jpg)
 
在上一步的 CMD 裡輸入

    gitlab-runner register

Command 執行之後，還需要輸入各項註冊資訊，其中前兩個重要的資訊便在上圖裡

![cmd](/step2/2.jpg)

GitLab Runner 還有很多可以設定的參數，想要了解可以參考[官方文件](https://docs.gitlab.com/runner/configuration/advanced-configuration.html)。
這邊我們統一使用 **shell** (就是 CMD)

註冊完畢後，Runner 的 config 會存放在 config.toml 裡

![config](/step2/3.jpg)

這樣你的專案便與 Runner 連在一起了，[下一步](/step3/README.md)我們會實際讓他去執行測試