# DetIE-with-ELECTRA

This repository contains the measurements and the paper (written in German for [Jugend forscht](https://www.jugend-forscht.de/)) for replacing the BERT-encoder inside the [DetIE](https://arxiv.org/abs/2206.12514) model with the more effective encoders RoBERTa, ELECTRA, DeBERTa and DeBERTaV3. RoBERTa and ELECTRA improved the results for DetIE significantly for multiple benchmarks and train datasets and provide new state of the art performances for half of the benchmarks while not slowing down the extraction speed:

![IMoJIE_tests](https://user-images.githubusercontent.com/60894149/211881793-ed820c0a-b338-4017-8299-d7d43e313edd.png)

---

Another interesting discovery while applying these encoders include the factors of the ease of the task which is determined by the IGL-CA component and the amount of traning data. With it, it could be observed that significant improvements were made for DetIE models with ELECTRA encoders which did not have either to simple tasks or the inability to learn complex hypotactic sentences due to a lack of training data.

This explains why DetIE trained with an IMoJIE dataset and an ELECTRA encoder achieves on average 1.0 F1 and 1.3 AUC more than the precious DetIE model and also only minor improvements are made with an IGL-CA component as it makes the task easier by splitting up every input sentence on conjunction structures.

In contrary, this also explains why DetIE trained with the LSOIE dataset, an ELECTRA encoder and an IGL-CA achieves on average 1.1 F1 and 1.3 AUC more then before as only then the OIE task is comprehensible enough to apply the better language understanding of the ELECTRA encoder. Without an IGL-CA for LSOIE-trained models, only minor improvements are made.

---


As the used code is similar to the original code in the [DetIE repo](https://github.com/sberbank-ai/DetIE), only the results are published.
However, the corresponding German research paper is included as well as this work sets the new state of the art in the area of OIE by simply using newer BERT encoder variants. 

---

The end results results compared to all recent OIE models look as follows:

![table_comparison_to_all_oie_models](https://user-images.githubusercontent.com/60894149/211881404-ca23e882-9258-47f6-9641-b2b5875ee793.png)

---

DeBERTa and DeBERTaV3 models were found to be harshly worsening the model performance but only due to their sharing of the relative embedding matrices across all encoder layers. I am looking forward to update this repository with measurements of the DeBERTa encoders.
