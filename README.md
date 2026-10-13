<!-- solve-problem:1d48ccb1-684a-4d4f-9494-e6efb602ed96 -->
# Execution-ticket capital concentration

A [Tangle Solve problem](https://solve.tangle.tools/problems/1d48ccb1-684a-4d4f-9494-e6efb602ed96).

## What is the problem?

**Setting.** In Ethereum's proposed execution-ticket (ET) design, agents buy "execution tickets" for the right to propose (or select the proposer of) future blocks, thereby capturing MEV. Formally: in each period, tickets are sold (e.g., via uniform-price or fixed-price lottery/sale), and a winner gains the right to extract MEV of stochastic value $V$ for that slot. Buyers differ in two dimensions:

- **Financing costs:** buyer $i$ faces per-dollar cost $r_i$ of capital (cheap capital ⇒ large funds, low opportunity cost).
- **Risk tolerance:** buyer $i$ has risk aversion $\gamma_i$ (e.g., CARA/CARA-utility or mean-variance), facing the variance of $V$.

**Problem (census statement, formalized):** Characterize — and bound — the equilibrium degree of concentration of ticket purchases (e.g., market share of the largest buyer, HHI, or probability that a single buyer holds a dominant stake) as a function of the distribution of $(r_i, \gamma_i)$ across buyers. Under what conditions on heterogeneity does concentration remain bounded away from monopoly, and when does a single low-$r$, high-risk-tolerance buyer capture (nearly) all advance rights?

**Ambiguity note:** the record does not specify the ticket-sale mechanism (fixed price vs. auction, per-slot vs. continuous), nor the concentration measure. A solver must fix these: a reasonable formalization is a repeated symmetric auction/sale for tickets with heterogeneous values driven by $(r_i, \gamma_i)$, measuring steady-state equilibrium HHI.

## Why does it matter?

Execution tickets are a leading Ethereum roadmap proposal for MEV democratization; if cheap financing lets a whale monopolize tickets, ETs fail their decentralization goal and reproduce PBS-style builder concentration. A concentration bound would tell protocol designers which sale mechanisms (per-slot caps, subscription smoothing, borrowing constraints) preserve dispersion, and would feed into financial-constrained auction design more broadly. Without it, ET deployment risks optimizing MEV capture at the cost of censorship resistance and proposer decentralization.

## What's already known?

- Burian, Crapis, Saleh (2024), *MEV Capture and Decentralization in Execution Tickets* (arXiv:2408.11255), analyze ET equilibrium, characterize conditions under which ETs fully capture MEV, and identify that these conditions are restrictive — with heterogeneity in financing costs/risk tolerance, ticket holdings concentrate and full MEV capture or decentralization fails. (Verify precise theorem statements from the paper; the census summarizes it at this level.)
- The census tags this exact concentration problem as open since that 2024 analysis; no published bound on concentration as a function of $(r_i, \gamma_i)$ heterogeneity is recorded.
- Adjacent literatures: financially constrained/budget-constrained auction theory (where wealth heterogeneity causes concentration and first-price auctions favor deep pockets), and PBS/builder-concentration empirical work — suggestive analogies, not solved versions of this problem.

## What would count as solving it?

1. **Upper/lower bounds:** Given a specified sale mechanism and buyer distribution over $(r_i, \gamma_i)$, prove a bound on steady-state equilibrium concentration (e.g., expected top buyer's share or HHI) — ideally showing it converges to 1 as cost dispersion grows (monopoly result) and stays below some $\bar{c}<1$ under bounded heterogeneity.
2. **Mechanism design:** Construct a modified ET sale (caps, convex pricing, smoothed ticket streams) with a proven concentration bound while retaining near-full MEV capture.
3. **Referee criterion:** rigorous equilibrium analysis (existence + uniqueness or selection), with explicit dependence of concentration on primitives; or a calibrated simulation demonstrating a phase transition in financing-cost dispersion (weaker, empirical variant).

## How to start

1. Read arXiv:2408.11255 end-to-end; extract the exact model of ticket purchase, the MEV-capture conditions, and where heterogeneity enters — that model is your baseline.
2. Formalize a minimal two-buyer version: one deep-pocketed low-$r$ buyer vs. one constrained buyer, CARA utility over stochastic MEV, uniform-price ticket sale. Solve for equilibrium shares; this gives the monopoly comparative statics.
3. Bring in budget-constrained auction tools (Balakrishnan/Said/Chawla-style constrained-bidder results — verify applicability) to extend to $n$ buyers.
4. **Main obstacle:** endogenous repetition — concentrated holdings change future financing and risk exposure, so steady-state analysis requires handling dynamics; two-period or mean-field approximations are natural first cuts.

## Key references

- Burian, I., Crapis, D., Saleh, F. (2024), "MEV Capture and Decentralization in Execution Tickets," arXiv:2408.11255. Analyzes execution-ticket equilibria and shows the conditions for complete MEV capture are restrictive, with concentration emerging under buyer heterogeneity. https://arxiv.org/abs/2408.11255
- (Verify) Literature on financially/budget-constrained auction design — the census lists "financially constrained auction design" as the related field; a solver should search for budget-constrained first-price/share auctions as the closest transferable toolkit.

## Warnings

- The census record is thin; the "restrictive conditions for complete MEV capture" claim is attributed to the 2024 paper but theorem-level details must be verified against the actual text before building on them.
- Don't conflate two distinct objectives: MEV *capture* (protocol revenue) and *decentralization* (dispersion of rights) — improving one can worsen the other; state which you're bounding.
- Mechanism details (fixed-price vs. auction, per-slot lotteries vs. subscriptions) materially change the answer; declare yours upfront or the result is ill-defined.
- Real-world financing (leverage, derivatives on ticket streams) can break budget-cap fixes; check your mechanism against such circumvention before claiming robustness.

---
*`BCGT-000097` · flagged for review*

## Acceptance guidance

1. **Upper/lower bounds:** Given a specified sale mechanism and buyer distribution over $(r_i, \gamma_i)$, prove a bound on steady-state equilibrium concentration (e.g., expected top buyer's share or HHI) — ideally showing it converges to 1 as cost dispersion grows (monopoly result) and stays below some $\bar{c}<1$ under bounded heterogeneity.
2. **Mechanism design:** Construct a modified ET sale (caps, convex pricing, smoothed ticket streams) with a proven concentration bound while retaining near-full MEV capture.
3. **Referee criterion:** rigorous equilibrium analysis (existence + uniqueness or selection), with explicit dependence of concentration on primitives; or a calibrated simulation demonstrating a phase transition in financing-cost dispersion (weaker, empirical variant).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/1d48ccb1-684a-4d4f-9494-e6efb602ed96?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000097.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000097)
