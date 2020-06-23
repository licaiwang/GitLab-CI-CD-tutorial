# 建立 CI/CD Pipeline
----
GitLab CI 預設會檢查 Project 內是否含有檔名為 .**gitlab-ci.yml** 的檔案，並根據該檔案所定義的內容自動建立 CI/CD Pipeline。

## 撰寫 .gitlab-ci.yml 
----
**stages：**
* stages 表示任務構建的階段。一次 pipeline 中允許定義多個 stages，這些 stages 會有以下特點：
    
    * **所有 stages 會按照順序運行，一個 stage 完成後，下一個 stage 才開始**

    * **所有 stages 完成後，該 pipeline 才會成功**

    * **任一個 stage 失敗，後面的 stages 皆不會執行，該 pipeline 失敗**
        ```
        stages:
          - build
          - test
        ```

**job：**
* jobs 表示構建工作，表示某個 stage 裡面執行的工作。我們可以在 stages 裡面定義多個 jobs，這些 jobs 會有以下特點：

    * **相同 stage 中的 jobs 會同時執行**

    * **相同 stage 中的 jobs 都執行成功時，該 stage 才會成功**

    * **任一 job 失敗，則該 stage 失敗，即該 pipeline 失敗**

* jobs 的定義：

    * **定義了在什麼條件下才能執行它們的**
    
    * **必須至少包含 script 這個關鍵字**

    * **不受定義數量的限制，也可以自己定義名稱 (除了關鍵字外)**
        ```
        stg-build:
          stage: build
          script: python test.py
        ```
**artifacts：**
* artifacts 可以在 job 裡附加你的檔案，該檔案只能在該 job 裡使用，想傳遞到其他 job 的話請參考。
    ```
        artifacts:
            // 這個工作目錄下所有名稱為 test 的檔案
            paths:
             - test.*
            // 有效期限：7 天
            expire_in: 
             - 1 week
    ```
**image：**
* 可以從 Docker 上直接拿你需要的鏡像檔建置 pipeline 環境

    ```
    image: "python:3.7"
    ```

更多的功能請參照[官方文件](https://blog.csdn.net/xl_lx/article/details/78329089)，但目前我們就先使用這四個。

```
// 運行環境
image: "python:3.7"

// 我有一個階段
stages:
  - build
  - 
// job1
stg-build:
  stage: build
  // 跑我的主程式
  script: python test.py
  // 主程式的位置
  artifacts:
    paths:
     - test.*
```
如此，你上傳的程式碼便會自動運行 test.py 這隻程式，如果有誤的話，便會造成 pipeline 失敗

![1.jpg](/step3/1.jpg)

你可以看到目前只有 build 這個 stages，也只有一個 Job，但有時候我們的程式也許語法沒錯，但是邏輯有誤，造成**輸入** != **我們想要的輸出**，此時我們應該要使用[單元測試](https://zh.wikipedia.org/wiki/%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)來為每一個 function 做驗證。

下一步我們將實作 python 的單元測試並將其加入 pipeline 中
