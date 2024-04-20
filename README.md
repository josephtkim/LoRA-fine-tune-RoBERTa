# Finetuning RoBERTa with LoRA

### Introduction
This notebook goes over how to add LoRA layers into the RoBERTa base model and then finetune it on the Yelp Reviews polarity dataset. 

LoRA (Low-Rank Adaption) is a PEFT (Parameter Efficient Fine Tuning) technique to fine-tune models while reducing the required amount of resources such as memory.

LoRA Paper: https://arxiv.org/abs/2106.09685
RoBERTa base model: https://huggingface.co/FacebookAI/roberta-base
Dataset: https://huggingface.co/datasets/yelp_polarity

### Settings
lora rank: 16
lora alpha: 32
batch size: 16
learning rate: 1e-5
epochs: 3
optimizer: Adam
loss function: Cross entropy

LoRA layers were only added to the Query and Value vectors in the Attention layers.

### Results
|   |         | RoBERTa base <br> Fine-tune |  RoBERTa base <br> LoRA |
|---|------------------------|----------------|--------------------------|
|   | # of Trainable Params  | 125M | 0.59M |
|   | Average Training Time <br>per Epoch (mm:ss) | 22:43 | 17:05 |
|   | Test Accuracy | 97.3 | 96.2 |

LoRA has about 210 times less trainable parameters than the fully fine-tuned model, which greatly reduces the computational costs.

The training time is also 25% faster than the fully fine-tuned model, while only losing on about 1.2% accuracy after 3 epochs. 