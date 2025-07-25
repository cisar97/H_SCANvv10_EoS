# Hydrogen Equation of State – H_SCANvv10_EoS.txt

This repository contains tabulated data for the **Equation of State (EoS) of Hydrogen** as computed and used in:

**C. Cozza, K. Nakano, S. Howard, H. Xie, R. Helled, and G. Mazzola. _A denser hydrogen inferred from first-principles simulations challenges Jupiter’s interior models_. arXiv:2501.12925, 2025.**  
[arXiv:2501.12925](https://arxiv.org/abs/2501.12925)

---

## 📄 Description

### `H_SCANvv10_EoS.txt`

This file provides a tabulated Hydrogen EoS over a **regular grid in Temperature and Pressure**, suitable for use in planetary interior modeling and related simulations.

- **Temperature range**: 150 K to 50000 K   (149 points)  
- **Pressure range**: 10⁻⁴ GPa to 10695 GPa  (349 points)

The data file consists of 5 columns:

1. **Temperature** [K]  
2. **log₁₀(Pressure)** [GPa]  
3. **log₁₀(Density)** [g/cm³]  
4. **log₁₀(Internal Energy)** [MJ/kg]  
5. **Entropy** [MJ/kg/K]

As shown in **Figure 6** of the paper, the `H_SCAN+vv10_EoS.txt` table is built from multiple sources:

- On the **low-pressure** side (150–11000 K, 10⁻⁴–0.1 g/cm³): SCvH data  
- In the **intermediate regime** (2000–15000 K, 0.3–2.6 g/cm³): SCAN+vv10 data  
- At **high densities** (> 3.4 g/cm³) and **high temperatures** (> 23000 K): CMS19 data  
- All remaining regions: interpolation between the above datasets

---

### `H_SCANvv10_MD.txt`

This file contains raw Molecular Dynamics results computed using the **SCAN+vv10** functional. It includes **total energies and pressures** (both electronic and ionic components) for selected state points.

The file consists of 6 columns:

1. **Temperature** [K]  
2. **Density** [g/cm³]  
3. **Energy per atom** [Ry]  
4. **Pressure** [GPa]  
5. **Statistical error (Energy)** [Ry]  
6. **Statistical error (Pressure)** [GPa]

These values were used to construct part of the SCAN+vv10 contribution to the full equation of state described above.
As shown in Fig.6 of the paper we performed 126 Molecular Dynamics on a regular grid of 7 Tempertures from 2000 to 15000K and 18 Densities from 0.3 to 2.6 g/cm^3.  


---

## ⚠️ Notes

- The EoS table is **rectangular in T-P space**, but **not all thermodynamic quantities are available at every point**.
- In regions where the density, internal energy, and entropy are **not physically meaningful or relevant** (e.g., **very high T and low P**, or **very low T and high P**), these columns contain the string `'NaN'`. For a clearer view of teh shape of the EoS we again refer to Fig. 6 of the paper.

---

## 📘 Usage

This dataset is intended for researchers modeling planetary interiors or conducting thermodynamic simulations of hydrogen under extreme conditions. 
To read the read the dataset using `pandas` use the following code snippet to delete the `'NaN'` values and convert all the data to floats" 
```python
import pandas as pd

df = pd.read_csv('H_SCANvv10_EoS.txt', sep=' ')

# Remove rows containing NaN (as string or real NaN)
df = df.replace('NaN', pd.NA)
df = df.dropna()

# Convert columns to float for plotting
df['T(K)'] = df['T(K)'].astype(float)
df['logP(GPa)'] = df['logP(GPa)'].astype(float)
df['logrho(g/cm^3)'] = df['logrho(g/cm^3)'].astype(float)
df['logE(MJ/kg)'] = df['logE(MJ/kg)'].astype(float)
df['S(MJ/kg/K)'] = df['S(MJ/kg/K)'].astype(float)
```

---

## 📜 License

This dataset is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).  
You are free to use, modify, and redistribute the data as long as you provide proper attribution.

---

## 📚 Citation

If you use this dataset in your work, please cite:

**C. Cozza, K. Nakano, S. Howard, H. Xie, R. Helled, and G. Mazzola. _A denser hydrogen inferred from first-principles simulations challenges Jupiter’s interior models_. arXiv:2501.12925, 2025.**  
[arXiv:2501.12925](https://arxiv.org/abs/2501.12925)


