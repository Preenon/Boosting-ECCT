# Boosting-ECCT
Contains the Google Colab notebooks used as the experimental pipeline for the project “Boosting the Transformer Decoder for LDPC and Polar Codes.” The project adapts four training methodologies: uncorrected-vector boosting, block-wise scheduling, dynamic weight sharing, and importance-sampling–based data augmentation—to the Error-Correcting Code Transformer (ECCT) and evaluates their effect on code performance via plotting BERs and FERs for given SNR ranges. Please feel free to reach out and file issues or submit pull requests and even fork it if you detect implementation errors or wish to improve on it. 

![alt text](https://github.com/Preenon/Boosting-ECCT/blob/main/Results/plots/LDPC_summary_BER.png)
![alt text](https://github.com/Preenon/Boosting-ECCT/blob/main/Results/plots/POLAR_summary_BER.png)

## Contents
boosted_ECCT_training_notebook.ipynb:
Trains baseline ECCT models using the official ECCT implementation.

boosted_ECCT_boosting_notebook.ipynb:
Loads trained models, applies selected boosting methodologies, and performs BER evaluations.

results/:
Contains sample boosted models and BER plots from the paper.

## Execution Environment
The full pipeline was executed in Google Colab using:

GPU: NVIDIA T4 (CUDA-enabled)
Python: 3.10+
PyTorch: 2.x
Dependencies: Installed automatically by the notebooks
Each notebook mounts Google Drive so models and results persist across Colab sessions.

## Running the Pipeline
1. Train baseline ECCT models

Open boosted_ECCT_training_notebook.ipynb in Colab and run all cells in order (adjust GDrive paths first if desired).
The notebook will:
-clone the ECCT repository
-train a 6-layer, 32-dimensional ECCT model by default
-save the model to your mounted Google Drive

You may change the model or training hyperparameters in the CONFIG dictionary and the training cell.

2. Boost and evaluate models
Open boosted_ECCT_boosting_notebook.ipynb and run all cells.
This notebook will:
-load the baseline model(s) from Drive (it will automatically select the most recent directory
-perform UC-based boosting, block-wise scheduling, dynamic weight sharing, and data augmentation
-evaluate BER across a configurable Eb/N0 range
-save boosted models and BER plots to Drive

To sweep hyperparameters (epochs_post, target_uc), edit the designated lists in the CONFIG cell.

## Configuration

Key experiment settings (modifiable in the notebooks):
epochs_base — baseline training epochs
epochs_post — post-stage fine-tuning epochs
target_uc — number of uncorrected vectors to collect
uc_snr_db, batch_size, post_batch_size

If doing LDPC and Polar codes, try also changing parameters: code_n, code_k

## Acknowledgements

This project builds on the following works:

Error-Correcting Code Transformer (ECCT)
Y. Leng, D. Burshtein, M. Medard (2022)
Paper: https://arxiv.org/abs/2203.14966
Code: https://github.com/yoniLc/ECCT

Boosting Neural Min-Sum Decoders
H. Gao, J. Wang, X. Ma, X. You (2025)
Paper: https://arxiv.org/abs/2405.13413
ode: https://github.com/ghy1228/LDPC_Error_Floor
