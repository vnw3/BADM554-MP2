# Initial Reflection: Stablecoin Risk Analysis

## Project: Analyzing USDC for Regional Bank Risk Assessment

---

## 1. Chosen Persona

**The Risk Analyst**

**Company Type:** Regional bank or fintech startup  
**Department:** Risk Management / Treasury Operations  
**Reporting To:** Chief Risk Officer (CRO) and Chief Financial Officer (CFO)

### Business Context

Our bank is exploring the possibility of offering stablecoin services to customers, including:

- Accepting USDC deposits
- Facilitating USDC transfers for cross-border payments
- Providing USDC-to-USD conversion services
- Potentially holding USDC in treasury reserves

Before proceeding, senior leadership needs a comprehensive risk assessment of the stablecoin infrastructure to understand:

- **Operational risks** (can the network handle our transaction volume?)
- **Concentration risks** (are we dependent on a few large holders?)
- **Stability risks** (does the peg hold during stress?)
- **Counterparty risks** (who controls the ecosystem flows?)

---

## 2. Chosen Stablecoin

**USDC (USD Coin)**

### Why USDC?

- **Transparency:** Circle (issuer) provides regular attestations
- **Regulatory compliance:** Strong regulatory positioning in the US
- **Institutional adoption:** Widely used by traditional finance companies
- **Market size:** Second-largest stablecoin (~$40B+ market cap)
- **Data quality:** Well-labeled addresses on Dune, good for entity analysis

### Analysis Time Period

**Last 6 months** (approximately May 2025 - November 2025)

- Recent enough to reflect current market conditions
- Long enough to capture normal vs. stress periods
- Includes enough data points for trend analysis

---

## 3. Key Business Questions

We will focus on **THREE core risk questions** that directly inform our bank's decision:

### Question 1: Concentration Risk - Whale Analysis

**"How concentrated is USDC usage across different wallets?"**

**Why this matters for our bank:**

- If a few whales control most USDC, their actions could destabilize the ecosystem
- High concentration = higher systemic risk (what if a whale exits?)
- Banks need to understand counterparty concentration limits
- Regulatory concerns about market manipulation

**What we need to find:**

- Who holds the most USDC?
- What percentage of total supply do top holders control?
- Is concentration increasing or decreasing over time?
- Are holders identifiable entities (exchanges, protocols) or unknown wallets?

---

### Question 2: Price Stability Risk

**"How stable is the USDC price around $1.00 over time?"**

**Why this matters for our bank:**

- Our customers expect $1 USDC = $1 USD at all times
- Price deviations = potential losses for the bank and customers
- Need to know: how often does USDC "depeg" and by how much?
- Stress test scenario: what happens during market crashes?

**What we need to find:**

- Daily price variance from the $1.00 peg
- Maximum depeg events (worst-case scenarios)
- How long do depegs last? (recovery time)
- Correlation between depegs and market stress events

---

### Question 3: Liquidity & Activity Risk

**"Do we see periods of unusual activity or spikes in volume?"**

**Why this matters for our bank:**

- Sudden volume spikes = potential liquidity crises or bank runs
- Need to know if the network can handle stress periods
- Unusual activity might indicate market manipulation or panic
- Operational planning: can we serve customers during high-volatility periods?

**What we need to find:**

- What is "normal" daily transaction volume?
- How frequent are volume spikes? (>2x or >3x normal)
- What triggers spikes? (market events, protocol issues, etc.)
- Are spikes concentrated in certain entities or distributed?

---

**What we need to find:**

- Top exchanges by USDC volume
- Top DeFi protocols using USDC
- Flow patterns between entities (where does USDC move?)
- Are flows centralized through a few hubs or distributed?

---

## 4. Metrics We Think We'll Need

### A. Concentration Metrics

- **Top N Holder Analysis:**

  - Top 10 holders' balance as % of total supply
  - Top 20 holders' balance as % of total supply
  - Top 100 holders' balance as % of total supply

- **Concentration Indices:**

  - Gini coefficient (if calculable - measures inequality)
  - Herfindahl-Hirschman Index (HHI) for market concentration
  - % of supply held by labeled vs. unlabeled wallets

- **Trend Analysis:**
  - Change in concentration over time (6-month trend)
  - New large holders appearing vs. existing whales

### B. Price Stability Metrics

- **Deviation Metrics:**

  - Daily average price
  - Daily standard deviation from $1.00
  - Maximum positive deviation (above $1.00)
  - Maximum negative deviation (below $1.00)

- **Depeg Events:**

  - Count of days where price > $1.01 or < $0.99
  - Duration of depeg events (consecutive days off-peg)
  - Severity of worst depeg (max % deviation)

- **Recovery Metrics:**
  - Average time to return to $0.99-$1.01 range
  - Volatility during stress periods

### C. Volume & Activity Metrics

- **Volume Metrics:**

  - Daily transaction count
  - Daily transfer volume (USD value)
  - 7-day and 30-day moving averages
  - Standard deviation of daily volume

- **Spike Detection:**

  - Days with volume >2x the 30-day average
  - Days with volume >3x the 30-day average
  - Largest single-day volume in 6-month period

- **Activity Patterns:**
  - Unique active wallets per day
  - Average transaction size
  - Distribution: retail (<$1K) vs. institutional (>$100K)

---

## 5. Expected Data Sources (Dune Tables)

Based on initial research, we expect to use:

| Table Name                    | What We'll Use It For                              |
| ----------------------------- | -------------------------------------------------- |
| `erc20_ethereum.evt_Transfer` | Core USDC transfer events (from/to/amount)         |
| `prices.usd`                  | USDC price data over time for stability analysis   |
| `tokens_ethereum.balances`    | Current wallet balances for concentration analysis |
| `labels.all`                  | Identify exchanges, protocols, known entities      |
| `ethereum.transactions`       | Transaction fees and success rates (optional)      |

---

## Appendix: Key Terms

**Depeg:** When a stablecoin's price deviates significantly from its $1.00 target  
**Whale:** A wallet holding a very large amount of a cryptocurrency  
**HHI (Herfindahl-Hirschman Index):** Measure of market concentration (0-10,000 scale)  
**Gini Coefficient:** Measure of inequality in distribution (0 = perfect equality, 1 = perfect inequality)  
**DeFi:** Decentralized Finance protocols (lending, trading, liquidity pools)  
**Labeled address:** Wallet address identified by Dune as belonging to a known entity

---
