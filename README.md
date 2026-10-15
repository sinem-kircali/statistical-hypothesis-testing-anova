# Applied Statistics Case Studies: Process Control and Service-Time Diagnosis

Two business cases worked through with estimation, confidence intervals, hypothesis tests, a two-way ANOVA, and an explicit check of every test's assumptions.

Built for the *Applied Statistics* course (Industrial Engineering, Koç University), as group case exams.

## Case A: Canned cat food filling
Is the filling process under control with respect to the legal lower limit (2.95 oz) and the spill / give-away upper limit (3.10 oz)? Do the two shifts differ?

- **Same average, different consistency:**
  - mean fill is 3.000 vs 3.015 oz (95% CI for the difference includes 0);
  - shift 1's variance is 2.4× shift 2's (Levene p = 0.016).
- **Not a random sample: the filler drifts.**
  - Shift 1's fill weight climbs by **+0.18 oz** across the shift, so its under-weight cans are at the start and its over-weight cans at the end.
  - Shift 2 drifts back down by −0.075 oz.
  - Lag-1 autocorrelation is 0.58 / 0.32, and the runs tests reject randomness.
- **Out-of-limit cans:**
  - shift 1: 14% under-weight, 8% over-weight;
  - shift 2: 2% and 2%.

  These are reported with Agresti–Coull intervals, Agresti–Caffo intervals for the differences, and Fisher exact tests.
- **Capability:** C_pk is 0.26 (shift 1) and 0.53 (shift 2), far below 1.33.
- **Recommendations:**
  - control-chart the run order;
  - re-calibrate the filler at the start of each shift and at regular intervals;
  - fix shift 1's drift first.

## Case B: Restaurant delivery times
After a new evening cook (from 19:00) and a new courier started, customers complained about deliveries taking longer than 25 minutes. Who is responsible?

- **Cooks:** the new cook's preparation time averages 16.1 min vs 8.1 min, far above the 10-minute target. **All 9 late deliveries** were orders from the new cook.
- **Two-way ANOVA** of total delivery time (cook × courier):

  | Effect | F | p |
  |---|---|---|
  | **cook** | 41 | < 0.001 |
  | courier | 0.96 | 0.33 |
  | interaction | 1.37 | 0.25 |

- **Couriers:**
  - The new courier's on-time share (78%) is significantly below the 90% target (exact binomial p = 0.047).
  - The new courier's travel time is *not* significantly above the 8-minute target, and the new courier is not significantly slower than the other one.
  - All of the new courier's late deliveries are orders from the slow kitchen.
- **Method note:** with n = 27 the normal approximation for the 90% test is unreliable (np₀(1−p₀) = 2.4). It gives p = 0.017 instead of the exact 0.047.
- **Recommendation:** fix the evening preparation process, and do not blame the courier.

## Methods
- Descriptive statistics, histograms, box plots, run-order plots, normal Q-Q plots, Shapiro–Wilk tests.
- Randomness checks: autocorrelation, runs test, linear trend.
- Intervals:
  - t-intervals for means and chi-square intervals for standard deviations;
  - Welch intervals for differences of means;
  - Agresti–Coull and Agresti–Caffo intervals for proportions and their differences.
- Tests:
  - one-sided z-tests with known σ;
  - exact binomial and Fisher exact tests;
  - Levene's test.
- Process capability (C_p, C_pk).
- Two-way ANOVA with interaction (statsmodels).

## Structure
```
applied_statistics_case_studies.ipynb   both cases with outputs
data/                                   place CF1.xlsx, Ahmet.xlsx, Mehmet.xlsx, KamilUsta.xlsx, SuphiUsta.xlsx here (not included)
```

## Tech stack
Python · pandas · SciPy · statsmodels · matplotlib
