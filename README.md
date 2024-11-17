# Expected Loss Modeling

This repository provides a detailed explanation and calculations for **Expected Loss (EL)** using the formula:
Expected Loss (EL) = EAD * PD * LGD

Where:
- **EAD** = Exposure at Default  
- **PD** = Probability of Default  
- **LGD** = Loss Given Default  

---
## 1. Exposure at Default (EAD)
**EAD** represents the total exposure in the event of a default.

### Steps:
1. **Usage Given Default (UGD)**:  
   The percentage of committed but undrawn balance expected to be drawn in default.  
   - **UGD** is determined by the company’s credit rating.

2. **Formula**:  
EAD = Outstanding Bonds + (Unused Commitment * UGD)
- **Outstanding Bonds (Notional)** = 500M  
- **Unused Commitment** = 500M  
- **UGD** = 65% (based on credit rating)

3. **Calculation**:
EAD = 500M + (500M * 0.65) = 825M

---

## 2. Probability of Default (PD)
**PD** is calculated using the **Merton Model**.

### Required Parameters:
- **Firm Value (Assets)** = 19.57M  
- **Expected Return** = 6%  
- **Time Horizon** = 1 year  
- **Volatility** = 44.7% (Historical asset-level volatility)  
- **Short-Term Liabilities (Max)** = 8.38M  
- **Long-Term Liabilities (Max)** = 20.38M  

### Default Point:
The sum of short-term and long-term liabilities that exceeds 12.5M is considered a default.  

### Distance to Default (DD):
The formula for DD is:
DD = [Ln(Firm Value / Default Point) + (Expected Return - (Volatility^2 / 2)) * Time] / (Volatility * sqrt(Time))

### Calculation:
DD = [Ln(19.57 / 12.5) + (0.06 - (0.447^2 / 2)) * 1] / (0.447 * sqrt(1)) DD ≈ 0.975

### Probability of Default:
PD = Normal Distribution(-Distance to Default) PD ≈ 13.85%

---

## 3. Loss Given Default (LGD)
**LGD** represents the proportion of loss in the event of default, calculated using a **Beta Distribution**.  

### Moody's Model:
Using parameters:
- **avg_LGD_on_bonds** = Average Loss Given Default on bonds  
- **std** = Standard Deviation of LGD  
- **max_for_bonds** = Maximum LGD value  

### Formula:
1. Calculate `alpha` and `beta` based on average, standard deviation, and max LGD.
2. Derive `mean_recovery` using Beta Distribution.
3. Compute `LGD` as:
LGD = 1 - mean_recovery

### Example:
LGD = 48.75%

---

## 4. Expected Loss (EL)
The final **EL** is computed as:
EL = (EAD * PD * LGD) / 10,000

### Calculation:
- **EAD** = 825M  
- **PD** = 13.85%  
- **LGD** = 48.75%  

EL = (825 * 13.85 * 48.75) / 10,000 EL ≈ $55,710,091.76

---

## Summary
- **EAD** = 825M  
- **PD** = 13.85%  
- **LGD** = 48.75%  
- **EL** = $55,710,091.76  

---

## References
- Moody's LGD Model  
- Merton Model for PD Estimation  

---
  
