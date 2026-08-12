# Retail merchandise planning · sample dataset

Synthetic data for a merchandise financial planning demo. Every figure is
generated. It describes no real company, and contains no real sales,
inventory, vendor or customer information.

The subject is the financial merchandise plan and the receipt buy plan for a
mid-size children's apparel brand: what was planned, what is selling, and what
still needs to be bought to support the rest of the year.

## Shape

| File | Grain | Rows |
|---|---|---|
| `dim_calendar` | fiscal month | 36 |
| `dim_channel` | channel | 3 |
| `dim_product` | style | 112 |
| `dim_vendor` | vendor | 5 |
| `fact_merch_plan` | month x channel x department x plan version | 4,320 |
| `fact_actuals` | month x channel x department, closed months only | 1,800 |
| `fact_open_to_buy` | month x channel x department, forward months | 360 |
| `fact_style_month` | style x month x channel | 1,957 |

Fiscal calendar is NRF 4-5-4 with a February start. FY2026 runs 1 Feb 2026 to
30 Jan 2027 and is set mid-year: February through July are actuals, August
through January are plan.

## The identity

Every row of `fact_merch_plan` satisfies this to the cent:

    EOM = BOM + Receipts@retail - Sales$ - Markdown$ - Shrink$

which rearranges to the buy:

    Receipts@retail = EOM_target + Sales$ + Markdown$ + Shrink$ - BOM

Receipts at cost derive from retail using channel IMU.

## Note on grain

Department names repeat across divisions. `Sets`, `Sleepwear`, `Bottoms`,
`Tops`, `Swim` and `Dresses` each appear under more than one division, so there
are 20 real departments but only 9 distinct department labels. Group on
division and department together, never on department alone.

## Licence

Public domain. Use it for anything.
