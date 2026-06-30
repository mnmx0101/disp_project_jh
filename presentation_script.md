# Iraq IDP Modeling: Detailed Presentation Script

## Meeting Overview & Analysis Structure

* **Opening:** "Hi everyone, thanks for joining. Today I’d like to share where we currently are with the empirical modeling of internal displacement in Iraq (2014–2024)."
* **How we approached the analysis:**
  * "Instead of putting all variables into the model at once, we tried building it sequentially."
  * "We started with a basic autoregressive model and then layered in conflict, climate, and economic blocks step-by-step."
  * "This was mostly to help us see if the climate and conflict patterns hold up as we add more controls."
* **Stress Testing:**
  * "We didn't just stop at the baseline."
  * "Because we hope to use these estimates as the core engine for our future scenario projections, we wanted to feel as confident as possible in the coefficients ($\beta$)."
  * "So, we ran some stress tests across different time lags, spatial definitions, and tried filtering out districts with poorer quality data."
* **Complex Dynamics & Projections:**
  * "We also spent some time exploring complex dynamics like potential non-linearities and interacting shocks."
  * "Toward the end, I'll walk through how we might use these empirical estimates to help drive our upcoming scenario-based projections."
  * "We want to be open that the overall explanatory power reflects the inherent noise in displacement data, meaning any future projections will naturally carry uncertainty bounds."
  * "But we feel these stress-tested coefficients give us a reasonable, data-driven starting point."

---

## Slide-by-Slide Speaking Notes

### Slide 1: Introduction
* **Goal:** "What we’re primarily trying to do here is understand the potential independent effects of climate anomalies on internal displacement in Iraq."
* **Context:** "We’re trying to do this by conditioning on the major conflict and economic shocks we observed between 2014 and 2024."

### Slide 2: What are we modelling?
* **The Outcome:** "For our outcome, we focused on the month-to-month *growth rate* of IDP stocks."
* **Why Stocks?** "This acts as a net measure. It captures the overall balance of returns, departures, and new arrivals, rather than trying to isolate specific migration flows, which the data might struggle to support reliably."

### Slide 3 & 3-1: Data Missingness & Quality
* **The Challenge:** "As you might expect, historical IDP data has some severe temporal gaps."
  * "Interestingly, while early gaps seem related to active conflict, the most widespread missingness actually shows up after October 2018."
  * "This was a period when overall IDP numbers largely stabilized, which seems to have led to less frequent data collection."
* **Our Solution:** "Since the trajectories looked relatively stable between the collected months during this post-2018 period, we felt comfortable linearly interpolating the missing observations."
  * "But just to be careful, we flagged districts with 6 or more consecutive months of missing data, so we could try dropping these 'unreliable' districts during our robustness checks."

### Slide 4: Variable Construction
* **Data Sources:** "We brought together gridded climate data, ACLED conflict events, and some local economic indicators."
* **Collinearity Control:** "One methodological choice worth noting: we decided to exclude neighboring climate variables."
  * "Climate is highly spatially correlated (over 0.90), so including neighbor climate tended to muddy the model."
  * "Conflict, on the other hand, is localized enough that we felt we could meaningfully measure its spillover."

### Slide 5: Econometric Specification
* **The Sequential Approach:** "We set up four models: M0 (Baseline), M1 (+Conflict), M2 (+Climate), and M3 (+Economics)."
* **The Logic:** "Going step-by-step like this lets us observe two things:"
  * "Roughly how much explanatory power each block adds."
  * "Whether our core signals stay fairly consistent as we add more controls."

### Slide 6: Interpreting Coefficients
* **Percentage Points:** "Because we're looking at a log growth rate, it's helpful to remember that our coefficients ($\beta$) roughly represent *percentage-point* changes in that growth rate."
* **Speed vs Volume:** "It might be useful to think of this as measuring changes in the *speed* of displacement growth, rather than absolute numbers of people moving."

### Slide 7: Core Findings (The Forest Plot)
* **Regional Heterogeneity:** "What stood out to us most is that there doesn't seem to be a single national pattern. The patterns look quite different between the North and South."
* **The North:** "The North seems more sensitive to connected conflict spillovers and fairly acute (1-3 month) agricultural shifts."
* **The South:** "The South, meanwhile, appears more influenced by chronic, long-term (10-12 month) environmental degradation."
* **Stability:** "If you look at the table, you can see these core signals stay relatively stable across our specifications."

### Slide 8: Possible Pathways
* **Econometric Reality:** "Of course, the regression only estimates net stock growth, so we can't definitively say *why* people are moving. But it does point toward some possible pathways."
* **North Pathways:** "The regional conflict signal might reflect delayed returns due to surrounding insecurity. The acute greening signal could point to rapid returns when local conditions temporarily improve."
* **South Pathways:** "The chronic environmental signal in the South might suggest a slower process of resource exhaustion that eventually contributes to secondary departures or delays returns."

### Slide 9: Transition to Robustness
* **The Question:** "We wanted to be cautious and see if these baseline results might just be statistical artifacts."
* **The Strategy:** "To check this, we ran the M3 model through several stress tests regarding data quality, timing, and spatial definitions."

### Slide 10: Data & Sample Robustness
* **Dropping Interpolations:** "When we tried dropping the heavily interpolated districts we flagged earlier, the results generally held up."
* **The Result:** "The core environmental and conflict signals actually seemed to persist or even strengthen slightly, which gave us a bit more confidence in them."

### Slide 11: Alternative Temporal Assumptions
* **Testing Timeframes:** "We also tried swapping our 10-12 month historical window for a more recent 7-9 month window."
* **The Contrast:** "This seemed to confirm that the South's displacement is linked to more cumulative, delayed exhaustion, as the signal persisted."
  * "The North, by contrast, continued to look more sensitive to immediate, acute shocks."

### Slide 12: Alternative Spatial Assumptions (Network Size)
* **Testing the Radius:** "We varied the spatial weight matrix from $K=10$ up to $K=30$ nearest neighbors."
* **The Finding:** "Local climate signals seemed fairly insensitive to network size."
  * "But for conflict, the coefficient grew noticeably as we expanded the network, suggesting we might need a broader regional lens to capture conflict spillover properly."

### Slide 13: Regional vs. Relative Local Shocks
* **Mathematical Isolation:** "We tried decomposing our spatial terms into a *Regional average* and a *Relative local deviation*."
* **Conflict vs Climate:** "This suggested that conflict spillover in the North acts primarily as a regional phenomenon."
  * "In contrast, agricultural shocks (NDVI) seemed to operate more at the localized level—meaning it matters if a district is greener or drier than its immediate neighbors."

### Slide 14-1 & 14-2: Interactions & Nonlinearities
* **The Conflict Trap (Interactions):** "We explored some interacting terms and found hints that shocks might multiply."
  * "For example, recent conflict layered on top of historical conflict seems to create a 'conflict trap' that amplifies displacement."
* **Thresholds (Nonlinearities):** "We also looked at squared terms."
  * "It appears that in the South, extreme degradation might eventually hit a saturation point where growth slows down."
  * "While in the North, it might act more like a sudden tipping point."

### Slide 15: Synthesis
* **The Bottomline:** "Looking across these checks, the general narrative seems to hold. Regional conflict spillovers and local agricultural conditions appear to be some of the most stable drivers we can identify for Iraqi displacement."

### Slide 16: Conclusions
* **Summary:** "To sum up, the displacement we're seeing appears highly persistent, regionally distinct, and driven by overlapping timelines of conflict and climate."
* **Limitations:** "While the results seem fairly robust, we definitely want to acknowledge that we are estimating conditional associations here, not definitive causal mechanisms."

### Slide 17: Future Work (Projections)
* **The Engine:** "Since the model predicts monthly stock growth dynamically, we think it could serve as a useful empirical engine for some scenario-based projections."
* **The Math in Action:** "For instance, if we use our derived North coefficient ($\beta=0.201$), a hypothetical doubling of connected conflict deaths would suggest a roughly 13.9 percentage-point increase in growth."
* **Compounding Effect:** "If we started with 10,000 IDPs, that single shock could theoretically compound to over 11,400 IDPs in a month, and over 23,000 IDPs within six months."
  * "This basically illustrates how we hope to approach our upcoming scenario analysis. Thank you."
