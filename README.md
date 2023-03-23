# DetIE-with-ELECTRA

This repository contains the measurements and the paper (written in German for [Jugend forscht](https://www.jugend-forscht.de/)) for replacing the BERT-encoder inside the [DetIE](https://arxiv.org/abs/2206.12514) model with the more effective encoders RoBERTa, ELECTRA. RoBERTa and ELECTRA improved the results for DetIE significantly for multiple benchmarks and train datasets and provide new state of the art performances for half of the benchmarks while not slowing down the extraction speed:

![IMoJIE_tests](https://user-images.githubusercontent.com/60894149/211881793-ed820c0a-b338-4017-8299-d7d43e313edd.png)

---

Two important criterias were identified that must be fullfilled to achieve an increased model performance: The language task must be complex enough while there must be also enough train data to adapt the model to the complex task.

This explains why DetIE trained with an IMoJIE dataset (90.000 samples) and an ELECTRA encoder achieves on average 1.0 F1 and 1.3 AUC improvement without an IGL-CA component but close to no improvements with the IGL-CA component, as it simplifies the task by splitting long sentences on coordination structures.

Conversely, DetIE trained with a LSOIE dataset (35.000 samples) and an ELECTRA encoder without an IGL-CA component achieves close to no improvements while it achives
on average 1.1 F1 and 1.3 AUC improvement with an IGL-CA component that simplifies the input sentences enough allowing the encoders to leverage their language understanding skills when trained with limited training data.

---

As the used code is similar to the original code in the [DetIE repo](https://github.com/sberbank-ai/DetIE), mainly the results are published.
However, the corresponding German research paper is included as well as the main model file and the changed DeBERTa model scripts of a custom [Transformers](https://github.com/huggingface/transformers) version.

---

The end results results compared to all recent OIE models look as follows:

![table_comparison_to_all_oie_models](https://user-images.githubusercontent.com/60894149/211881404-ca23e882-9258-47f6-9641-b2b5875ee793.png)

---

DeBERTa and DeBERTaV3 encoders were found to be not appliable inside the area of open information extraction, as they do not include the needed absolute position embeddings and instead feature a relative position embedding for the input tokens.

# Outlook for the Future

DeBERTa models cannot include any form of absolute position embeddings without disrupting the language processing. Hence, future research for including absolute position embeddings would require a costly pre-training of the DeBERTa models with up to 64 V100 Tesla GPUs.

As these requirements will likely be not fullfillable any time soon, the research inside this repository is halted for now but the idea for potential research are shared below.

## Making DeBERTa models appliable for OIE

A simple concept for solving the issue of missing absolute position embeddings is just to include it at the start and pre-train the model again also with the disentangled attention which would likely complement the absolute position information well, so that even improvements inside the area of NLP can be expected. 

So trying to add the small change of an additional absolute positon embedding would likely profit both the areas of NLP and OIE with improvements or a with new theory on how to handle both types of relative and absolute position embeddings together for processing languages.
