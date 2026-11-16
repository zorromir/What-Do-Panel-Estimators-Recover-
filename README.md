# What Do Panel Estimators Recover?

*A small Monte Carlo experiment with individual effects and persistent errors.*

This independent research note explores a basic question in panel econometrics: **what happens when we estimate a coefficient with different methods, even though we know the true value?**

I generate artificial panel data and compare pooled OLS, fixed effects (FE), and first differences (FD). I also experiment with a lagged dependent variable to see how FE behaves in a dynamic model with persistent disturbances.

## The experiment

For individual $i$ in period $t$, the main data-generating process is

```math
\begin{aligned}
y_{it} &= 1+\alpha_i+2x_{it}+u_{it},\\
x_{it} &= v_{it}+0.5\alpha_i,\\
u_{it} &= u_{i,t-1}+e_{it}.
\end{aligned}
```

Here, the individual effect $\alpha_i$ is correlated with the regressor $x_{it}$, while the error $u_{it}$ follows a random walk. The true slope is 2. The baseline simulation uses 200 individuals, 5 periods, and 1,000 repetitions.

- **Pooled OLS** ignores the individual effect and is biased in this setup.
- **Fixed effects** removes the time-invariant individual effect.
- **First differences** removes the individual effect and differences the random-walk error.

The second experiment adds a lagged outcome and looks at the estimated persistence coefficient as the number of periods changes. These results depend on the specific error process and should not be interpreted as a general ranking of panel estimators.

## Files

- [Paper (PDF)](paper/What_Do_Panel_Estimators_Recover.pdf) — the short research note, including tables and figures.
- [LaTeX source](paper/Panel_Estimators_Refined.tex) — editable source for the note.
- [Python simulation](code/panel_monte_carlo_minimal.py) — generates the simulated data, estimates coefficients, and saves two figures.

## Scope and background

This is a small learning exercise, not an empirical study with observed data. In particular, the dynamic-panel results use random-walk disturbances rather than the conventional serially uncorrelated errors often used to introduce dynamic fixed-effects bias.

The initial data-generating process was used in a coursework assignment with Walid Afasi (2026). I independently rewrote the note and reran the simulations for this project.

**Further reading:** Wooldridge, *Econometric Analysis of Cross Section and Panel Data* (2010); Nickell, “Biases in Dynamic Models with Fixed Effects” (1981).

[Personal portfolio](https://zorromir.github.io/)
