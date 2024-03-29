---
title: MACD
description: 
---

**MACD指标**由2条曲线和1组柱线构成

* DIF线:波动快. 股价短期内的涨跌速度. 2条EMA曲线的差. 默认: EMA(12日)-EMA(26日)
	* DIF在0轴之上 $\Longleftrightarrow$ EMA(12日)在EMA(26日) 之上 
		* 两者差距越大, DIF曲线就越高
		* 短期内的平均价格高于长期平均价格
		* 整个股价处于上涨过程中, 曲线位置越高, 说明股价的上涨速度越快
	* DIF在0轴之下 $\Longleftrightarrow$ EMA(12日)在EMA(26日) 之下 
		* 两者差距越大, DIF曲线就越低
		* 期内的平均价格低于长期平均价格
		* 整个股价处于下跌过程中, 曲线位置越低, 说明股价的下跌速度越快
	
	;![](DIF.png)
	
	DIF突破0轴, 股票短期内的平均股价开始超过长期平均股价的信号
	
	EMA(x) - EMA(y)
	
	* x越大 或 x与y之间差距越大: DIF线波动越平缓, 整个MACD支票的买卖信号准确度会更高, 但信号实效会落后

		准确度与实效性成反比
	
* DEA线: 波动慢. 股价较长时间的涨跌速度. DIF的9日平滑移动平均线

	DIF的辅助判断线
	
	* DIF高于DEA, 说明DIF线的值越来越高. 短期平均股价杜宇长期平均股价持续上涨的信号
	* DIF低于DEA, 说明DIF线的值越来越低短期平均股价杜宇长期平均股价持续下跌的信号

![](MACD指标.png)

**金叉**: DIF线自下向上突破DEA线

**死叉**: DIF线自上向下跌破DEA线


* MACD柱线: (DIF-DEA)*2

	* (DIF-DEA)*2 > 0: 零轴之上
		* 多方力量将股价向上拉升
		* 上涨的速度会加快
		* 下跌的速度会减慢
		* 柱线越长, 推动上涨的力量就越强
	* (DIF-DEA)*2 < 0: 零轴之下
		* 空方力量将股价向下打压
		* 上涨的速度会减慢
		* 下跌的速度会加快
		* 柱线越长, 打压行情下跌的力量就越强
	DIF线: 股票短期内的涨跌速度
	DEA线: 股票较长时间内的涨跌速度
	
	MACD柱: 股价涨跌的加速度, 推动股价涨跌的内在动能强弱
	
* 使用6日, 26日, 9日的原因

	当年每周交易6天
	
	* 买周交易天数6天
	* 26日为1个月
	* 9日是1.5周, 是1/3月

	
## MACD指标基本买卖形态

### 1. DIF线和DEA线金叉

DIF线从下向上突破DEA线

1. 零轴下方金叉

	* DIF线: 短期内股价的涨跌速度. 
		* DIF在零轴下方: 股价短期内处于下跌的行情中
		* 曲线位置越低, 短期内的下跌速度越快
	* DEA: 中长期的涨跌速度. 
		* DEA在零轴下方: 股价中长期内都处于下跌的行情中
		* 曲线位置越低, 中长期内下跌速度越快

	* 零轴下方金叉: 股价短期内的下跌速度已经小于长期下跌速度, i.e., 下跌速度有减缓趋势, 未来股价可能会见底反弹
	* 零轴下方的金叉越接近0轴: 股价的下跌趋势越弱, 未来能获得支撑进入持续上涨行情的可能性越大

1. 零轴上方金叉

	* 零轴上方金叉: 股价短期内的上涨速度已经超过长期上涨速度, i.e., 上涨速度有加速趋势, 未来股价可能会持续上涨. 
	* 看涨买入信号. 
	* 与零轴下方的金叉相比, 零轴上方金叉比零轴下方金叉更强的看涨买入信号
	*  零轴上方的金叉越接近0轴, 股价还处于上涨的初期, 未来有较大的上涨空间, 这样的上涨信号也会更加强势
	
1. 零轴附近金叉: 0轴附近的金叉是最强的看涨买入信号, 强度超过零轴上方和下方远离零轴的金叉

4. 金叉的买入仓位控制

	信号强弱: 零轴下方金叉 <	零轴商贩金叉 <	零轴附近金叉
	
	* 零轴下方金叉: 下仓位试探性地买入
	* 零轴上方很高的位置形成金叉时, 股价已经上涨到了高位, 未来继续上涨的空间有限: 控制仓位, 随时注意股价见顶下跌的风险
	