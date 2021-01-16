# 資財三乙 107AB0734 陳韋堯 期末

## run_complete_detector.sh
要執行的檔案為run_complete_detector.sh
從下圖的內容可以看到執行的主程式是 complete_detector.py 後面則是執行complete_detector.py時要用到的執行指令與執行檔案內容

![](https://i.imgur.com/GtO014P.png)

## complete_detector.py
```
vim complete_detector.py 
```
### get_string_features 
![](https://i.imgur.com/LPB63JV.png)
get_string_features這個副程式是用於執行提取檔案的特徵值，在於一開始先會使用regular expression去提取檔案的字作為特徵，提取完後會將這些字存在dictionary中去做雜湊形成特徵值的訊息摘要，在轉換為陣列方便後續作為比較。

### scan_file
![](https://i.imgur.com/3CKEw3W.png)
這是掃描單個檔案是否為惡意程式的副程式，如果我沒想錯的話
這個scan_file的副程式，會先去檔案的路經抓取檔案內容，再將檔案內容使用get_string_features 去抓取特徵，去預測其是惡意程式的可能性。

### train_detector
![](https://i.imgur.com/SYj3Ump.png)
train_detector這副程式是用來訓練detector的，首先先用get_training_paths與抓取檔案，再抓這些檔案的內容的特徵值，之後再用RandomForest的方式去進行訓練。

### cv_evaluate
![](https://i.imgur.com/YZJQJFK.png)
cv_evaluate這個副程式，首先會先將檔案經過KFold的交叉驗證用RandomForest的方式得出更多數據的訓練，再去用預測出來的可能性的scores與test_y去使用ROC去分類到底檔案是惡意的還是良性的，最後在畫出ROC curves的圖。

### get_train_data
![](https://i.imgur.com/dsCtFsn.png)
拿取malware_paths與benignware_paths檔案的資料，之後再分為X與Y的兩堆。
- X：檔案的特徵值
- Y：malware_paths內1的數量+benignware_paths內0的數量

### 其他
![](https://i.imgur.com/Ien9Tj5.png)
設定執行檔案時的額外指令

### 主要執行內容
![](https://i.imgur.com/RO0S50P.png)
判斷執行時輸入的內容，去決定要執行哪一個副程式，以這次作業中run_complete_detector.sh的內容來舉例，因為有輸入以下三個參數。
- args.malware_paths
- args.benignware_paths
- args.evaluate
  
所以會執行ev_evaluate的副程式

## 執行結果
透過執行run_complete_detector.sh後
```
run_complete_detector.sh
```
會出現以下的執行結果，從執行結果中就能看到
![](https://i.imgur.com/suzBUoe.png)
