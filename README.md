# Chemprop antibiotic

Broad spectrum antibiotic potential of small molecules

| Description | Input  | Output  | Training Data | Experimental Validation |
| ------- | --- | --- | --- | --- |
| Prediction of the growth inhibition potential of compounds on E.coli _in vitro_ | SMILES | IC50 | 2335 compounds | Yes |

## Source Code
This model has been published in: 

Stokes JM, Yang K, Swanson K, Jin W, Cubillos-Ruiz A, Donghia NM, MacNair CR, French S, Carfrae LA, Bloom-Ackermann Z, Tran VM, Chiappino-Pepe A, Badran AH, Andrews IW, Chory EJ, Church GM, Brown ED, Jaakkola TS, Barzilay R, Collins JJ. A Deep Learning Approach to Antibiotic Discovery. Cell. 2020 Feb 20;180(4):688-702.e13. doi: [10.1016/j.cell.2020.01.021.](https://www.sciencedirect.com/science/article/pii/S0092867420301021) Erratum in: Cell. 2020 Apr 16;181(2):475-483. PMID: 32084340; PMCID: PMC8349178.

* Code: https://github.com/chemprop/chemprop
* Model Checkpoints: http://chemprop.csail.mit.edu/checkpoints

## License and copyright notice
The GPL-v3 license applies to all parts of the repository that are not externally maintained libraries. 
This repository uses the externally maintained library "Chemprop", located at /model and licensed under an [MIT License](https://github.com/ersilia-os/eos4e40/blob/main/model/LICENSE.md)

## Extended description
Based on a simple _E.coli_ growth inhibition assay, the authors trained a model capable of identifying antibiotic potential in compounds structurally divergent from conventional antibiotic drugs. One of the predicted active molecules, Halicin (SU3327), was experimentally validated _in vitro_ and _in vivo_. Halicin is a drug under development as treatment for diabetes.

### Summary
* Predicts **antibiotic activity** of small molecules
* Takes **compound structures** as input
* Trained with **experimental** bioactivity data against _E.coli_
* Based on a dataset of **>2,000** molecules
* Results **validated experimentally**
* Used for **drug repurposing**
* Identified a **novel broad-spectrum** antibiotic
* Published in *Stokes et al., Cell, 2020*: [10.1016/j.cell.2020.01.021](https://www.sciencedirect.com/science/article/pii/S0092867420301021)
* Processed data can be downloaded [here](https://github.com/yangkevin2/coronavirus_data/blob/master/data/ecoli.csv)

### Specifications

* Input: SMILES string (also accepts an InChIKey string or a molecule name string, and converts them to SMILES) 
* Endpoint: _E.coli_ growth inhibition at 50 uM (0: inactive, 1: active)
* Results interpretation: 
    * 99 initial hits were identified from the Drug Repurposing Hub, with original prediction scores ranging from 0.967 to 0.294, with an  accuracy of 51%.
    * False Negative rate was estimated to be 3.17% (2 of the 63 lowest scoring molecules displayed _E.coli_ growth inhibition potential _in vitro_).
    * The model was fine-tuned using the experimental validation results, correcting for molecules with lower prediction score but high inhibitory activity _in vitro_. All         tested molecules with growth inhibition capacity (OD<sub>600</sub><0.2) were in the 0.8 - 1 range with the adjusted model. Halicin scored 0.92.
    * The WuXi antituberculosis library highest score was 0.37, and, consistently, none of its highest-ranking molecules demonstrated _E.coli_ growth inhibition _in vitro_.
    * Of the 23 selected molecules from the ZINC library (scores > 0.8), 8 displayed activity against at least one of the following: _E.coli, S. aureus, Klebsiella                 pneumoniae, A.baumannii_ and _P. aeruginosa_.

## History

1. Model was downloaded on 28/04/2021 from [Chemprop](http://chemprop.csail.mit.edu/checkpoints) following the direct link.
2. We opened an issue on GitHub [#128](https://github.com/chemprop/chemprop/issues/108#issuecomment-802245616) to be sure about feature scaling.
3. We duplicated `predict.py` and `scripts/save_features.py` scripts from chemprop GitHub repository.
4. Model was incorporated to Ersilia on 28/04/2021.
