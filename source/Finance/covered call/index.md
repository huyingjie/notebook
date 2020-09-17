---
title: covered call
description:
---


## bear and bull markets

type|bear | bull
---|---|---
covered call  | deeper in-the-money  |  out-of-the-money
cash-secured puts  | deeper out-of-the-money   | slightly out-of-mearket, at-the-money, slightly in-the-money

## Greek

* **Delta**: the expected amount a preimum wil change for every $1 change in the price of a stock, assuming all other price-related factors remin constant

* **Gamma**: the expected change in Delta for a short-term, $1 change in the price of the underlying security.

  * the same for both puts and calls
  - always positive
  - can be thought as the "Delta of the Delta"
  - Gamma has greatest impact and increases for at-the-money strikes, close to xpiration. This is where Deltas can change the fastest as options move in and out-of-the money
* **Theta**: the amount the price of calls and puts will decrease (at least in theory) for a one-calendar day (as opposed to trading day) change in the time to expiration assuming that all other pricing factors remain constant
  - Calls and puts have negative Theta
  - Put buyers are counting on gains in Delta to offset the losses in Theta
  - Thetas are highest for at-the-money strikes and options closest to expireation
* **Vega**: the expected change in the value of an option with a 1% change (whether up or down) in implied volatility assuming all other priciing factors remain constant
  - Calls and puts have positive Vega
  - A change in implied volatility, Vega does not require an associated change in stock prices
  - Vega has its greatest dollar impact on at-the-money strikes and its greatest percentage impact (amount of change divided by the original premium amount) on out-of-the money strikes
  - The greater the time to expiration, the higher the Vega
  - Higher Vega are associated with higher ooption premiums
  - ther greater the implied volatility => the higher the risk
    - e.g. prior to news announcements

High Vegas | Low Vegas|
---|---
HIgher personal risk tolenrance  | Low personal risk tolenrance
Bullish market outlook  | Bearish or volatile market outlook
Strong and confirming chart technicals  | Chart technicals mixed

* **Rho**: the expected change in the price of an option when there is a 1% change in the risk-free interest rate (usually associated with Treasuries) assuming all other pricing factors remain constant

  * Rho is larger in-the-market
  * Long calls and short puts have positive Rhos
  * Short calls and long puts have negative Rhos

put position | Delta|Gamma|Theta
---|---|---|---
at-the-money  |  around -0.5 | the highest Gammas|highest
in-the-money  |  between -0.5 and -1 | move deeper: increase
out-of-the-money  |  between -0.5 and 0 | move deeper: increase
deep in-the-money  |  approach -1 | much lss
deep out-of-the-money  |  approach 0 | much less
near expiration  |  ||highest
high volatility stocks  |   |   |  highest

## How much to earn

* Bullish: 2-4% per month
* Bearish: 1-2% per month
## How to measure option liquidity?

* **Daily Volume (Vol)**: the number of times a particular options contract was traded on a specific day

  Each day this figure is re-set to zero and historical statistics are difficult to access

* high liquid if Vol is big
* **Open Interest (OI)**: the number of outstanding options of that type which currently have not been closed out or exercised.
  - Cumulative statistics
  - an accurate idea of invester interest in that particular contract

## 20%/10% cash-secured puts guideline

In the first 2 weeks of a 4-week contract

In the first 3 weeks of a 5-week contract

buy back the put option when its value has declined to 20% or less of its oritinal sale price

In the 3rd week of a 4-week contract

In the 4th week of a 5-week contract

buyback the put option when its value has declined to 10% or less of the original put premium

## 3% cash-secured puts guideline

buy back the put option when the underlying security price falls below the strike sold by more than 3%
## corporation actions that effect options

* earning reports
* mergers
* takeovers
* spinoffs
* special 1-time cash dividends
# Covered Call
Covered calls work well in sideways, slightly down, or slightly up markets. Not optimal in strong bull or bear markets.

Market Type|Best strategy|Good strategy
---|---|---
Up (bull)|Buy and hold|OTM covered calls
Sideways  |ATM covered calls   | ITM or OTM covered calls
Down(bear)  |Cash   |ITM covered calls

![](covered call risk and rewards.png)

## Pros and cons

### pros

1. Receive cash the day you sell the call options
2. Create additional yield on stocks and ETFs you already own
3. Lower your break even point
  1. More consertive than the Buy and Hold strategy
4. Lower account volatility
  1.First part of any drop in stock price is covered by call premium

### cons

1. Put a cap on earning
2. Lose money if stock drops below net debit

  net debit = stock cost - call premium received

## Two wasy to end up with more monetary
### 1. Lose less

  1. diversity


### 2. Make more

a reasonable minimum goal is 1%/month

#### 1. non-dividend stocks into payers

* sell out of the money calls on every stock owned
* set strike price > 10% higher than current price
* set expiration date far enough away so premium meaningful

#### 2. double dividends

* take any dividend paying stock and generate the same or more income from selling calls
* monthly premium goal: Divide annual dividend by 12
* sell OTM calls to generate that much income

#### 3. target yield

Example: want to earn 1%/month (12%/year) with consavertive investments

1. Find deep in the money covered calls with no earnings releases before optin expiration
2. Remove thinly traded stocks, biotech, other risky situations

### 4. dividend capture

1. buy stock before ex-div date
2. sell calls that expire after ex-div date: get the call premium plus the dividend

early exercise possible if time premium small before ex-div date

### 5. Time premium capture

1. buy stocks
2. sell ITM or deep ITM calls

* Only focused on time premium capture, not capital gains
* Lots of transactions(no tax issues if in an IRA)
* Many people do this with margin (Reg T or Portfollio Margin)

# Cash Secured Put

stock price ↑ put price ↓
stock price ↓ put price ↑

Pros|Cons|
---|---
Generate a significant monthly cash flow  | Require cash to secure
Purchase a stock at a discount  |  Maximum gain is limited to the put premium
Generate a profit when the stock price remains stagnant  |  Capital risk if the stock price drops below the breakeven (strike price - premium)
Short holding periods are appropriate  |  Opportunity risk (could miss a runningup in share price)
Risk is reduced due to downside protection  | No or limited tax benefits
Extremely liquid allowing for position management via exit strategy execution  | Assignment risk

## monthly options

1. generate the highest annualized returns
2. make avoiding quarterly earnings reports much easier
3. based current monthly obligation on up-to-date screening information rather than information used months ago had a long-term position been initiated

## weekly options

Pros|Cons|
---|---
Annualized returns may be higher  |  The pool of stocks with weekly options is much smaller than those with monthly options
Can avoid exposure over weekends  | Management is much more time consuming as "rolling" possibilities come up every week
Can generate greater premium as earnings report dates are approached and trade up to the week before earnings|  Less time for exit strategy execution
  | Quadruple the number and amount of commissions
  | Lower option liquidity
  | Wider bid-ask spreads

# Which strike to use, ATM, OTM, ITM?

* return goal (How much do you want to make?)
* risk tolerance (Can you handle a loss? How big of a loss?)
* opinion of where the underlying stock will be at expireation
* taxes, if trading in a taxable account (Do you want to be called?)
* transaction costs (Frequent trading?)

## Which stock to pick?

remove risk where possible:

* High P/E and/or momentum stocks (volatile)
* thinly traded (wide bid ask spreads)
* tiny market cap (volatile)
* tiny option premiums (unprofitable)
* leveraged ETFs (meant for day trading)
* Earnings or FDA announcement before expireation (volatile)


example

1. remove leverage ETFs
2. stock price > $5
3. P/E ratio < 20
4. Epiration date = Feb 18
5. No earnings before expireationMarket cap > $500M
6. Time premium > 20 cents
7. annual return if flat > 12%
8. in the money 5% or more
9. open interest > 2000
10. no healthcare

## Action

1. Dont't invest just prior to earnings
2. Health sector: FDA events

  * https://www.biopharmcatalyst.com/calendars/fda-calendar

# strategy
## Put-Call-Put (PCP) strategy

1. sell an out-of-the-money cash-secured put on a high quality stock or ETF.
2. If unexercised, the cash generated from the sale of the put plus the cash used to secure the original put are used to secure the sale of another put
3. If exercised and the shares purchased at a discount, write a covered call option on the underlying shares

## Poor Man's Covered Calls

Pros|Cons|
---|---
Less capital required  |  Long-term commitment
Higher return on investment  |Cannot calculate maximum profit or breakeven
Less margin needed  | LEAP's have wider spreads
Less capital at risk  |Fewer stocks have LEAP's
theta decay is smaller for LEAP's  |  Must deal with earnings report
Lower time premium paid for LEAP's  | Wild bid-ask for LEAP's
Low volatility environment is best  | blue chip stocks generate lower premiums

 * blue chip stocks that I am happy to own for the long term
   - BA
 * ETF: ETF’s have no stock specific risk and they aren’t subject to earnings announcements.
   - IYR
   - EEM
   - SPY
 * reverse ETFs
   - PSQ: short QQQ (Nasdaq-100)
   - DOG: short Dow 30(DJIA)
   - SH: short S&Q(S&P 500)
   - RWM: short Russel 2000 (Russell 2000)

 Difference between the 2 strikes + premium generated from the short call > cost of LEAPS

* LEAP
   * Delta 0.70 to 0.80 for the LEAP
   * always check how much time premium is embedded in those strikes.
   * The deeper in-the-money the LEAP call is, the less time premium it is likely to have. The less time premium it has, the more it will behave like the underlying stock.

* short call
  * slightly out-of-the-money so that there is still some potential for capital appreciation in the trade.
  * But, it also depends on the underlying stock.
  * If I think the stock is going to be flat, I might consider an at-the-money call to increase the income portion of the position and forego any potential upside from the stock.
  * When selling the call, investors should aim to make sure the time premium in the short call is greater than the time premium in the LEAP. Usually this is not difficult.


#leverage

安全杠杆的理解，要同时具体三个条件

1. 期限要长
2. 没有催你还钱
3. 利率要够低。

# Preferred stocks

tax: certain types of preferred stocks can qualify for Qualified Dividend Income (QDI)

types

1. convertible: investors can exchange fix-rate preferred stocks for the issuer's commmon stocks at a preset price and sahre swap formula
2. floating rate: The dividend rate will vary according to percentage changes in an interest rate benchmark such as LIBOR, Bank Prime Rate, etc.
3. noncumulative: often issued by big banks. Don't accrue overdue dividends but pay a higher dividend than fixed rate preferreds.
4. U.S.Paid: Some foreign preferreds are issued and pay dividends in U.S. dollars to reduce currency risk for American investors.
5. Trust and 3rd Party trust: A company can place its bonds into a trust structure, and the trust can then issue preferred stocks. The hybrid securities are offered by major investment firms and go by abbreviations, such as: PINES, SATURNS, QUIBS, QUICS, QUIDS, QUIPS, TRUPS, TOPRS, etc.

## Pros

1. Margin used

    Many preferreds are gmarginable securities that can be used as collateral for brokerage house loans.

    No need committing new capital

    If margin rates are low, then small amounts of margin can be used to buy new bond or preferred-stock investments at opportune prices

    The recently borrowed funds used to buy new investments will be paid back when older bond investments mature and are cashed in.
  2. Bond substitues
  3. No accrued interest
  4. another way to own Real Estate

      Real estate investment trusts (REITs) regularly issue preferred stocks

    5. global opportunities: Many foreign companies also issue preferreds that trade in the U.S. and abroad.

## cons

* limited mutual fund availability
* few peferred-stock indices

  Winans International Preferred Stock Index (WIPSI)

  S&P Preferred Stock Index

* No listed stock options

## tips

* Patience is required. Many preferred stocks don't trade every day. So you must be patient to buy or sell them at a reasonable prices.

* Order type:

  * Limit orders to buy
  * Market and stop-loss ordeers can be a horrible way to buy or sell
* Ex-dividend date
* Much Brokerage House Information (montly brokerage house documents, trade confirmations, and 1099 forms) is inaccurate or useless

**Biggest risk: inflation.**


The higher interest, the lower preferred stocks.

the worst time in history: -28%

Change in interest rates relative to the supply and demand of an investment are of equal, if not more, importance than overall financial conditions in evaluting income investments
