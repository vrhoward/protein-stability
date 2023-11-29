# Aiming to Improve Protein Thermostability with LLMs

## Why do we care about protein stability?

Protein stability is a critical aspect of protein biology as it plays an important role in structure-function relationships. In the fields of structural biology and molecular biophysics, understanding the mutations that contribute to protein stability can provide insights into protein folding and functional efficacy. This knowledge is crucial for rational protein design, where proteins are engineered for specific functions. This concept extends into the fields of immunology and vaccinology, where stability is a key factor in the development of therapeutic proteins or vaccines: more stable proteins can withstand various physiological conditions, have longer shelf-lives, and may elicit a more robust immune response.

A common strategy in vaccine development against viral antigens involves stabilization of the prefusion conformation of the viral glycoprotein. These proteins, such as the spike (S) protein in SARS-CoV-2 (shown below), exist in a metastable prefusion conformation prior to contact with host-cell surface receptors. Upon binding to host receptors, the glycoprotein enters the postfusion conformation to facilitate viral-host membrane fusion and subsequent viral entry. It has thus become increasingly important to design prefusion-stabilized glycoprotein complexes for vaccines, allowing hosts to develop immune defense against the viruses before infection.

<img width="558" alt="Screen Shot 2023-11-29 at 8 16 54 AM" src="https://github.com/vrhoward/protein-stability/assets/107573643/5a049f03-62ba-4e4f-b983-800fab1c89b7">

Figure adopted from [Hsieh et al.](https://www.science.org/doi/10.1126/science.abd0826).

Despite the obvious importance of these efforts, the discovery of stabilizing mutations remains a time-consuming process. In light of recent global events, rapid and efficient vaccine development is vital. Here, we seek to leverage the power of transformer models to identify useful mutations and advance vaccine development.

## Base model: ESM-2

ESM-2 is a transformer protein language model, trained on protein sequence data without label supervision. The model is pretrained on Uniref50 with an unsupervised masked language modeling (MLM) objective, meaning the model is trained to predict amino acids from the surrounding sequence context. This pretraining objective allows ESM-2 to learn generally useful features which can be transferred to downstream prediction tasks.

## Dataset Curation and Model Fine-Tuning

The fine-tuning [dataset](https://huggingface.co/datasets/vrhoward/thermostableProteins/viewer/default/train) is composed of
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

**Benefits**
1) This work has introduced a freshly curated dataset for protein stability, including viral glycoproteins.
2) The results of this work have the potential to greatly impact the fields of structural biology and vaccinology through the introduction of a new method for rapid protein stabilization design.

**Limitations**
1) The model does not provide insight as to which amino acids should be mutated. However, researchers can rely on structure prediction tools, such as AlphaFold, to determine potentially useful sequence positions.
2) Experimental work must still be conducted in order to determine whether or not the recommended mutations will work to stabilize the protein structure.

**Future Steps**
1) Continue to curate the dataset of thermostable protein sequences, particularly for viral proteins.
2) Train the larger model versions (650M parameters vs. 35M)
3) Add functionality to determine stabilizing mutation *groups*.

## Additional Resources and Links

**1) Stabilizing mutations and the COVID-19 Vaccine:** Ching-Lin Hsieh et al., Structure-based design of prefusion-stabilized SARS-CoV-2 spikes. Science 369, 1501-1505(2020). DOI:10.1126/science.abd0826

**2) The GitHub repository for the ESM suite of models:** https://github.com/facebookresearch/esm

**3) Masked Language Modeling Procedure, inspired by BERT:** Devlin, Jacob et al. “BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.” North American Chapter of the Association for Computational Linguistics (2019).

**4) Read more on choosing perplexity as a masked language modelling metric:** https://huggingface.co/learn/nlp-course/chapter7/3?fw=pt

**5) Use tools like AlphaFold to determine useful positions:** Jumper, J., Evans, R., Pritzel, A. et al. Highly accurate protein structure prediction with AlphaFold. Nature 596, 583–589 (2021). https://doi.org/10.1038/s41586-021-03819-2

## Video Recording

https://github.com/vrhoward/protein-stability/assets/107573643/a6104405-23cc-4fec-8656-356cdd6d5dcd







