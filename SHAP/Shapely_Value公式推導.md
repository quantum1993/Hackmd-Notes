# Shapley Value 公式推導
###### tags: `SHAP`
[TOC]

## Ref Papers
 - [An Efficient Explanation of Individual Classifications using Game Theory (2010)](https://www.jmlr.org/papers/volume11/strumbelj10a/strumbelj10a.pdf)
 - [A General Method for Visualizing and Explaining Black-Box Regression Models (2011)](http://file.biolab.si/files/ml1/2011-Strumbelj-Kononenko-ICANNGA.pdf)
 - [Explaining prediction models and individual predictions with feature contributions(2013)](https://www.semanticscholar.org/paper/Explaining-prediction-models-and-individual-with-%C5%A0trumbelj-Kononenko/8fd17bf36bc22477bb2237c2be6e3212b753969d?year%5B0%5D=2015&year%5B1%5D=2020&sort=relevance&page=2)
 - http://www.sef.hku.hk/~schiu/6036/shapleyproof.pdf
 - http://www.math.ucsd.edu/~fan/152/fergusonIV.pdf
## Shapley Value公式推導
- 符號說明
    - $n$: 特徵數量
    - $F$: 所有特徵的集合，$F=\{1, 2, ..., n\}$
    - $A$: 特徵空間，以笛卡爾座標表示，$A=A_F=A_1\times A_2 \times ......\times A_n$，其中每個$A_i$是由有限個特徵值組合成的集合 (此定義限縮特徵空間為離散的，但後續會證明，後面近似方法可同時應用在連續與離散的特徵空間)
    - $A_S$: 子特徵空間，$A_S=A'_1\times A'_2 \times ......\times A'_n$，其中如果$i\in S$，則$A'_i=A_i$，否則$A'_i=\{\epsilon\}$。因此，給予子集合$S\subset F$，$A_S$為一子特徵空間，非$S$內的特徵將被忽略。子特徵空間裡的元素，都有一個或多個特徵被標註為$\{\epsilon\}$
    - 對於分類模型，$f:A\rightarrow [0, 1]^{|C|}$，$C$為有限的標籤集合
    - 對於迴歸模型，$f:A\rightarrow R$
    - $Q$: 我們感興趣的集合，$Q\subseteq F$
- 推導
    - 定義$f_Q$為，已知subset $Q$的前提下(conditional)，$f$的期望值:
$$
f_Q=E[f|X_i=x_i, \forall i \in Q]\hspace{1.2cm} (1)
$$
For empty set, it reduces to $f_{\{\}}(x)=E[f]$
[註]關於條件期望概念可參考[此資料](http://www.math.ncu.edu.tw/~yu/ps99/boards/lec43_ps_99.pdf)
    - Influence of a certain subset of features可定義為:
 $$
 \Delta_Q(x) = f_Q(x)-f_{\{\}}(x) \hspace{1.2cm} (2)
 $$
 可將此公式想成，當觀測到一部分特徵$x$時，預測值的改變。有$n$個特徵，即有$2^n$種子集合，這裡的工作即是要從$2^n$種集合中，找出$n$個特徵的貢獻
 註：$\Delta_{\{\}}(x) = f_Q(x)-f_{\{\}}(x)$
  - 假設，contribution of a certain subset $f_Q$由所有$Q$的子集合的交互作用相加而成
 $$
 \Delta_Q(x) = \sum_{W\subseteq Q}^{} I_W(x)\hspace{1.2cm} (3)
 $$
 註：since $\Delta_{\{\}}(x)=0$, $I_{\{\}}(x)=0$
  - 式(3)可推導出，$Q$有參與的交互作用$I_Q$
 $$
 I_Q(x) = \Delta_Q(x) - \sum_{W\subset Q}^{} I_W(x)
 \hspace{1.2cm} (4)
 $$
  - 再假設，所有交互作用的影響會平分給參與的特徵，例如特徵$1,2$會平分$I_{\{1, 2\}}$的影響
  - 則我們將這些交互作用平分後，蒐集各別特徵被分到的貢獻，相加後可得每個特徵的貢獻
 $$
 \phi_i(x) = \sum_{W\subseteq F\backslash\{i\}}^{} \frac{I_{W\cup\{i\}}(x)}{|W\cup\{i\}|}\hspace{1.2cm} (5)
 $$
  - 式(4)為recursive的(詳細可見下一章節範例)
   交互作用可全數轉換為$\Delta$的函數，使用non-recursive的方式可寫成(可用數學歸納法證明):
  $$
  I_Q(x)=\sum_{W\subseteq Q}^{}(-1)^{|Q|-|W|}\Delta_W(x)\hspace{1.2cm}(6)
  $$
  - 將式(5)(6)結合，可寫成:
  $$
  \phi_i(x)=\sum_{W\subseteq F\backslash \{i\}}^{}\sum_{G\subseteq (W\cup \{i\})}^{}\frac{(-1)^{|W\cup {\{i\}}|-|G|}}{|W\cup\{i\}|}\Delta_G(x)\hspace{1.2cm} (7)
  $$
  - 其中$G\subseteq W\cup \{i\}$，$G$的內容可分為$S$與$S\cup \{i\}$，且$S\subseteq W$，因此式(7)可寫成
  $$
  \begin{align*}
  \phi_i(x)&=\sum_{W\subseteq F\backslash \{i\}}^{}\sum_{S\subseteq W}^{}[(-1)^{|W\cup \{i\}|-|S\cup \{i\}|}\frac{1}{|W\cup \{i\}|}\Delta_{S\cup \{i\}}(x)+(-1)^{|W\cup \{i\}|-|S|}\frac{1}{|W\cup \{i\}|}\Delta_S(x)]\\
  &=\sum_{W\subseteq F\backslash \{i\}}^{}\sum_{S\subseteq W}^{}\frac{1}{|W\cup \{i\}|}(-1)^{|W\cup \{i\}|-|S\cup \{i\}|}[\Delta_{S\cup \{i\}}(x)-\Delta_S(x)]\tag{8}
  \end{align*}
  $$
  - 先撇除式(8)右側的兩個$\Delta(x)$，現在要來處理左邊的兩個summation。這邊最重要的任務就是把summation下的$S\subseteq W$想辦法變成$S\subseteq F\backslash\{i\}$，而變化的過程中會多出一個係數:
  $$
  \sum_{W\subseteq F\backslash \{i\}}^{}\sum_{S\subseteq W}^{}=\sum_{S\subseteq F\backslash\{i\}}^{} \sum_{w=s}^{n} \binom{n-s-1}{w-s} \tag{8.5}
  $$
  其中$s=|S|, w=|W|$
  - 因此我們可以把式(8)改寫成
  $$
  \begin{align*}
  \phi_i(x)&=\sum_{S\subseteq F\backslash\{i\}}^{} \sum_{w=s}^{n} \binom{n-s-1}{w-s} \frac{1}{w+1}(-1)^{(w+1)-(s+1)}[\Delta_{S\cup \{i\}}(x)-\Delta_S(x)]\\
  &=\sum_{S\subseteq F\backslash\{i\}}^{} \sum_{w=s}^{n} \binom{n-s-1}{w-s} \frac{1}{w+1}(-1)^{w-s}[\Delta_{S\cup \{i\}}(x)-\Delta_S(x)]\\
  & \equiv \sum_{S\subseteq F\backslash\{i\}}^{} \gamma(s)[\Delta_{S\cup \{i\}}(x)-\Delta_S(x)]
  \end{align*}
  $$
  - 進一步處理$\gamma(s)$
  $$
  \begin{align*}
  \gamma(s)&=\sum_{w=s}^{n} \binom{n-s-1}{w-s}(-1)^{w-s}\frac{1}{w+1}\\
  &=\sum_{w=s}^{n} \binom{n-s-1}{w-s}(-1)^{w-s}\int_{0}^{1}x^{(w+1)-1} \,dx\tag{9}\\
  &=\int_{0}^{1}\sum_{w=s}^{n} \binom{n-s-1}{w-s}(-1)^{w-s} x^w \,dx\\
  &=\int_{0}^{1}x^s\sum_{w=s}^{n} \binom{n-s-1}{w-s}(-1)^{w-s} x^{w-s} \,dx\tag{10}\\
  &=\int_{0}^{1}x^s\sum_{w=s}^{n} \binom{n-s-1}{w-s}(-x)^{w-s} \,dx\tag{11}\\
  &=\int_{0}^{1}x^s(1-x)^{n-s-1} \,dx\tag{12}\\
  &=\int_{0}^{1}x^s(1-x)^{n-s-1} \,dx \tag{13}\\
  &=B(s+1, n-s) \tag{14}\\
  &=\frac{(n-s-1)!s!}{n!}\tag{15}\\
  &=\frac{(|F|-|S|-1)!|S|!}{|F|!}
  \end{align*}
  $$
  - 因此:
  $$
  \phi_i(x)=\sum_{S\subseteq F\backslash\{i\}}^{}\frac{(|F|-|S|-1)!|S|!}{|F|!}[\Delta_{S\cup \{i\}}(x)-\Delta_S(x)]
  $$
## 如何理解公式的細節?
- 式(3): 如果$Q=\{1,2\}$，則$\Delta_{\{1,2\}}(x)=I_{\{1\}}(x)+I_{\{2\}}(x)+I_{\{1,2\}}(x)$
- 式(4): 例如$I_{\{1,2\}}(x)=\Delta_{\{1, 2\}}(x)-I_{\{1\}}(x)-I_{\{2\}}(x)$
- 式(4)為recursive的，例如：
 $$
  \begin{align*}
  I_{\{1,2,3\}}(x)&=\Delta_{\{1,2,3\}}(x)-(I_{\{1,2\}}(x)+I_{\{1,3\}}(x)+I_{\{2,3\}}(x)\\&+I_{\{1\}}(x)+I_{\{2\}}(x)+I_{\{3\}}(x))\\
  \textrm{where } I_{\{1,2\}}(x)&=\Delta_{\{1, 2\}}(x)-I_{\{1\}}(x)-I_{\{2\}}(x)\\
  \textrm{and } I_{\{1,3\}}(x)&=\Delta_{\{1, 3\}}(x)-I_{\{1\}}(x)-I_{\{3\}}(x)\\
  \textrm{and } I_{\{2,3\}}(x)&=\Delta_{\{2, 3\}}(x)-I_{\{2\}}(x)-I_{\{3\}}(x)\\
  \textrm{also } I_{\{1\}}(x)&=\Delta_{\{1\}}(x)-I_{\{\}}(x)=\Delta_{\{1\}}(x) \textrm{ and so on}\\
  \rightarrow I_{\{1,2,3\}}(x)&=\Delta_{\{1,2,3\}}(x)-\Delta_{\{1,2\}}(x)+\Delta_{\{1\}}(x)+\Delta_{\{2\}}(x)\\&-\Delta_{\{1,3\}}(x)+\Delta_{\{1\}}(x)+\Delta_{\{3\}}(x)\\&-\Delta_{\{2,3\}}(x)+\Delta_{\{2\}}(x)+\Delta_{\{3\}}(x)\\&-\Delta_{\{1\}}(x)-\Delta_{\{2\}}(x)-\Delta_{\{3\}}(x)\\&=\Delta_{\{1,2,3\}}(x)-\Delta_{\{1,2\}}(x)-\Delta_{\{1,3\}}(x)-\Delta_{\{2,3\}}(x)\\&+\Delta_{\{1\}}(x)+\Delta_{\{2\}}(x)+\Delta_{\{3\}}
  \end{align*}
 $$
- 式(5):  i.e. $\phi_1(x)=I_1(x)+\frac{1}{2}I_{\{1,2\}}(x)$ and $\phi_2(x)=I_2(x)+\frac{1}{2}I_{\{1,2\}}(x)$
- 式(7): 假設$F=\{1,2,3\}$，$i$選定為$1$，$W$則可能為$\{2,3\}， \{2\}， \{3\}， \{\}$
    - For $W=\{2,3\}$，$\frac{1}{|W\cup \{i\}|}=\frac{1}{3}$，$G$可能為$\{1,2,3\}，\{1,2\}，\{2,3\}，\{1,3\}，\{1\}，\{2\}， \{3\}， \{\}$，進一步考慮$S$

        | $S\cup\{i\}$ | $S\cup\{i\}$係數 | $S$ |$S$係數 |
        | :----: | :----: | :----: |:----:|
        | $\{1,2,3\}$ | 1     | $\{2,3\}$     | -1|
        | $\{1,2\}$ | -1     | $\{2\}$     | 1|
        | $\{1,3\}$ | -1     | $\{3\}$     | 1|
        | $\{1\}$ | 1     | $\{\}$     | -1|
        這即是式(8)的由來
- 式(8.5)，難以直接證明，可用舉例的方式了解
    | $w$ |$W$ | $S=\{\}$|$S=\{1\}$|$S=\{2\}$|$S=\{3\}$|$S=\{1,2\}$|$S=\{1,3\}$|$S=\{2,3\}$|$S=\{1,2,3\}$|
    | :----: | :----: |:----: |:----:|:----:|:----:|:----:|:----:|:----:|:----:|
    | 0 | $\{\}$| V     ||||
    | 1 | $\{1\}$| V     |V|||
    | 1 | $\{2\}$| V     ||V||
    | 1 | $\{3\}$| V     |||V|
    | 2 | $\{1,2\}$| V     |V|V||V||
    | 2 | $\{1,3\}$| V     |V||V||V|
    | 2 | $\{2,3\}$| V     ||V|V|||V|
    | 3 | $\{1,2,3\}$| V     |V|V|V|V|V|V|V|
    對於不同的$S$，勾勾的數量即為$\sum_{w=s}^{n} \binom{n-s-1}{w-s}$
    
- 
重點：探討每個玩家(特徵)的貢獻
細節：假設每個玩家(特徵)已知或未知
定義：對於某筆資料$x$，已知玩家集合為$Q$，條件預測值$f$即為$f_Q(x)$，i.e.已知玩家集合Q，對於預測值y的期望為$f_Q(x)$
期望值--蒙地卡羅--重要性抽樣

# Appendix
- [抽樣與蒙地卡羅(二)：蒙地卡羅方法與重要性抽樣](https://medium.com/%E6%95%B8%E5%AD%B8-%E4%BA%BA%E5%B7%A5%E6%99%BA%E6%85%A7%E8%88%87%E8%9F%92%E8%9B%87/%E6%8A%BD%E6%A8%A3%E8%88%87%E8%92%99%E5%9C%B0%E5%8D%A1%E7%BE%85-%E4%BA%8C-%E8%92%99%E5%9C%B0%E5%8D%A1%E7%BE%85%E6%96%B9%E6%B3%95%E8%88%87%E9%87%8D%E8%A6%81%E6%80%A7%E6%8A%BD%E6%A8%A3-7558764151b9)
- [重要性采样（Importance Sampling）](https://zhuanlan.zhihu.com/p/41217212)
- [A General Method for Visualizing and Explaining Black-Box Regression Models](http://file.biolab.si/files/ml1/2011-Strumbelj-Kononenko-ICANNGA.pdf)
- [Importance Sampling](https://www.youtube.com/watch?v=V8f8ueBc9sY&ab_channel=BenLambert)