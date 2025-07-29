(ignore heading numbers)
### 3.4 Butterfly Spread Strategy

**Definition**: A strategy that bets **against** movement (opposite of straddle/strangle)

**Long Call Butterfly Construction**:

- Buy 1 call at low strike price (e.g., $55)
- Sell 2 calls at middle strike price (e.g., $60)
- Buy 1 call at high strike price (e.g., $65)
- All options have same expiration date
- Strike prices are equidistant

**Market Expectation**: Price will hover around center strike price ($60) with minimal movement

**Payoff Analysis**:

- If ST < $55: All options worthless, payoff = 0
- If $55 < ST < $60: Only $55 call exercised, payoff = ST - 55
- If $60 < ST < $65: Profit from $55 call offset by losses from $60 calls
- If ST > $65: All options exercised, net payoff = 0

**Key Characteristic**:

- Maximum profit occurs when ST = middle strike price
- Limited profit potential and limited risk
- Profits from low volatility/minimal price movement

## 4. Portfolio Payoff Analysis

### 4.1 General Method for Complex Portfolios

**Systematic Approach**:

1. Identify all strike prices in ascending order
2. For each price range between consecutive strikes:
    - Determine which options are "in the money"
    - Calculate net payoff from active options
3. Plot piecewise linear payoff function

**Example Portfolio**:

- Sell 2 calls (E=$50)
- Buy 2 calls (E=$70)
- Buy 3 calls (E=$90)
- Sell 1 call (E=$110)
- Sell 2 calls (E=$120)

**Payoff by Price Range**:

- ST < $50: Payoff = 0
- $50 < ST < $70: Payoff = -2(ST - 50) = 100 - 2ST
- $70 < ST < $90: Payoff = -40 (constant)
- $90 < ST < $110: Payoff = 3ST - 310
- $110 < ST < $120: Payoff = 2ST - 200
- ST > $120: Payoff = 40 (constant)

## 5. Option Pricing Theory

### 5.1 Present Value of Money

**Continuous Compounding Formula**:

- dM/dt = M × r (where r = interest rate)
- Solution: M(t) = M₀ × e^(rt)

**Present Value Concept**:

- Having M₀ now ≡ Having M₀ × e^(rt) after time t
- Having Mt at time t ≡ Having Mt × e^(-rt) now

### 5.2 Put-Call Parity

**The Fundamental Equation**: **S + P(E,S,T) = C(E,S,T) + E × e^(-r(T-t))**

Where:

- S = Current stock price
- P(E,S,T) = Put option price
- C(E,S,T) = Call option price
- E = Strike price
- r = Risk-free interest rate
- T-t = Time to expiration

**Economic Interpretation**:

- Left side: Stock + Put (synthetic call)
- Right side: Call + Present value of strike price
- These portfolios must have equal value to prevent arbitrage

### 5.3 No-Arbitrage Proof

**If S + P > C + E×e^(-r(T-t))**: (Left side greater)

_Arbitrage Strategy_:

1. Short stock (receive S)
2. Sell put (receive P)
3. Buy call (pay C)
4. Deposit E×e^(-r(T-t)) in bank
5. **Result**: Immediate guaranteed profit with zero risk at expiration

_At Expiration_:

- If ST > E: Exercise call, use stock to cover short position
- If ST < E: Put exercised against you, use received stock to cover short
- Bank deposit grows to exactly E for transactions

**If S + P < C + E×e^(-r(T-t))**: (Right side greater)

_Arbitrage Strategy_:

1. Sell call (receive C)
2. Borrow E×e^(-r(T-t)) from bank
3. Buy stock (pay S)
4. Buy put (pay P)
5. **Result**: Immediate guaranteed profit with zero risk at expiration

**Conclusion**: Both inequalities lead to risk-free profits (arbitrage), which market forces eliminate, proving the equality must hold.

## 6. Advanced Concepts

### 6.1 Arbitrage Theory

**Definition**: Risk-free profit opportunity that requires no initial investment

**Market Efficiency**: Arbitrage opportunities cannot persist in efficient markets due to:

- Rapid exploitation by traders
- Price adjustments that eliminate opportunities
- Competitive forces

### 6.2 Option Pricing Applications

**Put-Call Parity Uses**:

- Determine fair value of one option given the other
- Identify mispriced options in the market
- Create synthetic positions (synthetic call = stock + put)
- Foundation for more complex pricing models

**Advanced Pricing Models**:

- **Black-Scholes-Merton Model**: Sophisticated option pricing
- **Mathematical Finance**: Branch studying quantitative financial instruments
- Consider factors: volatility, time decay, dividend yields

## Key Formulas and Notation

- **Call Option Payoff (Long)**: max(ST - E, 0) - PCE
- **Put Option Payoff (Long)**: max(E - ST, 0) - PPE
- **Short Stock Payoff**: S₀ - ST (where S₀ = initial sale price)
- **Straddle Cost**: PCE + PPE
- **Straddle Payoff**: |ST - E| - (PCE + PPE)
- **Butterfly Spread**: Limited risk, limited reward, profits from low volatility
- **Put-Call Parity**: S + P = C + E×e^(-r(T-t))
- **Present Value**: PV = FV × e^(-rt)

## Important Terms

- **Strike Price (E)**: Predetermined price for option exercise
- **Expiration Date (T)**: Date when option expires
- **Premium**: Price paid for option
- **Exercise**: Using the right provided by option
- **Volatility**: Measure of price movement magnitude
- **Hedge**: Strategy to reduce risk exposure
- **Arbitrage**: Risk-free profit opportunity
- **No-Arbitrage**: Principle that arbitrage opportunities cannot persist
- **Synthetic Position**: Combination of instruments that replicates another instrument