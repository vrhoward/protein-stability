# Aiming to Improve Protein Thermostability with LLMs

## Why do we care about protein stability?

Improving protein stability is critical in the fields of structural biology and molecular biophysics as increased stability enhances functional efficacy, which plays an important role in various biological processes. In the fields of immunology and vaccinology, understanding and predicting mutations that can enhance protein stability can be pivotal in drug development. 

Particularly, discovering stabilizing mutations within antigenic targets can not only stimulate greater immune response, but also increase protein yield and 


<img width="558" alt="Screen Shot 2023-11-29 at 8 16 54 AM" src="https://github.com/vrhoward/protein-stability/assets/107573643/5a049f03-62ba-4e4f-b983-800fab1c89b7">

rapid and efficient vaccine development is vital


## ESM-2

ESM-2 is a transformer protein language model, trained on protein sequence data without label supervision. The model is pretrained on Uniref50 with an unsupervised masked language modeling (MLM) objective, meaning the model is trained to predict amino acids from the surrounding sequence context. This pretraining objective allows ESM-2 to learn generally useful features which can be transferred to downstream prediction tasks.

## Dataset Curation and Model Fine-Tuning

The fine-tuning [dataset]([https://www.rapidnovor.com/identifying-cdrs-antibody-sequencing/](https://huggingface.co/datasets/vrhoward/thermostableProteins/viewer/default/train)) is composed of
1) CoV-S sequences containing experimentally-determined prefusion-stabilizing mutations
2) RSV-F sequences containing experimentally-determined prefusion-stabilizing mutations
3) Other viral glycoprotein sequences containing experimentally-determined prefusion-stabilizing mutations
4) Miscellaneous protein sequences containing mutations experimentally-determined as stabilizing

For fine-tuning, the dataset was shuffled and split into a training set and a testing set. The details of the masking procedure for each sequence follow Devlin et al. 2019:
1) 15% of the amino acids are masked.
2) In 80% of the cases, the masked amino acids are replaced by <mask>.
3) In 10% of the cases, the masked amino acids are replaced by a random amino acid (different) from the one they replace.
4) In the 10% remaining cases, the masked amino acids are left as is.



## Demo


## Critical Analysis
Answer one or more of the following questions: What is the impact of this project? What does it reveal or suggest? What is the next step?

## Additional Resources and Links





