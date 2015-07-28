#Week 3: Learning sets of rules and logic programs

##Rule Induction

**為什麼不只learn rules就好？**

*  slower

*  比較不明瞭

*  overfitting


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

<b>General Prior Estimate</b>: If prior belief p = 0.25, can use any number k

p = (m1 + k)/(m0 + m1 + 4k) -> the larger k is, the stronger our prior belief becomes

**Learning Rules for Multiple Classes**

*  Order rules

*  Weighted vote 

**Learning First-Order Rules:**

using first order logic to represent

<b>FOIL</b>:First-Order-Inductive Learner

*  不是只有是非，有更powerful的表示法(literals, candidate specialization)

Learning rule: P(x1, x2, ..xk) <- L1...Ln (L is literal)

special predicate "Equal(x1, x2)": x1, x2是一樣的

*  Information Gain in FOIL

Fail_Gain(L, R)定義為 t(log<sub>2</sub> p1/(p1+n1) - log<sub>2</sub> p0/(p0+n0))

binding: 會match某些subgraph

R: original rule p0: num of positive bindings of R n0: num of negative bindings of R
L: new rule p1: num of positive bindings of L+R n1: num of negative bindings of L+R
t: R & L+R 交集的positive binding

**Induction(歸納法) as Inverted Deduction(演繹法)**

induction is finding a hypothesis h s.t. 

(∀ <x<sub>i</sub>,f(x<sub>i</sub>)>∈ D) B∧ h∧ x<sub>i</sub> ├ f(x<sub>i</sub>)

more than one inverse deduction(跟積分一樣)

figure out what are relavant

優：background knowledge (B)

缺：無法接受noisy data, Huge hypothesis space: overfitting, 

**Deduction: Resolution Rule**

1. L 和 C1 在一個clause中，¬ L 和 C2 在另一個clause中

2. Form the resolvent C by including all literls from C1 and C2, 除了L和¬ L

  C = (C1 - {L})∪ (C2 - {¬ L})

--> C2 = (C - (C1-{L}))∪ {¬ L}

**First-Order Resolution**

1.  Find a literal L1 from clause C1, literal L2 from clause C2 and substitution θ s.t. L1θ = ¬L2θ

2.  Form the resolvent C by including all literals from C1θ and C2θ, 除了L1θ 和 ¬L2θ

C = (C1 - {L1})θ∪ (C2-{L2})θ

--> C2 = (C-(C1-{L1})θ<sub>1</sub>)θ<sub>2</sub><sup>-1</sup>∪ {L1θ<sub>1</sub>)θ<sub>2</sub><sup>-1</sup>}
    
generalization

**Progol: Reduce combination explosion by generating the most specific acceptable h**

**Questions**

Q1: argument, variable, literal指的是什麼？

Q2: binding不太懂（rule 間會有相關）

