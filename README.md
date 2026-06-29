# magmatic-redox-conformal

> **Major-element composition predicts tectonic setting, not oxygen fugacity** — a leakage-honest cross-setting benchmark with conformal uncertainty quantification.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

Code and data to reproduce the paper. A gradient-boosted model predicts magmatic redox (ΔQFM) from the ten major oxides of basaltic melts. Its apparent skill turns out to be **data leakage**: the model recognises the *tectonic setting* rather than predicting *redox*.

![Leakage and conformal coverage](figures/fig2_leakage_conformal.png)

## Key result

| Evaluation | R² |
| --- | --- |
| Random 5-fold CV | **0.55** |
| Leave-one-tectonic-setting-out | **0.03** |
| Setting-mean baseline | 0.38 |

The 0.52 gap between random and hold-out scores *is* the leakage. Split-conformal intervals are valid under exchangeable sampling (~91 % coverage) but collapse under setting shift (30 % on the arc); per-setting **Mondrian** calibration restores nominal coverage. The transferable redox signal lives in trace-element ratios (Ba/La vs ΔQFM, *r* = 0.93), not major elements.

## Contents

```text
magmatic_redox_conformal.ipynb   full analysis (Colab notebook)
magmatic_redox_conformal.py      same analysis as a plain script
data/
  cottrell2021_volcanics_unified.csv   684 volcanic glasses
figures/
  fig1_dQFM_by_setting.png       ΔQFM by tectonic setting
  fig2_leakage_conformal.png     leakage diagnosis + conformal coverage
  fig3_trace_context.png         trace-element context (Ba/La, V/Yb)
  figS1_loso_scatter.png         leave-one-setting-out predicted vs observed
requirements.txt
```

## Run

**Google Colab** — open `magmatic_redox_conformal.ipynb`, upload `data/cottrell2021_volcanics_unified.csv` when prompted, then **Runtime → Run all**.

**Locally**

```bash
pip install -r requirements.txt
cp data/cottrell2021_volcanics_unified.csv .   # the script reads it from the current folder
python magmatic_redox_conformal.py
```

Runs in a few minutes on a single CPU — no GPU required. Figures are written at 300 dpi (PNG + PDF). The script also accepts the original IEDA workbook (`.xlsx`) in place of the CSV.

## Data

Sample-level oxygen fugacities and major-element compositions are from
Cottrell, E., Birner, S. K., Brounce, M., Davis, F. A., Waters, L. E. & Kelley, K. A. (2021),
*Oxygen Fugacity Across Tectonic Settings*, Version 1.0, Interdisciplinary Earth Data Alliance —
<https://doi.org/10.26022/IEDA/111899>.

## Citation

```bibtex
@article{khairbek2026magmaticredox,
  author  = {Khairbek, Ali A.},
  title   = {Major-element composition predicts tectonic setting, not oxygen
             fugacity: a leakage-honest cross-setting benchmark with conformal
             uncertainty quantification},
  year    = {2026}
}
```

## License

Code released under the **MIT License**. The underlying data follow the terms of the IEDA source listed above.
