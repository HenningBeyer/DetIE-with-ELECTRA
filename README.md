# DetIE-with-ELECTRA

This repository contains the measurements and the paper (written in German for [Jugend forscht](https://www.jugend-forscht.de/)) for replacing the BERT-encoder inside the [DetIE](https://arxiv.org/abs/2206.12514) model with the more effective encoders RoBERTa, ELECTRA, DeBERTa and DeBERTaV3. RoBERTa and ELECTRA improved the results for DetIE significantly for multiple benchmarks and train datasets and provide new state of the art performances for half of the benchmarks while not slowing down the extraction speed:

![IMoJIE_tests](https://user-images.githubusercontent.com/60894149/211881793-ed820c0a-b338-4017-8299-d7d43e313edd.png)

---

Two important criterias were identified that must be fullfilled to achieve an increased model performance: The language task must be complex enough while there must be also enough train data to adapt the model to the complex task.

This explains why DetIE trained with an IMoJIE dataset (90.000 samples) and an ELECTRA encoder achieves on average 1.0 F1 and 1.3 AUC improvement without an IGL-CA component but close to no improvements with the IGL-CA component, as it simplifies the task by splitting long sentences on coordination structures.

Conversely, DetIE trained with a LSOIE dataset (35.000 samples) and an ELECTRA encoder without an IGL-CA component achieves close to no improvements while it achives
on average 1.1 F1 and 1.3 AUC improvement with an IGL-CA component that simplifies the input sentences enough allowing the encoders to leverage their language understanding skills.

---

As the used code is similar to the original code in the [DetIE repo](https://github.com/sberbank-ai/DetIE), mainly the results are published.
However, the corresponding German research paper is included as well as the main model file and the changed DeBERTa model scripts of a custom [Transformers](https://github.com/huggingface/transformers) version.

---

The end results results compared to all recent OIE models look as follows:

![table_comparison_to_all_oie_models](https://user-images.githubusercontent.com/60894149/211881404-ca23e882-9258-47f6-9641-b2b5875ee793.png)

---

DeBERTa and DeBERTaV3 encoders were found to be not appliable inside the area of open information extraction, as they do not include the highly needed absolute position embeddings and instead feature a relative position embedding for the input tokens. 

Including these absolute embeddings additionally at the start, before the unfrozen DetIE encoder layers or after the encoder did not change the outcome of the model being unable to extract a sufficient amount of correct extractions. Obviously, an absolute position embedding must be inserted in the first encoder layer to be processed deeply enough alongside the token embeddings which would only be possible with models that were pre-trained on absolute position embeddings.

An error in the own implementation seems unlikely as the NLP pipeline of the DetIE repository code works flexible for all of the encoders and their components: The model input was checked to be correct whereas the printed output probabilities did indicate that the model internals would produce incorrect extractions with this correct input format. Multiple configurations with separate relative embedding matrices for the 8 frozen and 4 unfrozen encoder layers were tried for the DeBERTa encoders which is visible in the deberta scripts (marked with #hbeyer).



