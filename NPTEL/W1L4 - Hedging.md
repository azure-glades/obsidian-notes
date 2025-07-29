# AI for Economics: Hedging and Uncertainty in Financial Markets

## 1. Options Trading Fundamentals

### 1.1 Call Options Review

**Long Call Option (Buying)**

- **Definition**: Right to buy an asset at strike price E on expiration date
- **Payoff**:
    - If ST > E: Profit = ST - E - PCE (where PCE = call option price)
    - If ST ≤ E: Loss = -PCE
- **Strategy**: Bullish - want asset price to increase

**Short Call Option (Selling)**

- **Definition**: Obligation to sell asset at strike price E if buyer exercises
- **Payoff**:
    - If ST > E: Loss = E - ST + PCE
    - If ST ≤ E: Profit = PCE
- **Risk**: Unlimited losses as asset price rises above strike price

### 1.2 Put Options

**Put Option Definition**

- **Notation**: P(E,S,T) where:
    - E = Strike price
    - S = Underlying asset
    - T = Expiration date
- **Purpose**: Insurance against price decline - right to sell at guaranteed price

**Long Put Option (Buying)**

- **Definition**: Right to sell asset at strike price E on expiration date
- **Payoff**:
    - If ST < E: Profit = E - ST - PPE (where PPE = put option price)
    - If ST ≥ E: Loss = -PPE
- **Strategy**: Bearish - profit when asset price falls

**Short Put Option (Selling)**

- **Definition**: Obligation to buy asset at strike price E if buyer exercises
- **Payoff**:
    - If ST < E: Loss = ST - E + PPE
    - If ST ≥ E: Profit = PPE
- **Risk**: Losses increase as asset price falls below strike price

## 2. Short Selling

### 2.1 Concept and Mechanism

**Definition**: Selling an asset without actually owning it

**Process**:

1. Borrow asset from broker and sell immediately
2. Receive cash from sale
3. Must eventually buy back asset to return to broker
4. Profit if asset price decreases; loss if it increases

**Example**: TCS Stock Short Sale

- Short TCS at ₹100
- If price drops to ₹90: Profit = ₹10
- If price rises to ₹110: Loss = ₹10

**Payoff Characteristics**:

- Downward-sloping payoff curve
- Profit when asset price falls below initial sale price
- Unlimited potential losses as price rises

## 3. Advanced Trading Strategies

### 3.1 Hedged Short Position

**Strategy**: Short stock + Buy call option

- **Purpose**: Limit losses from short position
- **Mechanism**: Call option caps maximum loss at strike price E
- **Benefit**: Protection against unlimited losses while maintaining profit potential

### 3.2 Straddle Strategy

**Definition**: Simultaneous purchase of call and put options with same strike price and expiration date

**Market Scenario**: Amazon vs. Future Group court case

- Uncertain outcome but expecting significant price movement
- Don't know direction but confident in volatility

**Construction**:

- Buy 1 call option (strike price E)
- Buy 1 put option (strike price E)
- Same expiration date for both

**Payoff Analysis**:

- If ST > E: Exercise call option, profit = ST - E
- If ST < E: Exercise put option, profit = E - ST
- **Key Insight**: Profit increases with deviation from strike price E

**Cost Consideration**:

- Total cost = PCE + PPE
- Need price movement > (PCE + PPE) to be profitable

**Real Example**:

- Stock trading at ₹15
- Call option (E=15): ₹2
- Put option (E=15): ₹1
- Total cost per straddle: ₹3
- Need price to move above ₹18 or below ₹12 to profit

### 3.3 Strangle Strategy

**Definition**: Buy call and put options with different strike prices

**Construction**:

- Buy call option with higher strike price
- Buy put option with lower strike price
- Creates a "plateau" in payoff diagram between strike prices

**Comparison with Straddle**:

- **Cost**: Lower than straddle (cheaper put option with lower strike)
- **Payoff**: Flat zone between the two strike prices
- **Breakeven**: Requires less movement than straddle

**Example Comparison**:

- **Straddle**: Call (E=15) + Put (E=15) = ₹2 + ₹1 = ₹3
- **Strangle**: Call (E=15) + Put (E=12.5) = ₹2 + ₹0.25 = ₹2.25
- **Advantage**: Need only ₹2.25 movement vs. ₹3 for straddle

## 4. Key Trading Concepts

### 4.1 Volatility Betting

**Core Principle**: Both straddle and strangle are bets on **movement**, not direction

- Profit from high volatility regardless of price direction
- Used when expecting significant news/events but uncertain of outcome

### 4.2 Risk Management

**Options as Insurance**:

- Put options provide downside protection
- Call options in short positions limit upside losses
- Cost of "insurance" must be weighed against potential benefits

### 4.3 Portfolio Construction

**Combining Instruments**:

- Multiple financial instruments can be combined for complex strategies
- Each component serves specific risk/reward purpose
- Total payoff = sum of individual instrument payoffs

## 5. Real-World Applications

### 5.1 Event-Driven Trading

**Scenario**: Major corporate events (mergers, court cases, elections)

- High uncertainty about outcome
- Certainty about significant price impact
- Straddle/strangle strategies capitalize on volatility

### 5.2 Risk Hedging

**Portfolio Protection**:

- Long stock positions hedged with put options
- Short positions hedged with call options
- Balance between protection cost and risk reduction

## Key Formulas and Notation

- **Call Option Payoff (Long)**: max(ST - E, 0) - PCE
- **Put Option Payoff (Long)**: max(E - ST, 0) - PPE
- **Short Stock Payoff**: S₀ - ST (where S₀ = initial sale price)
- **Straddle Cost**: PCE + PPE
- **Straddle Payoff**: |ST - E| - (PCE + PPE)

## Important Terms

- **Strike Price (E)**: Predetermined price for option exercise
- **Expiration Date (T)**: Date when option expires
- **Premium**: Price paid for option
- **Exercise**: Using the right provided by option
- **Volatility**: Measure of price movement magnitude
- **Hedge**: Strategy to reduce risk exposure

[[W1L5 - Hedging]]