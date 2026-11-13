# DataCo Supply Chain Analysis: South America, Indoor/Outdoor Games

Notebook analysis of the [DataCo Smart Supply Chain dataset](https://data.mendeley.com/datasets/8gx2fvg2k6/5), filtered to **South America** and **Indoor/Outdoor Games** (1,681 of 180,519 orders). It covers late-delivery drivers, cost-optimised fraud detection, and safety-stock planning.

## Findings

| Task | Method | Result |
|---|---|---|
| Late delivery | EDA by shipping mode, segment, country | **55.74%** of orders at late risk. Shipping mode drives it: First Class 92.0%, Second Class 80.5%, Same Day 61.3%, Standard 40.3%. Customer segment has almost no effect (55-56%). |
| Fraud detection | Random Forest (100 trees, 70/30 stratified split); threshold chosen to minimise FP x $25 + FN x $300 | Optimal threshold **0.7227**; cost $3,900 vs $4,000 at 0.50 (saves $100). |
| Inventory | 3-month moving-average forecast; safety stock = Z x sigma x sqrt(lead time) at 85% service level | Forecast **441** units + safety stock **49** = order-up-to level **491** units. |

**Caveats:** only 44 fraud cases (about 13 in the test set) and 11 months of demand data, so the fraud and forecast results are illustrative. The $25 / $300 costs and 85% service level are assumed inputs.

## Run

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter
```

1. Download the CSV from the dataset link above and place `DataCoSupplyChainDataset.csv` next to the notebook (it is ~96 MB; add it to `.gitignore`).
2. Run `jupyter notebook DataCo_Analysis.ipynb` top to bottom. The CSV is read with `encoding="ISO-8859-1"`.

## Next steps

- Check fraud features for leakage (`SUSPECTED_FRAUD` is an order status; `Sales` and `Order_Item_Total` overlap).
- Evaluate with precision/recall, PR-AUC and cross-validation; handle class imbalance.
- Compare the moving average against exponential smoothing or SARIMA.

## Credit

Constante, F., Silva, F., Pereira, A. (2019). *DataCo Smart Supply Chain for Big Data Analysis.* Mendeley Data. Check the dataset page for licence terms.

**Author:** Faria Hassan, BBA (Finance), North South University
