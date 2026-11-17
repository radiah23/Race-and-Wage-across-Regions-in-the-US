# Race and Wages Across U.S. Regions

**Were Black men paid less than non-Black men with the same education and experience, and did the gap differ by region? A multiple regression case study on 25,632 workers from the Current Population Survey.**

![R](https://img.shields.io/badge/R-276DC3?logo=r&logoColor=white)
![Quarto](https://img.shields.io/badge/Quarto-39729E?logo=quarto&logoColor=white)
![Regression](https://img.shields.io/badge/method-multiple%20regression-blue)

Case study for **SDS 291: Multiple Regression** at Smith College, co-authored by **Radiah Khan, Mercer Mercer, Catherine Weeks and Nafisa Mohamed**. Full report: [`main.pdf`](main.pdf).

---

## Question

The Census Bureau's Current Population Survey (CPS) tracks the economic status of the U.S. labor force. Using a sample of **25,632 male respondents from March 1988**, we asked:

> After adjusting for education and experience, did Black men earn less than non-Black men, and **did that gap change across the Northeast, Midwest, South and West**?

## Approach

1. **Exploratory analysis**: weekly wages by race, region and experience band (0–20, 21–40, 41–60 years); average education by race and region.
2. **Multiple linear regression** of wage on education, experience, race, region, and a **race × region interaction**.
3. Wages were right-skewed, so the response was **log-transformed** to satisfy the linearity, normality and equal-variance conditions:

   `log(Wage) ~ Education + Experience + Black * Region`

4. **Nested F-test** comparing the models with and without the interaction terms, to test whether the racial gap differs by region.

## Results

| Term | Estimate (log wage) | Interpretation |
|---|---|---|
| Education | +0.10 per year | ≈ 10% higher weekly wage per extra year of schooling |
| Experience | +0.02 per year | ≈ 2% higher per year of experience |
| **Black** | **−0.19** (p < 0.001) | **≈ 17% lower weekly wage** than comparable non-Black men |
| Black × Region | not significant | F = 1.45, p = 0.23 |

- **A clear, significant racial wage gap exists nationwide**: Black men earned about 17% less than non-Black men with the same education and experience (e^−0.19 − 1 ≈ −17%).
- **The gap is consistent across regions.** The interaction terms were not jointly significant, so there is no evidence that the gap grows or shrinks by region.
- In the exploratory plots, Black men earned less on average within every experience band in every region.

## Limitations

- One month of data from 1988; the results describe that labor market, not today's.
- Men only, and race is coded only as Black vs. non-Black, which hides differences among other groups.
- Self-reported wages leave out informal and unreported work.

## Files

| File | Purpose |
|---|---|
| `main.qmd` | Full analysis (Quarto + R) |
| `main.pdf` | Rendered report |
| `plan.md` | Team research plan |

## Reproduce

```r
install.packages(c("tidyverse", "broom", "flextable", "Sleuth2", "kableExtra"))
quarto::quarto_render("main.qmd")
```

Data: 1988 CPS wage sample from the `Sleuth2` package (Ramsey & Schafer, *The Statistical Sleuth*).
