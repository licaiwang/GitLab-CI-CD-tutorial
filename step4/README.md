# 在 Pipeline 中運行單元測試


### 什麼是單元測試？
---
單元測試就是所謂的 **Unit Test**

一個單元測試就是一段程式碼，這段程式碼呼叫了另一段程式碼，用來**驗證**某些假設的正確性。如果這些假設是錯的，單元測試就會失敗。

你可以在[這裡](https://openhome.cc/Gossip/CodeData/PythonTutorial/UnitTestPy3.html)找到更多的資訊

### 我要如何在 python 上寫單元測試？
---
假設我現在有一個簡單的計算機程式，裡面有 4 個 function

```
def add_int(x, y):
    return x + y


def sub_int(x, y):
    return x - y


def mul_int(x, y):
    return x * y


def div_int(x, y):
    return x / y

```
顯然的，如果我要測試這 4 個 function，我必須每次編譯完成後都要手動去按我的計算機看看是否正確，同時不同的輸入也有可能會有例外狀況發生 - **例如：0/5** ，這樣子每次都要手動作測試是很浪費時間的，因此要是能夠先把所有的輸入輸出狀況想好，並寫好驗證的方法，我要驗證時只需一個動作就好了！

```
import unittest
// 要測試的檔案
import test

class TestCalculator(unittest.TestCase):

    def test_add_int(self):
        result = test.add_int(1,4)
        self.assertEqual(result,5)

    def test_sub_int(self):
        result = test.sub_int(4,1)
        self.assertEqual(result,3)

    def test_mul_int(self):
        result = test.mul_int(2,4)
        self.assertEqual(result,8)

    def test_div_int(self):
        result = test.div_int(4,4)
        self.assertEqual(result,1)

if __name__ == '__main__':
    unittest.main()
```
當你在本地端運行這個單元測試的時候，你會得到以下輸出

![1.jpg](/step4/1.jpg)

### 一些常用的 function
---
檢查結果是否符合預期，通常使用這四個 function 

    assertTrue(expr)                 expr 是否為真
    assertFalse(expr)                expr 是否為非
    assertEqual(first, second)       first 是否 = second
    assertNotEqual(first, second)    first 是否 != second

在[這裡](https://imsardine.wordpress.com/tech/unit-testing-in-python/)你可以找到更多的 function 使用，但光這四個就很好用了。

### 讓 pipeline 跑我的單元測試

修改上一步寫的 .gitlab-ci.yml

```
image: "python:3.7"

stages:
  - build
  - test

stg-build:
  stage: build
  script: python test.py
  artifacts:
    paths:
     - test.*

stg-test:
  stage: test
  script: python myTest.py
  artifacts:
    paths:
     - myTest.*
```

運行結果

![2.jpg](/step4/2.jpg)

到此，我們有了簡單的 pipeline 來協助我們做程式碼的檢查了，接下來會介紹一些小細節在進入 cd 的部分 (~ 暫時告一段落，中場休息時間)