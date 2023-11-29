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

The training procedure and loss values can be found in the [model card](https://huggingface.co/vrhoward/esm2_t12_35M_UR50D-finetuned).

The perplexity of the model was measured at the beginning and at the end of the fine-tuning procedure. A lower perplexity score means a better language model, and we achieved a large reduction in perplexity after fine-tuning: from 7.83 to 1.77. This reduction tells us the model has learned something about the domain of thermostable proteins.

## Demo

The fine-tuned model can be demoed in multiple ways:
1) Inference via a [Jupyter Notebook](https://github.com/vrhoward/protein-stability/blob/main/demonstration.ipynb).
2) A user-friendly [HuggingFace Space](https://huggingface.co/spaces/vrhoward/protfill) powered by Gradio.
3) The on-demand Inference API available in the [model card](https://huggingface.co/vrhoward/esm2_t12_35M_UR50D-finetuned).

## Critical Analysis
Answer one or more of the following questions: What is the impact of this project? What does it reveal or suggest? What is the next step?

## Additional Resources and Links

**1) Stabilizing mutations and the COVID-19 Vaccine:** Ching-Lin Hsieh et al., Structure-based design of prefusion-stabilized SARS-CoV-2 spikes. Science 369, 1501-1505(2020). DOI:10.1126/science.abd0826

**2) The GitHub repository for the ESM suite of models:** https://github.com/facebookresearch/esm

**3) Masked Language Modeling Procedure, inspired by BERT:** Devlin, Jacob et al. “BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.” North American Chapter of the Association for Computational Linguistics (2019).

**4) Read more on choosing perplexty for masked language modelling:** https://huggingface.co/learn/nlp-course/chapter7/3?fw=pt







