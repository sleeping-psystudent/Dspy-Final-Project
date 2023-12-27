# ❤️‍🔥1992-2020新興韓團火熱程度關聯分析❤️‍🔥

**作者**：歷史二 [王學謙](https://github.com/Ken7222)、心理五 [李采蓉](https://github.com/sleeping-psystudent)、地理碩一 [賴郁升](https://github.com/yusheng1027)<br>
**報告日期**：2023/12/21
- 👉[Github](https://github.com/sleeping-psystudent/Dspy-Final-Project.git)👈
- 👉[Proposal](https://github.com/sleeping-psystudent/Dspy-Final-Project/blob/main/Proposal.md)👈<br>
- 👉[Report](https://github.com/sleeping-psystudent/Dspy-Final-Project/blob/main/Final%20Report.pdf)👈<br>
###### tags: `Introduction to programming for data science`

---

## 📖 目錄
- [研究動機](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%AA%A9-%E7%A0%94%E7%A9%B6%E5%8B%95%E6%A9%9F)
- [資料選用](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%AA%A9-%E8%B3%87%E6%96%99%E9%81%B8%E7%94%A8)
    - [主要資料集](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%E4%B8%BB%E8%A6%81%E8%B3%87%E6%96%99%E9%9B%86)
    - [次要資料集](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%E6%AC%A1%E8%A6%81%E8%B3%87%E6%96%99%E9%9B%86)
- [分析方法](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%AA%A9-%E5%88%86%E6%9E%90%E6%96%B9%E6%B3%95)
    - [資料預處理](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%92%A0-%E8%B3%87%E6%96%99%E9%A0%90%E8%99%95%E7%90%86)
    - [初步分析](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%92%A0-%E5%88%9D%E6%AD%A5%E5%88%86%E6%9E%90)
    - [多元迴歸分析](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%92%A0-%E5%A4%9A%E5%85%83%E8%BF%B4%E6%AD%B8%E5%88%86%E6%9E%90)
- [結論](https://hackmd.io/@895n2PoiTf6zr08FjTMQ_Q/B1pipknLT#%F0%9F%AA%A9-%E7%B5%90%E8%AB%96)

---

## 🪩 研究動機

K-pop潮流近年來席捲全世界，然而除了廣為人知的頂流團體，每年也有許許多多中小團體推陳出新，激烈競爭之下要如何殺出一片血路是許多人不斷探討的問題。本研究專案利用kaggle上所取得的資料集，搭配Youtube所爬蟲取得的點閱率、讚數、留言數等等數據，試圖簡單歸納出一個韓團的成功要素。

## 🪩 資料選用

### 主要資料集
採用資料集：[K-Pop Database (1992-2020)](https://www.kaggle.com/datasets/kimjihoo/kpopdb/data)<br>
根據kaggle上的說明，此份資料整理自[K-Pop Database](https://dbkpop.com/)<br>

這次分析探討中使用的三個檔案，其欄位表如下：

💁‍♂️ **kpop_idols_boy_groups.csv**
|﻿Name|Short|Debut|Company|Members|Orig. Memb.|Fanclub Name|Active|
|----|----|----|----|----|----|----|----|

這份資料共紀錄147個男性組成韓國流行樂團體

💁‍♀️ **kpop_idols_girl_groups.csv**
|﻿Name|Short|Debut|Company|Members|Orig. Memb.|Fanclub Name|Active|
|----|----|----|----|----|----|----|----|

這份資料共紀錄152個女性組成韓國流行樂團體

🎵 **kpop_music_videos.csv**
|Date|Artist|Song Name|Korean Name|Director|Video|Type|Release|
|----|----|----|----|----|----|----|----|

這份資料共紀錄3443筆韓國流行樂影片

### 次要資料集

利用YouTube Data API，將**kpop_music_videos.csv**所提供`Video`中的網址，爬下其`Views`、`Likes`、`Comments`的數量，輸出做成**youtube.csv**。過程中我們發現有些影片會鎖點閱率、點讚數、評論區等等，於是我們將有這種情況的資料皆刪除。

次外，我們也分配一人查找99個團的成員出道年齡，最後整合成包含每個團體出道時平均年齡，使這個欄位命名為`Average_age`。


## 🪩 分析方法

我們主要想從五個因素下手，去分析其與「團體火熱程度」的關聯性，五個因素如下：
1) 性別 `Gender`
2) 出道平均年齡 `Age`
3) 團體人數（取出道時的原始人數）`Original Member`
4) 出道年份 `Year`
5) 經紀公司 `Company`

而「團體火熱程度」我們利用`Views`、`Likes`、`Comments`將之定調為 $\dfrac{MV點閱率or點讚數or留言數}{(2020-發佈年份)}$

### 💠 資料預處理
合併**kpop_idols_boy_groups.csv**和**kpop_idols_girl_groups.csv**的過程中，我們新增`Gender`欄位並分別標上M和F。爾後除掉多餘欄位留下`Name`、`Debut`、`Compnay`、`Orig. Member`、`Gender`，並且利用pd.factorize將`Company`轉化為`Company Code`，`Name`則設為index。我們也將次要資料集的`Average_age`加入主要資料集。最後資料集長相如下：

|Name|Debut|Company|Orig.Memb.|Average_age|Gender|Company Code|
|---|---|---|---|---|---|---|

針對另個次要資料集**youtube.csv**，在未處理前其長相如下：

|Name|Date|Likes|Views|Comments|
|---|---|---|---|---|

我們寫了一個迴圈，針對主要資料集中的團體，假若此團體有歌曲被記錄在**youtube.csv**中，便將這些歌曲抓出來，並且計算距今已被發佈幾年作為欄位`Years`。如下，我們查看(G)I-DLE有哪幾首歌，以及其他數據。

<center>
    
![圖片](https://hackmd.io/_uploads/HkBgVpHPT.png =70%x)

</center>

我們的計算方式為，先算出每首歌平均年點閱率、讚數、留言數，接著再將欄位各自相加取平均。假若該團體沒有任何一首歌被收錄進此資料集中，便去除此團體。最後剩下**239**個韓國流行樂團體。

```python=
yt["Years"]=0
yt["Avg_L"]=0
yt["Avg_V"]=0
yt["Avg_C"]=0
Factors["Likes"]=0
Factors["Views"]=0
Factors["Comments"]=0
for name in Factors.index:
    if name in yt.index:
        yt.at[name, "Years"]=yt.at[name, "Release Year"]-Factors.at[name, "Debut Year"]+1
        # Likes
        yt.at[name, "Avg_L"]=yt.at[name, "Likes"]/yt.at[name, "Years"]
        Factors.at[name, "Likes"]=yt.at[name, "Avg_L"].mean().round().astype(int)
        # Views
        yt.at[name, "Avg_V"]=yt.at[name, "Views"]/yt.at[name, "Years"]
        Factors.at[name, "Views"]=yt.at[name, "Avg_V"].mean().round().astype(int)
        #Comments
        yt.at[name, "Avg_C"]=yt.at[name, "Comments"]/yt.at[name, "Years"]
        Factors.at[name, "Comments"]=yt.at[name, "Avg_C"].mean().round().astype(int)

    else:
        Factors.drop(name, inplace=True)
```

### 💠 初步分析

#### 描述統計

##### 💁‍♂️ 男團
- 男團出道平均年齡最小的年份：1995，平均年齡：14.00
- 男團出道平均年齡最大的年份：2010，平均年齡：22.00
![圖片](https://hackmd.io/_uploads/rJptHTHDa.png)
- 男團平均出道年齡樣本數據的算術平均數為: 20.959183673469386
- 男團平均出道年齡樣本數據之中位數為: 21.0
- 男團平均出道年齡樣本數據中出現最頻繁的眾數為: 20.0
![圖片](https://hackmd.io/_uploads/SyjcHpSwa.png)
- 男團平均出道年齡樣本數據中最大值減去最小值之範圍為: 13.0
- 男團平均出道年齡樣本數據之四分位數 Q1: 20.0
- 男團平均出道年齡樣本數據之四分位數 Q2 (中位數): 21.0
- 男團平均出道年齡樣本數據之四分位數 Q3: 22.0
- 男團平均出道年齡樣本數據之標準差: 2.347027504977562
- 男團平均出道年齡樣本數據之變異數: 5.5085381091212
- 男團平均出道年齡樣本數據之偏度: -0.38980768104145425
- 男團平均出道年齡樣本數據之峰度: 0.7979371586820543

<center>

|平均年齡最小的公司（前五名）|平均年齡最大的公司（前五名）|
|-----------------------|-----------------------|
|SS                13.0|JJ Holic          26.0|
|MBK, Turbo Co.    14.0|J-Star            26.0|
|Music K           17.0|Jackpot           26.0|
|Pledis            17.5|Brand New, RBW    26.0|
|DSP, YG           18.0|Elen              25.0|
    
</center>

---

##### 💁‍♀️ 女團

- 女團出道平均年齡最小的年份：1997，平均年齡：16.16
- 女團出道平均年齡最大的年份：2006，平均年齡：23.00
![圖片](https://hackmd.io/_uploads/HkrnwaHPp.png)
- 女團平均出道年齡樣本數據的算術平均數為: 20.024026845637582
- 女團平均出道年齡樣本數據之中位數為: 20.0
- 女團平均出道年齡樣本數據中出現最頻繁的眾數為: 20.0
![圖片](https://hackmd.io/_uploads/BJeSTprDT.png)
- 女團平均出道年齡樣本數據中最大值減去最小值之範圍為: 15.0
- 女團平均出道年齡樣本數據之四分位數 Q1: 18.512500000000003
- 女團平均出道年齡樣本數據之四分位數 Q2 (中位數): 20.0
- 女團平均出道年齡樣本數據之四分位數 Q3: 21.0
- 女團平均出道年齡樣本數據之標準差: 2.416796870994948
- 女團平均出道年齡樣本數據之變異數: 5.84090711565097
- 女團平均出道年齡樣本數據之偏度: 0.3017751082266939
- 女團平均出道年齡樣本數據之峰度: 0.49614939631576194

---

#### 相關分析
- 下圖為出道團體人數與年份之間的散佈圖，團體人數很長一段時間都落在平均之下。隨著韓團數量的增加，人數還是集中在平均上下，但也出現一些人數更多的團體，此情況在男團更為明顯。
![圖片](https://hackmd.io/_uploads/Sk4VC3BDp.png)
- 下圖為出道團體平均年齡與年份之間的散佈圖，男團的平均年齡較女團略高，但綜合而言皆落在20歲的區間中。隨著年份，韓團的數量增加外，也出現更廣的出道平均年齡範圍。
![圖片](https://hackmd.io/_uploads/H1LH0hBP6.png)
- 接著我們對團體的出道平均年齡和團體人數畫散佈圖，在不同性別間呈現不太一樣的集中趨勢，女性會較男性更為分散，反應在團體人數跟出道年齡上女團較為多元。
![圖片](https://hackmd.io/_uploads/Hy0rCnrw6.png)

- 針對我們所選取的五個變項做相關矩陣，值得注意的是`Company`和`Gender`間的相關為-0.5，`Company`和`Debut Year`間的相關為0.52，皆為中度相關。
<center>
    
![圖片](https://hackmd.io/_uploads/Hy8s467Pp.png)
    
</center>


### 💠 多元迴歸分析
在這個階段我們將針對上述五因素針對「團體火熱程度」進行多元迴歸分析。先畫一個相關矩陣查看變項間的關係，令人意外的是，`Likes`、`Views`、`Comments`之間為完全相關。

<center>
    
![圖片](https://hackmd.io/_uploads/BkXBSOWwa.png)
    
</center>

我們利用LinearRegression來做多元迴歸，Y變項分別放入`Likes`、`Views`、`Comments`，先前做的相關矩陣幫助我們預測出來的結果會非常相近。

```python=
# 設X和Y
X=Factors[["Member Number", "Average Age", "Gender", "Company Code", "Debut Year"]]
Y=Factors[["Likes"]]

# 訓練多元迴歸模型
regressor = LinearRegression()
regressor.fit(X,Y)

accuracy = regressor.score(X,Y)
print('Score: ', accuracy)
print('Accuracy: ' + str(accuracy * 100) + '%')
```

以下是我們得到的預測準確率，非常的低，不到1%，可以說這五個X變項幾乎無法幫助我們判斷一個團體是否會火起來。

|Y|X|Accuracy|
|-|-|-----|
|Likes|Member Number, Average Age, Gender, Company, Debut Year|0.4734814692184175%|
|Views|Member Number, Average Age, Gender, Company, Debut Year|0.4734814691657152%|
|Comments|Member Number, Average Age, Gender, Company, Debut Year|0.4734814692189837%
## 🪩 結論

1) 男團近年來的出道年紀多落在21-22區間，而女團則是落於20歲為主。簡而言就是女團組合在近年來大致都比男團組合年輕，但女團成員的年齡差異也比男團來得大。
2) 團體成員的年齡組合，在女團的分布較為集中，男團較為分散。可能與訓練時長、經紀公司、男性入營與團體活動有關。
3) 公司與性別、公司跟出道年份存在較高的相關，推測前者與小公司多半只有推出一個團體，沒有火起來就後繼無力。後者則是與在2008年後許多公司如雨後春筍般冒出的趨勢有關，關於為何2008年後韓團數量增加，推測與該年所推出的「文化藝術振興法」有關，韓國的影視、音樂、文化從這之後被推廣到全世界，許多小型公司也趁勝追擊推出團體加入競爭。
4) 我們所選擇的五個X變項：出道人數、平均出道年齡、性別、公司、出道年份表現不佳，推測多元迴歸分析結果那麼慘的原因有二：一是樣本數太少，在做完一連串處理後僅剩239筆男團女團；二是我們的資料集來源本身可靠度就不是那麼高，僅7.06分
5) 假若往後要持續針對這個主題進行研究，可以考慮做進一步的特徵選擇，以及增加youtube影片部分的樣本，這部分kaggle所給的資料集不太可靠，並沒有將一個團體在2020年前所有的youtube影片列出。

