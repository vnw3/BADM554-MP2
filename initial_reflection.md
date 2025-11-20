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

### Bonus Question 4 (If Time Permits): Entity Dominance

**"Which labeled entities (exchanges, DeFi protocols) dominate USDC flows?"**

**Why this matters for our bank:**

- Understanding the ecosystem structure
- Identifying key counterparties and dependencies
- Competitive intelligence: where do users actually use USDC?
- Partnership opportunities: should we integrate with these platforms?

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

### D. Entity Flow Metrics (Bonus)

- **Entity Volume Share:**

  - Top 10 exchanges by volume
  - Top 10 DeFi protocols by volume
  - % of volume through labeled vs. unlabeled addresses

- **Flow Analysis:**
  - Inflow/outflow for major exchanges
  - Net flows to/from DeFi protocols
  - Exchange-to-exchange flows

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

## 6. Preliminary Analysis Approach

### Phase 1: Establish Baseline (Week 1)

1. Query total USDC supply and daily volumes
2. Identify top holders and calculate concentration ratios
3. Pull price data and calculate daily deviations
4. Map out major labeled entities

### Phase 2: Risk Deep-Dive (Week 1-2)

1. **Concentration Analysis:**

   - Calculate top holder percentages over time
   - Identify if concentration is growing or shrinking
   - Label top holders (exchanges, protocols, unknown)

2. **Stability Analysis:**

   - Plot daily price with $1.00 baseline
   - Mark depeg events (>1% deviation)
   - Correlate depegs with volume spikes

3. **Volume Spike Analysis:**

   - Calculate rolling averages and standard deviations
   - Flag anomalous days (>2σ from mean)
   - Investigate what caused major spikes

4. **Entity Flow Analysis (if time):**
   - Calculate volume share by entity type
   - Visualize flow between major entities

### Phase 3: Risk Synthesis (Week 2)

1. Synthesize findings into risk categories:
   - **High Risk:** Issues requiring immediate attention
   - **Medium Risk:** Issues to monitor
   - **Low Risk:** Acceptable risk levels
2. Develop recommendations for bank leadership

---

## 7. Potential Limitations & Challenges

### Data Limitations We Anticipate:

- **On-chain only:** Won't capture off-chain USDC held by Circle or custodians
- **Ethereum-only:** USDC exists on multiple chains (Polygon, Arbitrum, etc.)
- **Unlabeled wallets:** Many large holders may not be labeled in Dune
- **Historical depth:** Only analyzing last 6 months (may miss important historical events)

### Technical Challenges We Expect:

- **SQL complexity:** Window functions for moving averages, CTEs for complex joins
- **Query performance:** Large datasets may require optimization
- **Labeling accuracy:** Not all entities are correctly labeled in Dune
- **Interpretation:** Distinguishing between "normal" and "risky" behavior requires domain knowledge

### Analytical Challenges:

- **Causation vs. correlation:** Volume spikes correlate with many events
- **Defining thresholds:** What concentration % is "too high"?
- **Context needed:** Need to understand broader crypto market events during analysis period

---

## 8. Success Criteria

Our analysis will be successful if we can confidently answer:

✅ **For Leadership:**

- Should we proceed with offering USDC services? (Yes/No/Conditional)
- What are the top 3 risks we face?
- What risk mitigation strategies should we implement?

✅ **For Risk Committee:**

- What is the concentration risk profile?
- How stable is USDC during market stress?
- What operational risks exist during high-volume periods?

✅ **For Project Grading:**

- Clear, data-driven story with 4-5 compelling visualizations
- SQL queries that demonstrate technical proficiency
- Professional slide deck with actionable recommendations

---

## 9. Initial Hypotheses (To Be Tested)

Before diving into data, our team's initial hypotheses:

**H1: Concentration**

- We expect USDC to be moderately concentrated (top 20 holders = 30-50% of supply)
- Most large holders will be exchanges and DeFi protocols (not individuals)
- Concentration has likely decreased as USDC adoption grows

**H2: Stability**

- USDC maintains its peg better than most stablecoins
- Depegs are rare (<5 events in 6 months) and short-lived (<24 hours)
- Major depegs correlate with broader crypto market crashes

**H3: Volume**

- Daily volume is relatively stable with occasional 2-3x spikes
- Spikes correspond to market volatility events
- Institutional transactions (large size) dominate total volume

**H4: Entities**

- Top 5 exchanges account for >60% of USDC volume
- Coinbase and Binance are likely dominant
- DeFi protocols (Aave, Uniswap) represent growing but smaller share

_Note: These are preliminary guesses to guide our analysis - we will let the data tell the real story._

---

## 10. Next Steps

### Immediate Actions (This Week):

1. ✅ Complete this initial reflection
2. Set up Dune Analytics account
3. Explore USDC-related dashboards for inspiration (not copying)
4. Read Dune documentation on key tables
5. Write first exploratory SQL query (daily volume)

### AI Tool Usage Plan:

- Use AI to explain Dune table schemas
- Ask AI for SQL query optimization help
- Use AI to review our risk interpretation logic
- Have AI critique our executive summary draft

### Team Coordination:

- Assign query development tasks
- Schedule mid-week check-in to review progress
- Set up shared document for SQL query library
- Plan slide deck outline together

---

## 11. Risk Assessment Framework

We will evaluate findings using a standard risk matrix:

| Risk Level | Concentration   | Price Stability        | Volume Volatility      |
| ---------- | --------------- | ---------------------- | ---------------------- |
| **Low**    | Top 20 < 40%    | Depeg < 0.5%, < 2x/6mo | Spikes < 2x, < 5x/6mo  |
| **Medium** | Top 20 = 40-60% | Depeg 0.5-2%, 2-5x/6mo | Spikes 2-3x, 5-10x/6mo |
| **High**   | Top 20 > 60%    | Depeg > 2%, > 5x/6mo   | Spikes > 3x, > 10x/6mo |

**Final Recommendation Framework:**

- **All Low:** ✅ Proceed with USDC services
- **One High:** ⚠️ Proceed with caution, implement specific controls
- **Multiple High:** 🛑 Do not proceed, re-evaluate in 6 months

---

## Appendix: Key Terms

**Depeg:** When a stablecoin's price deviates significantly from its $1.00 target  
**Whale:** A wallet holding a very large amount of a cryptocurrency  
**HHI (Herfindahl-Hirschman Index):** Measure of market concentration (0-10,000 scale)  
**Gini Coefficient:** Measure of inequality in distribution (0 = perfect equality, 1 = perfect inequality)  
**DeFi:** Decentralized Finance protocols (lending, trading, liquidity pools)  
**Labeled address:** Wallet address identified by Dune as belonging to a known entity

---
