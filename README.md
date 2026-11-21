# DrugRepurposing_MMP2_Docking-MD-Simulation

# Practice 
(Research Project Practice and troubleshooting exercise)

This repository contains a **computational practice project** on **drug repurposing of cephalosporins against MMP-2 (Matrix Metalloproteinase-2)**, a key target in tumor progression and metastasis. 

It documents the workflow — from protein preparation to docking and normal mode analysis — along with results and visualizations.

---

## 🔹 Workflow Overview

### 1. Protein Selection & Preparation
- Target: **MMP-2**  
  - UniProt ID: **P08253**  
  - PDB ID: **7XJO** (catalytic domain, 2.0 Å resolution)  
- Cleaned in Discovery Studio (removed water, ligands, ions, Chain B → kept single Chain A).  
- Refined with **GalaxyRefine** (Model 5 chosen).  
- Validation:  
  - ERRAT score improved from **78 → 95**  
  - PROCHECK Ramachandran: **95.6% residues in favored regions**

### 2. Protein Analysis
- **ProtParam**: Stable (Instability Index = 27.46), acidic pI (5.26), soluble (GRAVY = –0.446).  
- **PSIPRED**: Balanced α-helices and β-sheets, well-defined structure.

### 3. Ligand Selection & Preparation
- Cephalosporins retrieved from **PubChem**:  
  Cefoperazone, Ceftizoxime, Ceftazidime, Cefixime, Cefditoren, Ceftibuten, Cefpodoxime, Cefotaxime.  
- ADME analysis via **SwissADME** (GI absorption, MW, TPSA, Lipinski).  
- Converted: **SDF → PDB → PDBQT** (OpenBabel + AutoDockTools).

### 4. Molecular Docking (AutoDock Vina)
- Binding pocket defined using co-crystallized inhibitor from **7XJO**.  
- Docking performed (single + batch mode).  
- **Docking Scores (kcal/mol):**
  - Cefoperazone: **–7.061** ✅ (best)  
  - Ceftizoxime: –6.996  
  - Ceftazidime: –6.691  
  - Others ranged –5.8 to –6.5  

👉 See docking_scores.csv file for full results.

### 5. Post-docking Analysis
- **Complex formed only with Cefoperazone** (top hit).  
- **PLIP Analysis:**  
  - H-bonds → LEU83, ALA84, ALA86, ALA88  
  - Salt bridges → HIS121, HIS125, HIS131  
  - π–π stacking → PHE87  
- **Visualization:** Complex generated in PyMOL.

### 6. Molecular Dynamics Simulation (iMODS)
- Normal Mode Analysis (NMA) confirmed structural stability of the MMP-2–Cefoperazone complex.  

Plots exported from iMODS:  
- **deformability.png** → deformability of residues  
- **bfactor.png** → normalized B-factor plot  
- **eigenvalue.png** → eigenvalue (stiffness of motion)  
- **covariance.png** → covariance map (correlated/anticorrelated motions)  
- **elastic_network.png** → elastic network model  

---

## 📂 Repository Structure
```
MMP2_DrugRepurposing/
│
├── README.md
├── Docking_Results.docx # Full detailed report
│
├── data/
│   ├── protein/ # Protein files (raw, cleaned, refined, validation)
│   └── ligands/ # Ligands (SDF, PDB, PDBQT, ADME reports)
│
├── docking/
│   ├── config_single.txt # config for single docking
│   ├── config_batch.txt # config for batch docking
│   ├── commands.txt # commands used
│   ├── docking_scores.csv # docking results
│   └── Results/ # Vina outputs
│       ├── out_files/ # .pdbqt
│       ├── logs/ # .txt
│       └── split_poses/ # vina_split outputs
│
└── analysis/
    ├── plip/ # Protein–ligand interaction analysis
    │   ├── MMP2_Cefoperazone_complex.pdb
    │   ├── PLIP_report.xml
    │   └── 2D_Diagram_PLIP.png
    │
    └── imods/ # Molecular dynamics (iMODS)
        ├── index.html
        ├── index2.html
        ├── deformability.png
        ├── bfactor.png
        ├── eigenvalue.png
        ├── covariance.png
        ├── elastic_network.png
        └── model.pdb
```
---

## 🔹 Key Takeaways
- **Cefoperazone** emerged as the strongest binder to MMP-2 (–7.061 kcal/mol).  
- Stable hydrogen bonds, salt bridges, and π–π stacking confirmed via PLIP.  
- **iMODS simulation** validated overall structural stability.  

---

## 🛠 Tools & Servers Used
- **Docking & Prep:** AutoDock Vina, MGLTools (ADT), Discovery Studio, PyMOL, OpenBabel  
- **Protein analysis:** ProtParam, PSIPRED, GalaxyRefine, ERRAT, PROCHECK  
- **Ligand analysis:** SwissADME, PubChem  
- **Interaction analysis:** PLIP, PyMOL  
- **MD simulation:** iMODS

  ---


## 📚 Related Research Publication

This research practice involves drug repurposing analysis on **MMP-2**, using a **different protein ID** than the one used in our published research.  
The workflow here is a **practice and troubleshooting exercise**, while the publication presents the **formal, peer-reviewed analysis** with deeper computational validation.

**Research Article:**  
📄 *“In Silico Discovery of Cefoperazone as a Novel MMP-2 Inhibitor for Ovarian Cancer Therapy”*  
Published in **Scientific Inquiry and Review**

🔗 **Full Text:**  
https://journals.umt.edu.pk/index.php/SIR/article/view/7532  


**Summary of the Publication:**  
- Evaluated eight cephalosporins against **MMP-2**.  
- **Cefoperazone** showed the strongest binding (ΔG = –8.1 kcal/mol).  
- **100-ns MD simulations** validated complex stability.  
- Highlights the potential of **in-silico drug repurposing** in early-stage oncology research.

---

## Feedback
Your **reads, critical feedback, and citations** are greatly appreciated and help amplify the impact of this work. 

---

## ⚖️ License
This repository is shared under the **MIT License** — feel free to use and adapt with proper attribution.
