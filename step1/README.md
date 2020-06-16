# 架設 GitLab CI Runner

### 什麼是 CI Runner？
---
 CI Runner 即是為你執行自動化測試的工人，如果有很多個 Runner 那麼你在同一時間內便可處理很多測試，反之如果有大量的測試需要執行，但 Runner 有限，該測試就會程現 **Pending** 狀態，然後等待其他工作完成後才執行。

### CI 流程
---
簡略的 CI 流程如下圖所示，**黑色框框**是我們平常在做的事，而我們現在要做的就是派遣一個  CI Runner 去幫你做**紫色框框**內事情

![flow](/step1/1.png)

### 安裝 GitLab CI Runner
---
GitLab 官方為 Runner 提供了多種安裝方式，在[官網](https://docs.gitlab.com/runner/install/linux-repository.html)上皆有詳盡的文件可以參考。

由於我的作業系統為 win10，於是我們到這裡來[下載](https://docs.gitlab.com/runner/install/windows.html)

![download](/step1/2.png)

照著官網的指示，在本地端建立一個名叫 GitLab-Runner 的資料夾，把下載下來的**檔案改名為 gitlab-runner.exe** 然後丟進去

用系統管理員的身份打開 CMD，前往該資料夾然後執行以下指令

    .\gitlab-runner.exe install
    .\gitlab-runner.exe start

你也可以用你的帳戶登錄，只要把第一行改為

    .\gitlab-runner.exe install --user ENTER-YOUR-USERNAME --password ENTER-YOUR-PASSWORD

到此，Runner 的部分準備好了，但他還不知道他要去哪裡做事，因此[下一步](/step2/README.md)我們要把 Runner 跟我們專案連接起來。
