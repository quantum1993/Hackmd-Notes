# 筆記: Colloquium: Statistical mechanics of money, wealth, and income
[Paper連結](https://arxiv.org/pdf/0905.1518.pdf)

## Outline
[TOC]

## Brief Intro
- Author: Victor M. Yakovenko(Department of Physics), J. Barkley Rosser, Jr.(Department of Economics)
- Dated: 24 December 2009
- Summary: 
    - 這篇文章整理了自1990年後期以來，經濟物理學(econophysics)所發展出的金錢、財富及收入分布統計模型。
    - 藉由與Boltzmann-Gibbs能量分布類比，內文展示了金錢的機率分布在某些階級呈現exponential樣貌。
    - 另外，資料分析結果顯示，財富與收入分布呈現雙階級分布。
        - 多數人屬於低等階級，呈現exponential分布(thermal)，不隨時間變化(穩態)
        - 少數人屬於高等階級，呈現power-law分布(superthermal)，會隨時間變化(非穩態)

> “Money, it’s a gas.” Pink Floyd, Dark Side of the Moon


## Content
### Historical Introduction
- **經濟物理學**(econophysics)最早由理論物理學家Eugene Stanley在1995年，Dynamics of Complex Systems會議上提出
- 後續Stanley(1996)寫了一篇文章主張:
  "behavior of large numbers of humans (as measured, e.g., by economic indices) might conform to analogs of the scaling laws that have proved useful in describing systems composed of large numbers of inanimate objects"
- 經濟物理學並不像生物物理學，直接應用物理基礎定律(例如牛頓力學、量子力學等)，它應用的是統計物理的數學手法，去研究複雜的經濟系統
- 另一個常跟經濟物理學一起提到的是**社會物理學**(sociophysics)，由理論物理學家Serge Galam在1982年提出
- 統計這個詞彙是在18世紀因為研究出生、死亡結婚率等人口指標所發展出來的
- 在1850年前，統計一直被認為是政治經濟學的左右臂膀，爾後才逐漸演變成一門分析學科，這也刺激了19世紀後半統計力學的發展
- 物理領域的統計力學是由James Clerk, Maxwell, Ludwig Boltzmann, and Josiah Willard Gibbsy在19世紀末期發展出來的
- Maxwell當初研究統計力學很大一部分是受到社會統計(social statistics)的啟發，Boltzmann在此之上更進一步提到：
    "The molecules are like individuals, . . . and the properties of gases only remain unaltered, because the number of these molecules, which on the average have a given state, is constant."
- Philip Bally在2004年的文章提到，物理學與經濟學演化到後期愈來愈專精，大家已忘記當初發展的同源關係．在20世紀，有一些人開始嘗試再次把經濟與物理學連結在一起．例如諾貝爾化學獎Frederick Soddy(1877~1956)在著作*Wealth, Virtual Wealth and Debt*裡認為[真實財富的衡量應基於人類利用能量加工原料而得到的實物與服務](https://zh.wikipedia.org/wiki/%E8%B4%A2%E5%AF%8C%E3%80%81%E8%99%9A%E6%8B%9F%E8%B4%A2%E5%AF%8C%E5%8F%8A%E8%B4%9F%E5%80%BA)

### Statistical Mechanics of Money Distribution
- A Recap
- The Boltzmann-Gibbs distribution of energy
    - 原先社會物理學只專注在財經市場(1990中期)，後來發展出另一個方向是研究社會中金錢、財富與收入的機率分佈
    - 許多經濟學文獻會利用隨機過程去描述個體財富與收入的動態過程，並推導出機率分佈
    - 有人會將此稱為 one-body approach，因為對於個別economic agent，財富與收入的波動是獨立運作的
    - 受到Boltzmann氣體動力論的影響，社會物理學家引入所謂 two-body approach，每個agent會傳遞金錢、相互交易(pairwise economic transactions)
    - 上述方法被社會學家John Angle在1980年大量使用，但直到2005年後才被大家大量關注
    - 2000年共三篇具有極度影響力的文章(Bouchaud and M´ezard; Chakraborti and Chakrabarti; [Dr˘agulescu and Yakovenko](https://arxiv.org/pdf/cond-mat/0001432.pdf))為此領域豎立了里程碑，基本上皆架構於 pairwise money transfer model的概念上
    - 有趣的是，pairwise money transfer model在經濟學上並沒有相應的概念
    - 此一模型刺激了Bak, Nørrelykke, and Shubik (1999)對於金錢動力學的研究
    - 關於機率分佈的研究是直到2006年Miguel Molico才有了數值上的結果(非解析形式)
- The Boltzmann-Gibbs distribution of energy
    - Boltzmann-Gibbs distribution講述，找到具有能量$\epsilon$的物理系統的機率函數為
$$
P(\epsilon)=ce^{-\epsilon/k_bT}\hspace{0.5cm}(1)
$$
    其中T是溫度，$k_b$為Boltzmann常數，c是歸一常數
    - 對於某物理變量x，其期望值可表示成:
$$
<x> = \frac{\sum_{}^{}\mathop{}_{\mkern-5mu i} x_ie^{-\epsilon/k_bT}}{\sum_{}^{}\mathop{}_{\mkern-5mu i} e^{-\epsilon/k_bT}}\hspace{0.5cm}(2)
$$
    summation是針對系統內所有狀態
- Conservation of money
    - 上節推導過程要求的前提是能量守恆
    - Dr˘agulescu and Yakovenko主張，在經濟物理學討論的範疇裡，金錢可視為守恆量，因為所謂economic agent是不被允許**製造**錢(印鈔)
    - 因此，假設agent i 付錢$\Delta m$給agent j，且金錢轉移前，各擁有錢$m_i$與$m_j$；轉移後，各擁有錢$m'_i$與$m'_j$，轉移公式可寫成
$$
m_i\rightarrow m'_i=m_i-\Delta m\hspace{1cm}$$$$
m_j\rightarrow m'_j=m_j+\Delta m\hspace{0.5cm}(3)
$$
    - 上述金錢轉移的假設，可類比為粒子能量轉移，推導後可得公式(1)
    - 這樣的金錢守恆模型也被用在經濟學文獻裡(Kiyotaki and Wright, 1993; Molico, 2006)
    - 這裡強調，<font color="#DC143C">這裡的金錢轉移代表著在經濟市場上對於物品或服務的付出</font>，這邊只記錄<font color="#DC143C">金錢的流動而非相對應得到的物品或服務</font>，其中一個原因為<font color="#DC143C">很多物品使用後會消失，且多數服務並非有形之物</font>，這帶來以下特性:
        - 物品與服務非守恆量
        - 物品與服務難以用同一單位量化
    - 相對的，金錢具有以下特性:
        - 錢有共同單位(至少在同一國家、使用單一貨幣時)
        - 錢在交換前後不會增加或損失(守恆)
    - 另一個要注意的點為，物品的增加不會帶來相應金錢的增加$\rightarrow$我們可以種植蘋果樹帶來蘋果，但市場上的錢不會因此變多
    - <font color="#DC143C">只有中央銀行有能力增加市場上流動的金錢數量</font>(McConnell and Brue, 1996)
    - 我們可以將中央銀行視為外部金錢(能量)來源，而原系統內的金錢(能量)依舊保持守恆，可類比對象如:地球接收太陽(外部)能源
    - 因此，一般我們會先從封閉系統開始分析(i.e.封閉系統內的金錢/能量守恆假設)，在推廣至開放系統(i.e.挹注外部金錢/能量)
    - 一般情況，我們可以假設中央銀行的金錢增減率(單位時間內增減的金錢數量)很小，不會造成惡性通膨或通縮，則系統可視為半靜態統計平衡(quasi-stationary statistical
equilibrium)
    - 此系統可類比成瓦斯上加熱的爐子，只要加熱速度慢，爐子溫度在單位時間內只會緩慢上升
    - 這樣的行為牽扯到複雜的多貨幣匯率議題 (McCauley, 2008)
    - 上述討論了許多延伸，不過一般常見的模型假設有以下:
        - 單一國家，單一貨幣
        - 不允許負債(agent的財產需大於0)
        - 交易金額需小於付款人的財產
        - 若agent財產為0，還是可(藉由付出勞力或服務)獲得金錢
        - agent不能製造金錢(印鈔)
        - agent不需擔心金錢的信用問題(由中央銀行擔保)
    - 後續會討論到銀行、負債與信用問題
    - 宏觀經濟議題如供需法則，不在這篇文章的討論範圍內
    - 雖然實際上市場永遠不會平衡，但*平衡*這一概念在經濟學文獻中卻很常見。在此延伸此一概念至*統計平衡*:在供需的*力*相等時，金錢機率分佈$P(m)$為靜態
    - 此文章的重點在於研究agent之間的金錢機率分布，因此適當的理想化一些宏觀經濟議題有助於尋找模型中的統計平衡
- The Boltzmann-Gibbs distribution of money
    - 藉由上述的金錢守恆假設，Dr˘agulescu和Yakovenko主張金錢機率分布$P(m)$應為靜態的，也就是各別agent擁有的錢會波動，但整體分布是恆定的:
$$
P(m)=ce^{-m/T}\hspace{0.5cm}(4)
$$
其中c為常數，m為錢，$T$為金錢溫度(money temperature)，由normalization conditions
$$
\int_{m=0}^{\infty}P(m)\,dm=1\\
\rightarrow\int_{m=0}^{\infty} ce^{-m/T}\,dm=1\\
\rightarrow\int_{m=0}^{\infty} e^{-m/T}\,dm=1/c\\
\textrm{since}  \int_{}^{} e^{ax}\,dx=\frac{1}{a}e^{ax}\\
\textrm{gives} \int_{x=0}^{\infty} e^{-ax}\,dx=\frac{1}{-a}e^{-ax}\rvert^{x=\infty}_{x=0}=0-\frac{1}{-a}=\frac{1}{a}\\
\textrm{thus} \int_{m=0}^{\infty} e^{-m/T}\,dm=T=1/c\\
\rightarrow c=\frac{1}{T}
$$
$$
\textrm{also}<m>=
\int_{m=0}^{\infty}mP(m)\,dm=\int_{m=0}^{\infty} mce^{-m/T}\,dm\\
=T\int_{m=0}^{\infty} \frac{m}{T}e^{-m/T}\,d(\frac{m}{T})\\
\textrm{set}\hspace{0.3cm} u=\frac{m}{T}\\
\rightarrow=T\int_{u=0}^{\infty} ue^{-u}\,du
=T e^{-u}(-u-1)\rvert^{u=\infty}_{u=0}
=T(0-1\times-1)=T\\
\textrm{thus}\hspace{0.3cm} T=\frac{M}{N}
$$
其中$M$為總金錢數，$N$為總agent數
    - 為了驗證這個理論，Dr˘agulescu和Yakovenko進行了agent-based電腦模擬：
        1. 初始化：所有agent都擁有等量的錢
        2. 隨機選取兩個agent$(i, j)$，並轉移$\Delta m$的錢
        3. 重複步驟2多次
        4. 最後可證實，機率分布$P(m)$為一exponential遞減曲線
    - 若假設$\Delta m = 1$，也就是所有的產品都是1元。電腦模擬顯示，一開始會形成對稱的高斯曲線(對應到物理上的diffusion特性(?))，隨著時間推移，大家都會擠在$m=0$的地方(邊界條件$m\geq0$)，使得分布形成非對稱的exponential曲線，且達到靜態平衡。
    - 邊界條件$m\geq0$其實相當於統計物理上的ground-state energy，若邊界條件不存在，則靜態平衡不存在(?)
    - 又， (Chen and Yakovenko, 2007; Wright, 2007)指出，金錢分布的entropy
$$
\frac{S}{N}=-\sum_{k}^{}P(m_k)\textrm{ln}P(m_k)
$$
        一開始(所有agent都是都擁有等量的錢時)為0，後來在靜態平時會達到最大值
    - 另一個模型假設$\Delta m \in [0, <m>]$，或寫成
$$
\Delta m = \nu (M/N) \textrm{   where  }
\nu \sim U[0, 1]
$$
    呈現不同物品的價錢屬性，而電腦模擬顯示同樣的exponential曲線(動畫可見Chen and Yakovenko (2007))
    - 另一種模型假設交易金錢的上限，為雙方的平均
$$
\Delta m = \nu (m_i+m_j) /2 
$$
模擬出同樣的曲線
    - 雙邊交易模型簡單，卻顯得原始。現代經濟是由大公司主導，因此Dr˘agulescu和Yakovenko假設狀況如下:
        1. 每個時間點，某個agent $i$會被視為一個公司主體
        2. agent $i$會跟agent $j$借錢$K$，並償還利息$hK$
        3. 每個公司會雇用$L$個agent，每個agent付薪水$w$
        4. 公司會製造$Q$個產品，並賣給$Q$個agent，每個賣$p$元
        5. agent $i$會獲利
$$
F=pQ-wL-hK
$$
        6. 其中，供需公式為$p(Q)=v/Q^\eta$，$v, \eta$為參數，$Q$為消費者在價錢$p$時會買的產品數量
        7. 公司的產能公式為傳統的Cobb-Douglas form: $Q(L,K)=L^xK^{1-x}$，$x$為參數
        8. 利潤$F$會針對$K, L$最大化
    加入公司概念的模型依然遵循exponential的分布
    - 在此可見，Boltzmann-Gibbs distribution基本上與假設無關
    - 後人發現，Dr˘agulescu和Yakovenko的概念早在1988被Eleonora Bennati提出(1988, 1993)，因此又被稱為Bennati-Dr˘agulescu-Yakovenko game (Garibaldi et al., 2007; Scalas et al., 2006)
- Models with debt