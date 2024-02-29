# Cantonese Bible Speech-To-Text System

## Abstract 
Downloaded audio clips and scraped transcription from an online multilingual Bible corpus. 

Created a 14-hour dataset by force alignment with SpeechBrain and segmentation to clips of 1 to 5 seconds. 

Fine-tuned on a pretrained Cantonese wav2vec model on Hugging Face with the self-created dataset. 

Character error rate on the same test set decreased from 0.48 to 0.28 after fine-tuning. 

## Purpose of the project 
The purpose of this project is to adapt the acoustic model to the unique characteristics of Cantonese speech within the context of religious text. The initial pretrained wav2vec model, having learned representations from a diverse set of audio data, forms a basis for capturing general acoustic patterns. Fine-tuning on the Bible ensures that the model not only understands the nuances of Cantonese pronunciation but also adapts to the specific linguistic and contextual intricacies of the religious content.

## Dataset 
Training data: 20041 pairs of audio and transcription (14h 30min)

Dev data: 1769 pairs (1h 30min)

Test data: 1995 pairs (1h 30min)

We used the Bible New Testament Cantonese dataset we created in Assessment 1, as the training data is of good recording quality, and it is large enough to fine tune a model (14.5 hours) without overfitting. Recordings in the training data and their transcriptions were downloaded from bible.is, while dev and test data are from another website (https://www.wordproject.org/bibles/audio/13_cantonese/index.htm) to avoid speaker overlapping. 


## FineTuning Details 
Pretrained Model: "ctl/wav2vec2-large-xlsr-cantonese" from huggingface 

Architecture: wav2vec 

About the pretrained model: it fine-tuned on facebook/wav2vec2-large-xlsr-53 on Cantonese using the Common Voice zh-HK dataset. 

Baseline: We used the evaluation code provided in the pretrained model official huggingface page to get the baseline. Originally, we thought too much data would cause the Google Colab RAM to crash, so we used the first 1000 pairs of data (there are 1995 pairs in total) for baseline. The baseline CER is 0.476284.

Lowest training loss: 1.5094 

Lowest training CER: 0.3540

Hyperparameters and their values:
training_args = TrainingArguments(
  output_dir = repo_name,
  group_by_length=True,
  per_device_train_batch_size=8,
  gradient_accumulation_steps=2,
  evaluation_strategy="steps",
  num_train_epochs=10,
  fp16=True,
  fp16_backend="amp",
  gradient_checkpointing=True,
  save_steps=400,
  eval_steps=400,
  logging_steps=400,
  learning_rate=1e-4,
  warmup_steps=100,
  save_total_limit=2,
  push_to_hub=True,
)

## Evaluation 
To make it a better comparison between baseline CER and the fine-tuned CER, we also calculated CER on the first 1000 pairs of test dataset. The final CER we got is 0.279798, which should be considered as a significant improvement from the baseline 0.476284. 
