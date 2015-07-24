#Week 3: Learning sets of rules and logic programs

##Rule Induction

**為什麼不只learn rules就好？**

**rules are popular:**  

*  簡單好理解

*  variable size

*  deterministic

*  discrte & continuous parameters

**單獨rule的形式: 一群tests的交集**  

**rule set: 一群rules的聯集**

**用rule set建decision tree:**    

root的影響不太大，可以隨便挑其中一個條件，當一個條件不合時，就換下一個。

exponential time(ADA的什麼東西也是這樣...), replication problem(同樣的條件不斷重複出現)

**rule induction 比較容易overfitting:**

flexible but might find some sets of rules that just looks good sometimes
