# 1992-2020新興韓團火熱程度關聯分析

作者：歷史二 [王學謙](https://github.com/Ken7222)、心理五 [李采蓉](https://github.com/sleeping-psystudent)、地理碩 [賴郁升](https://github.com/yusheng1027)

## 研究動機

K-pop潮流近年來席捲全世界，然而除了廣為人知的頂流團體，每年也有許許多多中小團體推陳出新，激烈競爭之下要如何殺出一片血路是許多人不斷探討的問題。本研究專案利用kaggle上所取得的資料集，搭配Youtube所爬蟲取得的點閱率、讚數、留言數等等數據，試圖簡單歸納出一個韓團的成功要素。

## 理論方法與設計
### 資料選用
#### 主要資料集
採用資料集：[K-Pop Database (1992-2020)](https://www.kaggle.com/datasets/kimjihoo/kpopdb/data)<br>
根據kaggle上的說明，此份資料整理自[K-Pop Database](https://dbkpop.com/)<br>
- 四份檔案
  + kpop_idols.csv
  + kpop_idols_boy_groups.csv (以下簡稱`boy`)
  + kpop_idols_girl_groups.csv (以下簡稱`girl`)
  + kpop_music_videos.csv (以下簡稱`mv`)
 
這次分析探討中僅會使用其中三個檔案，其欄位表如下：

💁‍♂️ **kpop_idols_boy_groups.csv**
|﻿Name|Short|Korean Name|Debut|Company|Members|Orig. Memb.|Fanclub Name|Active
|----|----|----|----|----|----|----|----|----|

這份資料共紀錄147個男性組成韓國流行樂團體

💁‍♀️ **kpop_idols_girl_groups.csv**
|﻿Name|Short|Korean Name|Debut|Company|Members|Orig. Memb.|Fanclub Name|Active
|----|----|----|----|----|----|----|----|----|

這份資料共紀錄152個女性組成韓國流行樂團體

🎵 **kpop_music_videos.csv**
|﻿Date|Artist|Song Name|Korean Name|Director|Video|Type|Release
|----|----|----|----|----|----|----|----|

這份資料共紀錄3772筆韓國流行樂影片

#### 次要資料集
除此之外我們也將手動根據`boy`以及`girl`所列出團體，收集他們出道當年的團員平均年齡。收集資料任務分配如下：
- 李采蓉：`girl`: index 2-101
- 賴郁升：`girl`: index 102-153, `boy`: index 102-148
- 王學謙：`boy`: index 2-101<br>

資料將先分別存於.txt檔中，格式為
|﻿Group|Age
|----|----|

### 分析方法

我們主要想從五個因素下手，去分析其與「團體火熱程度」的關聯性，五個因素如下：
1) 性別 `Gender`
2) 出道平均年齡 `Age`
3) 團體人數（取出道時的原始人數）`Original Member`
4) 出道年份 `Year`
5) 經紀公司 `Company`

其中除(2)外，其餘資料可從主要資料集取得。<br>

而「團體火熱程度」我們將之定調為`mv`中出現該團的MV點閱率，資料以youtube爬蟲方式取得，算法為 $\dfrac{MV點閱率}{(2020-發佈年份)}$
#### 初步分析

##### 描述統計
首先我們將進行一些簡易的描述分析，將變項基本統計量算出。

##### 相關分析
畫scatter plot，以及correlation matrix<br>

工作分配：
- 李采蓉：相關分析
- 賴郁升：描述統計
- 王學謙：Youtube爬蟲

#### 最終分析
在這個階段我們將針對上述五因素針對「團體火熱程度」進行多元迴歸分析。

## 問題與討論

2023/11/19 updated!!!
1) 除此之外，火熱程度其實可以去爬`MV`中的歌曲點閱率，以 $\dfrac{MV點閱率}{(2020-出道年份)}$ 量化。
2) 經紀公司作為類別變項，要如何轉化成數值需要討論，不然就得刪掉不用了。 -> linear mixed model

2023/11/26 updated!!!
1) 部分Youtube所爬得的資料有點閱率、讚數、留言數的缺失。


## 時間表
✅：已完成 ❌：未完成

|日期|進度|是否完成
|---|---|---|
|2023/11/19|進行小組規劃討論|✅|
|2023/11/21|14:30博雅一樓office hour|✅|
|2023/11/19|進行小組規劃討論|✅|
|2023/11/26|完成平均出道年齡資料集|✅|
|2023/12/01|github資料集整理|✅|
|2023/12/07|上臺口頭propose|✅|
|2023/12/21|期末專案成果報告|❌|
