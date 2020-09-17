---
title: MACD
description:
---

* MACD 与三个量有关系

	* EMA
	* DIFF
	* DEA

* EMA, aka. EXPMA: exponential moving average 指数平均数指标

	MA vs EMA: MA均线因为给计算的每一天都赋予相同权重，不太好使，所以出了EMA, 给越接近当天的收盘价越高的权重
	
	$EMA_t(N)$: 在t时刻N天的权重平均数
	
	* 公式&推导
		
		EMA(N): $EMA_t = \alpha \times Price_t + ( 1 - \alpha) \times EMA_{t - 1}$
		
		* $\alpha$: 平滑指数,可取 $ \frac{2}{N+1}$ 或 $\frac{2}{N}$
		* $Price$: 收盘价
	
		递推公式: $EMA_t = \alpha \times Price_t + \dots + \alpha \times (1-\alpha)^{t-2} \times Price_2 + \alpha \times (1-\alpha)^{t-1} \times EMA_1$
		
		* $EMA_1$: 起始的收盘价
		* $\alpha \in (0,1)$. 随着t的增加, 权重越小,可以忽略

* $DIFF = EMA(12) - EMA(26)$

	更准确写法 $DIFF_t = EMA_t(12) - EMA_t(26)$
	
	= $(\alpha_1 - \alpha_2) \times Price_t + \dots + (\alpha_1 \times (1-\alpha_1)^{t-2} - \alpha_2 \times (1-\alpha_2)^{t-2}) \times Price_2 + (\alpha_1 \times (1-\alpha_1)^{t-1} - \alpha_2 \times (1-\alpha_2)^{t-1}) \times EMA_1$
	
	* 画图

		Let $y = \alpha_1 \times (1-\alpha_1)^{x} - \alpha_2 \times (1-\alpha_2)^{x}$
		
		$\alpha_1 = \frac{2}{12+1} = \frac{2}{13}$ 
		$\alpha_2 = \frac{2}{26+1} = \frac{2}{27}$
		
		![](DIFF1.jpg)
		![](DIFF2.jpg)
		
		From graph: **DIFF把最近8天的收盘价乘以几个权重后相加, 然后减去前8天到100天的收盘价乘以某些权重的和**
		
		* DIFF>0: 最近几天的趋势是涨
		* DIFF<0: 最近几天的趋势是跌

* $DEA$

	$t = \alpha \times DIFF_t + (1 - \alpha ) \times DEA_t - 1$
	
* $MACD = 2 (DIFF-DEA)$

结论：用MACD指标来判断未来趋势，其实隐含着一个前提：股价的变化是有趋势的，是和物体运动一样有动量。但实际上不一定的，所以专业的机构投资人基本不会根据这个指标操作的，最多辅助看看。macd本来就是从期货市场来的，在股票市场是个不实用的指标。


MACD有两种主要作用:一是判断趋势，二是通过背离判断回调或转折。
一. 顺势操作：金叉买入，死叉卖出
就是追涨杀跌，在多头市场时金叉买入，在空头市场时死叉卖出。
二. 逆市操作：在顶背离卖出，在底背离买入
一般情况下，指标都随着股价走。但有些时候，因为某些因素，造成了指标没法和价格形成同步，因此形成了背离。背离简单来说就是价格和指标之间产生了不同的走势。价格创出新高，而指标却在下降；或者是价格下降，而指标却在上升。

## 缠论
MACD的唯一的，正真的作用在于利用其背离判断顶部和底部
周级别准确率可以达到95％以上。