# 107ab0756 吳秉儒 資安期末作業
### **執行run_complete_detector.sh**
- 這邊要執行ch08/code底下名為==run_complete_detector.sh==的檔案。
下圖是執行 complete_detector.py ，後面則是執行complete_detector.py時要用到的指令與檔案內容。
![](https://imgur.com/DcemCaS.png)
-------
### **complete_detector.py**
``` 
vim complete_detector.py 
```
### get_string_features
![](https://imgur.com/q47IjOf.png)
- get_string_features這個副程式是用於執行提取檔案的特徵值，在於一開始先會使用regular expression去提取檔案的字作為特徵，提取完後會將這些字存在dictionary中去做雜湊形成特徵值的訊息摘要，在轉換為陣列方便後續作為比較。
-------
### scan_file
![](https://camo.githubusercontent.com/55625bd698c247e0500092617decb9fe45c335d7c0df8b00e3fcffa0f6a87e40/68747470733a2f2f692e696d6775722e636f6d2f33434b457733572e706e67)
- 這是掃描單個檔案是否為惡意程式的副程式，如果我沒想錯的話 這個scan_file的副程式，會先去檔案的路經抓取檔案內容，再將檔案內容使用get_string_features 去抓取特徵，去預測其是惡意程式的可能性。
----
### train_detector
![](https://camo.githubusercontent.com/4b9ad745cca85181978de859246c147ca55b641fc7a81d4c78f70db2d571cff9/68747470733a2f2f692e696d6775722e636f6d2f53596a33556d702e706e67)
- train_detector這副程式是用來訓練detector的，首先先用get_training_paths與抓取檔案，再抓這些檔案的內容的特徵值，之後再用RandomForest的方式去進行訓練。
----
### cv_evaluate
![](https://camo.githubusercontent.com/239e19534b247109b9bcbf4ca9dca22e0704020fbae535daf8b22b934ab634a8/68747470733a2f2f692e696d6775722e636f6d2f595a4a514a464b2e706e67)
- cv_evaluate這個副程式，首先會先將檔案經過KFold的交叉驗證用RandomForest的方式得出更多數據的訓練，再去用預測出來的可能性的scores與test_y去使用ROC去分類到底檔案是惡意的還是良性的，最後在畫出ROC curves的圖。
---
### get_train_data
![](https://camo.githubusercontent.com/7a9bfb5e787892fa1f9b87e2576e5871e8cdcf75801477a33d050ade85ef47a0/68747470733a2f2f692e696d6775722e636f6d2f6473437446736e2e706e67)
- 拿取malware_paths與benignware_paths檔案的資料，之後再分為X與Y的兩堆。
 --X：檔案的特徵值
 --Y：malware_paths內1的數量+benignware_paths內0的數量
 
 ---
 ### 其他
 ![](https://camo.githubusercontent.com/a188a8718ad23a206cfba05db133669f69674da8f27fb50a41b02d63cf6d984b/68747470733a2f2f692e696d6775722e636f6d2f49656e39546a352e706e67)
- 設定執行檔案時的額外指令
---
### 主要執行內容
![](https://camo.githubusercontent.com/5a6930c01b1be9fcd455e065bdab6099ebcd2044eb650d13dd1cc4a801a38338/68747470733a2f2f692e696d6775722e636f6d2f524f30533530502e706e67)
- 判斷執行時輸入的內容，去決定要執行哪一個副程式，以這次作業中run_complete_detector.sh的內容來舉例，因為有輸入以下三個參數。
    ==args.malware_paths
    args.benignware_paths
    args.evaluate==
所以會執行ev_evaluate的副程式
---
### 執行結果
- 執行run_complete_detector.sh後
![](https://camo.githubusercontent.com/7fe2530d7ff4acab954925118cb81d7ff2736d1490295673165624f94ad65346/68747470733a2f2f692e696d6775722e636f6d2f73757a42556f652e706e67)
---
# 心得
每次上資安課都能聽到很多從沒聽過的東西，加上老師會將時事結合到課堂中，把很多資安的概念帶到日常。雖然每次我的虛擬機不知道為啥打不開，害我都得跟同學一起做，有夠不方便。總結來說，我很喜歡老師這樣想要教什麼就教甚麼的方式。
(拜託老師給我高分一點＞＜)
