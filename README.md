# PCA, Random Matrices, and Market Modes

This project is my first taste of quantitative finance, and it made the field feel genuinely alive to me. We do not know exactly how markets work, but we can model market returns and ask whether hidden structure appears in the data. Through these experiments, I found that the data can tell stories consistent with macroeconomic intuition: during stress regimes, market-wide co-movement becomes stronger, while sector-level exposures shift across regimes. Seeing mathematical tools reveal this kind of structure was deeply fulfilling. As Simons said, "the market is not totally random, and it can be modeled mathematically." I will always keep this sentence in mind.

The central question is:

> Can PCA recover hidden generating patterns from high-dimensional noisy samples?

Starting from synthetic random matrix experiments, I carried out multiple numerical experiments to verify theories in random matrix theory, especially around the BBP phase transition. Then I applied the same PCA viewpoint to equity returns, where the first principal component is interpreted as a market co-movement mode.

## Project Structure

```text
.
├── theories/
│   ├── research_overview.ipynb
│   ├── pure_noise_experiment.ipynb
│   ├── one_factor_spike.ipynb
│   ├── multi_factor_extension.ipynb
│   └── poster.pdf
├── macro_mode_chinese_a_shares.ipynb
├── why_correlation_pca.ipynb
└── README.md
```

## Theory Notebooks

The `theories/` folder contains the mathematical and numerical core of the project.

- `research_overview.ipynb` introduces the project motivation and the PCA/SVD viewpoint.
- `pure_noise_experiment.ipynb` uses the Marchenko-Pastur law as a pure-noise benchmark.
- `one_factor_spike.ipynb` studies a one-factor spiked covariance model and numerically verifies the BBP phase transition.
- `multi_factor_extension.ipynb` extends the one-factor model to multiple hidden factors and tests outlier counting and subspace recovery.
- `poster.pdf` is the final research poster.

## Empirical Extension

`macro_mode_chinese_a_shares.ipynb` applies rolling correlation PCA to Chinese A-shares in two regimes:

- Property stress: 2021-11-01 to 2022-10-31
- Tech/dividend: 2025-06-30 to 2026-03-31

The notebook focuses on PC1 as a market co-movement mode. The main diagnostics are:

- PC1 explained variance ratio, measured by `lambda_1 / N`
- PC1 sign coherence
- correlation between PC1 score and CSI 500 index return
- SW2021 sector-average PC1 loadings

In the current experiment, PC1 score is highly correlated with CSI 500 returns in both regimes, suggesting that PC1 is a useful indicator of broad market co-movement rather than a direct price-trend detector.

## Why Correlation PCA?

`why_correlation_pca.ipynb` is a synthetic experiment explaining why correlation PCA is often preferable to covariance PCA for equity returns. In a covariance matrix, high-volatility stocks can dominate the principal component even when their underlying factor exposure is not the main signal. Standardizing returns before PCA makes the analysis focus more on co-movement structure.

## Data Notes

The A-share notebook uses Tushare data. To rerun the notebook, set your token locally:

```bash
export TUSHARE_TOKEN="your_token_here"
```

No token is included in this repository.

Large cached market data files are intentionally not included. The notebook downloads and caches the required data locally when run.

## References

- Marchenko and Pastur, "Distribution of eigenvalues for some sets of random matrices", 1967.
- Baik, Ben Arous, and Peche, "Phase transition of the largest eigenvalue for nonnull complex sample covariance matrices", 2005.
- Johnstone, "On the distribution of the largest eigenvalue in principal components analysis", 2001.
