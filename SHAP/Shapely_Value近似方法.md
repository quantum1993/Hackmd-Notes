# Shapley Value(2)--近似方法
###### tags: `SHAP`
[TOC]
## Shapley Value為何需要近似？
 - 觀察公式本身，需要sum over $S\subseteq F \backslash \{i\}$，一共有$2^{n-1}$項，時間複雜度為$O(2^n)$
  $$
  \phi_i(x)=\sum_{S\subseteq F\backslash\{i\}}^{}\frac{(|F|-|S|-1)!|S|!}{|F|!}[\Delta_{S\cup \{i\}}(x)-\Delta_S(x)] \tag{1}
  $$
  
 - 若再考慮$\Delta (x)$本身的計算量，參考原始$\Delta (x)$的[定義](https://hackmd.io/VyQGMJ1qRCGiT5GmNz4ySg)
  $$
  \Delta_Q(x) = f_Q(x)-f_{\{\}}(x)\tag{2}
  $$
  其中$f_Q=E[f|X_i=x_i, \forall i \in Q]$，已知$Q$的前提下，要sum over剩下集合空間裡$F-Q$的所有點，若假設每個維度有m個點，則時間複雜度也是exponential  $O(m^{|F-Q|})$
 - Overall，整體的計算量十分龐大，故需要近似方法加速計算
## Shapley Value要如何近似？
 - 有人先考慮對$f_Q(x)$近似，使用$Q$的特徵來訓練模型以得到$f_Q(x)$，假設模型訓練成本為$O(n^2)$，則可把原先exponential降為polynomial。此方法的缺點為：
     - Shapley value變得依賴模型
     - 需要訓練資料
 - 另有人考慮對$\phi_i(x)$的近似，概念上，可視所有的組合$2^{n-1}$為母體，並利用抽樣的方法來估計$\phi_i(x)$，假設我們抽了$k$次，$k$足夠大時，根據中央極限定理，則可逼近母體$\phi_i(x)$
     - 符號定義：
         - $A_Q=\prod_{l\in Q}^{}A_l$，e.g. $A_{\{1,3\}}=A_1\times A_3$
         - For $p\in A_Q$，意思是$p$為$A_Q$空間中的某一點，若$Q$是多維的，則$p$是多維的座標點
     - 改寫$f_Q(x)$:
      $$
       \begin{align*}
       f_Q&=E[f|X_i=x_i, \forall i \in Q]\\
       &=\frac{1}{|A_{F-Q}|}\sum_{p\in A_{F-Q}}^{}f(\tau(p,q;Q)) \tag{3}\\
       &\textrm{where } \tau(p,q;Q)=(z_1,z_2,...,z_n)\\
       &z_i=\left\{
                \begin{array}{ll}
                  q_i ; i\in Q\\
                  p_i ; i\notin Q
                \end{array}
              \right.\\
       &p=\{p_i;i\notin Q\}, q=\{q_i;i\in Q\}
       \end{align*}
      $$
     - 依照前一章節的"快速推導$\gamma(S)$"段落，式(1)可改寫為，:
## Appendix
- [抽樣與蒙地卡羅(二)：蒙地卡羅方法與重要性抽樣](https://medium.com/%E6%95%B8%E5%AD%B8-%E4%BA%BA%E5%B7%A5%E6%99%BA%E6%85%A7%E8%88%87%E8%9F%92%E8%9B%87/%E6%8A%BD%E6%A8%A3%E8%88%87%E8%92%99%E5%9C%B0%E5%8D%A1%E7%BE%85-%E4%BA%8C-%E8%92%99%E5%9C%B0%E5%8D%A1%E7%BE%85%E6%96%B9%E6%B3%95%E8%88%87%E9%87%8D%E8%A6%81%E6%80%A7%E6%8A%BD%E6%A8%A3-7558764151b9)
- [重要性采样（Importance Sampling）](https://zhuanlan.zhihu.com/p/41217212)
- [A General Method for Visualizing and Explaining Black-Box Regression Models](http://file.biolab.si/files/ml1/2011-Strumbelj-Kononenko-ICANNGA.pdf)
- [Importance Sampling](https://www.youtube.com/watch?v=V8f8ueBc9sY&ab_channel=BenLambert)