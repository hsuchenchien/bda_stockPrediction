# 大數據與商業分析期中專案 - 以新聞報導做股價預測
本專案目標為以新聞文章來預測股票未來的表現：  
資料集：群創（股票代號：3481）在2021年所有 bbs, forum 中新聞文章  
資料前處理：  
 1. 將群創 2021 年的股價表現整理後，得出該股在哪幾天的股價起伏超過 0.5%，分別將股價漲幅大於0.5%前一天的新聞標示為「漲」；股票跌幅大於0.5%前一天的新聞標示為「跌」；其他則標示為「停」
 2. 將這些日期的所有新聞資料都取出，並以 keyword '群創‘, '面板' 將與群創相關的所有新聞資料取出  
----------------------------------------  
模型使用：BernoulliNB, kNN, SVM, Decision Tree, GradientBoostingClassifier  
模型建立：  
 1. 將新聞資料利用 monpa, ckiptagger 斷詞
 2. 將斷詞好的 token 以 TFIDF 評估 token 重要性，並依重要性取出 10000 個 token
 3. 將新聞資料丟入模型訓練，並算出準確率
-----------------------------------------
預測結果（以混淆矩陣方式呈現）：
 1. BernoulliNB

|          | 真實為停 | 真實為漲 | 真實為跌 |
|----------|:-------:|:-------:|---------:|
| 預測為停 | 12 | 26 | 17 |
| 預測為漲 | 1 | 62 | 174 |
| 預測為跌 | 0 | 47 | 207 |
測試模型20次後得到平均準確率為0.5080

 2. SVM Linear:  
  
  | precision  | precision  | recall  || F1-score  | support  |  
  | ---------  | ---------  | ------  || --------  | -------  |  
  | 漲  | 0.66  | 0.39  || 0.49  | 1230  |  
  | 跌  | 0.25  | 0.51  || 0.33  | 490  |  
  | accurancy  |   |   || 0.42  | 1720  |  
  | macro avg  | 0.46  | 0.45  || 0.41  | 1720  |  
  | weighted avg  | 0.55  | 0.42  || 0.44  | 1720  |  
 
 3. SVM RBF

|          | 真實為停 | 真實為漲 | 真實為跌 |
|----------|:-------:|:-------:|---------:|
| 預測為停 | 36 | 6 | 13 |
| 預測為漲 | 0 | 54 | 183 |
| 預測為跌 | 0 | 14 | 240 |
測試模型20次後得到平均準確率為0.6035

 4. Decision Tree

|          | 真實為停 | 真實為漲 | 真實為跌 |
|----------|:-------:|:-------:|---------:|
| 預測為停 | 11 | 30 | 14 |
| 預測為漲 | 12 | 182 | 43 |
| 預測為跌 | 11 | 173 | 70 |
測試模型20次後得到平均準確率為0.4692

 5. kNN

|          | 真實為停 | 真實為漲 | 真實為跌 |
|----------|:-------:|:-------:|---------:|
| 預測為停 | 1 | 44 | 21 |
| 預測為漲 | 2 | 186 | 47 |
| 預測為跌 | 1 | 172 | 72 |
測試模型20次後得到平均準確率為0.4769
