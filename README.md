# AICS-submission-


PROJECT OVERVIEW

This project builds and evaluates a multiclass intrusion detection system (IDS)
to classify network flows from the CIC-IDS2017 Wednesday dataset into five
classes: BENIGN, DoS Hulk, DoS GoldenEye, DoS slowloris, and DoS Slowhttptest.

Two models are trained and compared:
  - LightGBM (primary model)   — macro F1 = 0.9951 on 175,488 test flows
  - MLP / Neural Network (comparison) — macro F1 = 0.9883 on 175,488 test flows


REPOSITORY CONTENTS

The submission zip contains:

  IDS_CIC2017_Report.ipynb       — Main coursework report (read this first)
  Source Code.ipynb              — Full training pipeline with all code and outputs
  Trained Models Demo.ipynb      — Quick demo loading pre-trained models
  models/
      lgbm_dos_classifier.pkl    — Saved LightGBM pipeline (includes scaler)
      mlp_dos_classifier.pkl     — Saved MLP pipeline (includes StandardScaler)
      label_encoder.pkl          — Fitted LabelEncoder for class names
  README.txt                     — This file

The cleaned dataset is NOT included in the zip (47 MB). Download it from:
  https://github.com/nasrinpnazar/AICS-submission-2141045
  File: wednesday_cleaned.csv.gz

Place wednesday_cleaned.csv.gz in the SAME folder as the notebooks before
running any cells.


ENVIRONMENT REQUIREMENTS

Python 3.9 or higher is recommended.

Install all dependencies with:

    pip install lightgbm scikit-learn pandas numpy matplotlib seaborn joblib

Exact versions used during development:
    lightgbm       >= 3.3
    scikit-learn   >= 1.1
    pandas         >= 1.5
    numpy          >= 1.23
    matplotlib     >= 3.6
    seaborn        >= 0.12
    joblib         >= 1.2


HOW TO RUN 
View results only (fastest — ~1 minute)

1. Download wednesday_cleaned.csv.gz from GitHub and place in the same folder
2. Open Trained Models Demo.ipynb
3. Run ALL cells top to bottom (Kernel > Restart & Run All)
   This loads the saved pkl models and reproduces all metrics on the test set.
   No training is required.

--------------------------------------------------------------------------------
IMPORTANT NOTES FOR THE MARKER
--------------------------------------------------------------------------------
1. RANDOM SEED: All splits use SEED=42 and stratified sampling. Running the
   code in any order will reproduce identical train/test splits and results.

2. PRE-SAVED OUTPUTS: All code cells in the Report notebook have pre-saved
   outputs. The report can be read end-to-end without executing any cells.

3. MODELS FOLDER: The models/ folder must remain in the same directory as the
   notebooks. The pkl files are large (~70 MB for LightGBM) and contain the
   full fitted pipeline including any preprocessing steps.

4. WORD COUNT: The report targets 4,000 words (+10% buffer = 4,400). A word
   count checker cell is included near the top of the Report notebook. Tables,
   figures, references, the TOC, and the AI Declaration appendix are excluded
   from the count per the brief guidelines.

5. DATASET NOTE: The raw CIC-IDS2017 Wednesday CSV (692,703 rows) is not
   included. wednesday_cleaned.csv.gz (584,959 rows, 62 features) is the
   output of the cleaning pipeline documented in Source Code.ipynb Section 1
   and Report Section 2.2. It is available on GitHub as noted above.

6. AI DECLARATION: See the Appendix at the end of IDS_CIC2017_Report.ipynb
   for a full description of AI tool use, list of prompts, and critical
   assessment of AI-generated content, as required by the brief.

--------------------------------------------------------------------------------
RESULTS SUMMARY
--------------------------------------------------------------------------------
Test set: 175,488 flows (30% stratified hold-out, SEED=42)

  Model         Accuracy    Macro F1    Macro Prec.  Macro Recall
  LightGBM      0.9994      0.9951      0.9929       0.9974
  MLP           0.9954      0.9883      0.9875       0.9892

Majority-class baseline (always predict BENIGN):
  Accuracy = 0.6691   Macro F1 = 0.2000

LightGBM improvement over baseline: +0.7951 macro F1

