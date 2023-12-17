# ❤️‍🔥1992-2020新興韓團火熱程度關聯分析❤️‍🔥
**作者**：歷史二 [王學謙](https://github.com/Ken7222)、心理五 [李采蓉](https://github.com/sleeping-psystudent)、地理碩 [賴郁升](https://github.com/yusheng1027)<br>
**報告日期**：2023/12/21
- 👉[Github](https://github.com/sleeping-psystudent/Dspy-Final-Project.git)👈
- 👉[Proposal](https://github.com/sleeping-psystudent/Dspy-Final-Project/blob/main/Proposal.md)👈<br>
###### tags: `Introduction to programming for data science`

---

## 🪩 研究動機

K-pop潮流近年來席捲全世界，然而除了廣為人知的頂流團體，每年也有許許多多中小團體推陳出新，激烈競爭之下要如何殺出一片血路是許多人不斷探討的問題。本研究專案利用kaggle上所取得的資料集，搭配Youtube所爬蟲取得的點閱率、讚數、留言數等等數據，試圖簡單歸納出一個韓團的成功要素。

## 🪩 資料選用

採用資料集：[K-Pop Database (1992-2020)](https://www.kaggle.com/datasets/kimjihoo/kpopdb/data)<br>
根據kaggle上的說明，此份資料整理自[K-Pop Database](https://dbkpop.com/)<br>

這次分析探討中使用的三個檔案，其欄位表如下：

💁‍♂️ **kpop_boy_groups.csv**
|﻿Name|Short|Debut|Company|Members|Orig. Memb.|Fanclub Name|Active|Average_age
|----|----|----|----|----|----|----|----|----|

這份資料共紀錄147個男性組成韓國流行樂團體

💁‍♀️ **kpop_girl_groups.csv**
|﻿Name|Short|Debut|Company|Members|Orig. Memb.|Fanclub Name|Active|Average_age
|----|----|----|----|----|----|----|----|----|

這份資料共紀錄152個女性組成韓國流行樂團體

🎵 **youtube.csv**
|Name|Likes|Views|Comments|
|----|----|----|----|

這份資料共紀錄3443筆韓國流行樂影片


## 🪩 分析方法

我們主要想從五個因素下手，去分析其與「團體火熱程度」的關聯性，五個因素如下：
1) 性別 `Gender`
2) 出道平均年齡 `Age`
3) 團體人數（取出道時的原始人數）`Original Member`
4) 出道年份 `Year`
5) 經紀公司 `Company`

而「團體火熱程度」我們將之定調為`mv`中出現該團的MV點閱率，資料以youtube爬蟲方式取得，算法為 $\dfrac{MV點閱率}{(2020-出道年份)}$
### 初步分析

#### 描述統計


#### 相關分析



### 最終分析
在這個階段我們將針對上述五因素針對「團體火熱程度」進行多元迴歸分析。

## 🪩 結論
