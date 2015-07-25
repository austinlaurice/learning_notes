#Week 3: Learning sets of rules and logic programs

##Rule Induction

**為什麼不只learn rules就好？**

**rules are popular:**  

*  簡單好理解

*  variable size

*  deterministic

*  discrete & continuous parameters

**單獨rule的形式: 一群tests的交集**  

**rule set: 一群rules的聯集**

**用rule set建decision tree:**    

root的影響不太大，可以隨便挑其中一個條件，當一個條件不合時，就換下一個。

exponential time(ADA的什麼東西也是這樣...), replication problem(同樣的條件不斷重複出現)

**rule induction 比較容易overfitting:**

flexible but might find some sets of rules that just looks good sometimes

**choosing the best test:** 

proposed rule covers m0' and m1' examples

gain = m1'((-plgp)-(-p'lgp'))  (old surprise - new surprise, want to reduce our surprise)

但是decision tree會看兩邊(Divide and Conquer)，learning rules只會看一邊(Seperate and Conquer)

**Search Procedure:**

*  RR replacement

*  Backfitting

*  Beam Search: growin k new rules

**Probability Estimates from Small Numbers:**

原本的 p = m1/(m0 + m1) 但如果樣本數少，極不可靠

<b>Laplace Estimate</b>: p = (m1 + 0.5)/(m0 + m1 + 1) 

<b>General Prior Estimate</b>: prior belief p = k

p = (m1 + k)/(m0 + m1 + 4k) -> the larger k is, the stronger our prior belief becomes
























