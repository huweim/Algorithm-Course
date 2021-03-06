NP问题关乎计算复杂性理论

+ NP 千万不要理解为 non-polynomial，而是 non-deterministic. 
+ 严谨点的定义为：在非确定性图灵机上可以被多项式时间内求解的决策问题即为NP问题
+ 简化后的定义为：当给出决策问题的答案的时候 可以很容易（多项式时间内）验证该解是正确的，那么这类决策问题就是NP的。

##### case

+ NP问题正面例子1：例如数独游戏 我给你一个数独游戏的解，你可以很容易的验证（多项式时间内）这个解正确不正确，那么就可以说明数独游戏就是属于NP问题。

+ NP问题正面例子2：决策问题为 是否存在 $x\in R^n_+$ 使得 $c^Tx \geq k$  成立。那么我给你一个 $x$，你能不能在很容易（多项式时间内）验证这个决策问题是成立的。

  + 答案当然是能了，我只需要做一个向量乘法然后再比较一下就能做出判断了，而向量乘法是多项式时间可以被计算出来的。由此可知该问题为NP问题。

+ NP问题反面例子：例如下围棋 我告诉你当前这步棋是最好的，你就很难验证我的说法是否正确，那么这类问题就不属于NP问题。

  + 可以想象一下如果给我们一步棋 我们能判断是最好的话 我们就已经成为围棋上帝了，那么围棋不复存在了 因为可以很容易找到必胜之法了。
+ 虽然阿尔法狗已经轻松击败人类棋手了，但是离围棋上帝还差很多。
  
  

### Difference of NP and P

##### I. Key

+ P问题的核心在于 这类问题是在多项式时间内可以找到该问题的解的
+ NP问题核心是 给我一个问题的解，我能在多项式时间内判断这个解是不是正确的。
+ 从数学上来说，$P \subseteq NP$