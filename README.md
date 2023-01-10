# DetIE-with-DeBERTaV3

This repository contains the measurements and the paper (written in German for [Jugend forscht](https://www.jugend-forscht.de/)) for replacing the BERT-encoder inside the [DetIE](https://arxiv.org/abs/2206.12514) model with the more effective encoders RoBERTa, ELECTRA, DeBERTa and DeBERTaV3. RoBERTa and ELECTRA improved the results for DetIE significantly for multiple benchmarks and train datasets and provided new state of the art performances for half of the benchmarks while not slowing down extraction speed.

As the used code is similar to the original code in the [DetIE repo(https://github.com/sberbank-ai/DetIE)], only the results are published.
However, the corresponding German research paper is included as well as this work sets the new state of the art in the area of OIE by simply using newer BERT encoder variants. 

However, DeBERTa and DeBERTaV3 models were found to be harshly worsening the model performance as their pre-trained relative attention does hinder the decoder to predict  even one extraction most of the time. It is hypothesized that the relative embedding of DeBERTa pre-trained on classical NLP data cannot include meaningful relative position information on OIE task as it does for DetIE's grid token classification task. Instead it would add wrong information that impaires DetIE.

It was carefully proofed that no incorrect implementation, not the freezing of the 8 bottom encoder layers and not the grid prediction task of DetIE would cause this problem in combination with DeBERTa or DeBERTaV3. DetIE models with DeBERTa encoders were trained with no frozen layers and only 1 and also 5 simoultaneously predicted extraction token labels. Still models with DeBERTa nealy never yield any extractions, which led to the stated hypothesis.





