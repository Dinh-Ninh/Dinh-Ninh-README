\---

type: spec

capability: marginal-analysis

engagement: perfect-competition

date: 2026-10-16

status: draft            # draft | built | audited

built\_with: "Claude Code, from this file"  

\---



\# Marginal Analysis – Model Specification



\## Purpose



The model will assist the farm in making decisions on how many of the 64 available beds should be allocated to tomatoes, carrots, and mesclun to achieve the highest possible profits during the 36-week growing season. The model needs to find the best allocation of beds to each crop taking into account revenue, fertilizer cost, decreased need for labor as time goes on, labor cost, and the farm's available beds and labor.



\## Inputs — the named contract



| Name | Value | Unit | Source |

|---|---|---|---|

| `WEEKS` | 36 | weeks per season | Case Givens |

| `BED\_CAP` | 64 | beds | Case Givens |

| `FIXED\_COST` | 20000 | USD per season | Case Givens |

| `FARMER\_HOURS` | 720 | hours per season | Case Givens |

| `FARMER\_PAY` | 50000 | USD per season | Case Givens |

| `FARMER\_PAID\_HOURS` | 1440 | hours per season | Case Givens |

| `TEMP\_WORKERS\_MAX` | 4 | workers | Case Givens |

| `TEMP\_PAY` | 25000 | USD per worker per season | Case Givens |

| `TEMP\_HOURS` | 1440 | hours per worker per season | Case Givens |

| `TOM\_MAX` | 20 | beds | Case scenario, crop table |

| `TOM\_PRICE` | 8800 | USD per bed | Case scenario, crop table |

| `TOM\_HRS` | 2.5 | hours per week per bed | Case scenario, crop table |

| `TOM\_FERT` | 880 | USD per bed | Case scenario, crop table |

| `TOM\_DIM` | 0.10 | proportion | Case scenario, crop table |

| `CAR\_MAX` | 20 | beds | Case scenario, crop table |

| `CAR\_PRICE` | 2094 | USD per bed | Case scenario, crop table |

| `CAR\_HRS` | 2.5/3 | hours per week per bed | Case scenario, crop table |

| `CAR\_FERT` | 440 | USD per bed | Case scenario, crop table |

| `CAR\_DIM` | 0.025 | proportion | Case scenario, crop table |

| `MES\_MAX` | 30 | beds | Case scenario, crop table |

| `MES\_PRICE` | 2700 | USD per bed | Case scenario, crop table |

| `MES\_HRS` | 2.5/2 | hours per week per bed | Case scenario, crop table |

| `MES\_FERT` | 880 | USD per bed | Case scenario, crop table |

| `MES\_DIM` | 0.0125 | proportion | Case scenario, crop table |



\## Structure



The workbook is divided into four parts; Inputs, Calculations, Optimization, and Validation. In the "Inputs" section you'll find all of your farm wide inputs along with your specific crop inputs. In the "Calculations" section you'll be able to calculate your crop revenue, fertilizer cost, labor hours, labor cost, marginal cost, and total seasonal profit. In the "Optimization" section you'll be able to optimize the number of beds per crop to maximize profit while staying within the limits of the farm. Finally, in the "Validation" section you'll be able to validate the formulas used, verify that the results are what you expect them to be, and document any audit findings.



\## Calculation logic

In named-range notation, never cell addresses:



&#x20; LABOR\_HRS(q) = q x HRS\_PER\_BED x WEEKS x (1 + DIM\_PCT)^q



For each crop, calculate seasonal labor hours using the following formulas:



Tomatoes: TOM\_LABOR = TOM\_Q × TOM\_HRS × WEEKS × (1 + TOM\_DIM)^TOM\_Q



Carrots: CAR\_LABOR = CAR\_Q × CAR\_HRS × WEEKS × (1 + CAR\_DIM)^CAR\_Q



Mesclun: MES\_LABOR = MES\_Q × MES\_HRS × WEEKS × (1 + MES\_DIM)^MES\_Q



TOM\_Q, CAR\_Q, and MES\_Q represent the number of beds planted for each crop.



Total labor: TOTAL\_LABOR = TOM\_LABOR + CAR\_LABOR + MES\_LABOR



Total fertilizer cost: TOTAL\_FERT = TOM\_Q × TOM\_FERT + CAR\_Q × CAR\_FERT + MES\_Q × MES\_FERT



Seasonal profit: PROFIT = TOTAL\_REVENUE - TOTAL\_FERT - TOTAL\_LABOR\_COST - FIXED\_COST



\## Conventions



Crop bed allocations must be positive integers.



The farmer's 720 available field hours will be utilized first. Temporary workers may be hired to meet additional labor needs, with a maximum of four workers.



All calculations use unrounded values; rounding is for display only.



\## Validation rules



Optimal crop allocation: 10 tomato beds, 20 carrot beds, and 30 mesclun beds.



Expected seasonal profit: $42,762, within $5.



One tomato bed must require 99 seasonal labor hours, within 0.01 hours.



Standalone price and marginal-cost crossings should occur around 10 tomato beds, 10 carrot beds, and 6 mesclun beds



Run Solver from 2 starting point (0/0/0 and 20/0/0).



Check if all bed and labor constraints are satisfied, all calculated cells contain formulas, and no spreadsheet errors remain.



\## Outputs



OPT\_TOM\_BEDS: Optimal number of tomato beds.



OPT\_CAR\_BEDS: Optimal number of carrot beds.



OPT\_MES\_BEDS: Optimal number of mesclun beds.



TOTAL\_BEDS: Total number of beds planted.



UNUSED\_BEDS: Number of beds left unplanted.



TOTAL\_REVENUE: Total revenue from all crops.



TOTAL\_FERT: Total fertilizer costs.



TOTAL\_LABOR: Total seasonal labor hours.



TOTAL\_LABOR\_COST: Total labor costs.



PROFIT: Total seasonal profit.



BED\_CHECK: Whether the bed constraints are satisfied.



LABOR\_CHECK: Whether the labor constraints are satisfied.



\## Audit findings

Added AFTER the build. For each check: what you checked, what you found, what

you did about it.

