# Domain-Specific Fine-Tuning of Qwen2.5-7B Using LoRA

## Advanced Internship Program on Generative AI

This project was completed as part of the Advanced Internship Program on Generative AI conducted by iHUB-Data.

---

# 1. Project Overview

Large Language Models (LLMs) are trained on broad datasets and are capable of performing a wide variety of tasks. However, a general-purpose model may not provide sufficiently domain-specific responses for specialized applications.

This project explores domain-specific fine-tuning using **Low-Rank Adaptation (LoRA)**.

The selected domain for this experiment was **Indian criminal law**, with a focus on legal questions and answers related to:

- Bharatiya Nyaya Sanhita (BNS), 2023
- Bharatiya Nagarik Suraksha Sanhita (BNSS), 2023
- Bharatiya Sakshya Adhiniyam (BSA), 2023

A Qwen2.5-7B language model was adapted using LoRA and 4-bit quantization with the Unsloth framework.

---

# 2. Objective

The primary objectives of this task were:

1. Understand domain-specific fine-tuning.
2. Understand the concept of Low-Rank Adaptation (LoRA).
3. Prepare a domain-specific dataset for supervised fine-tuning.
4. Fine-tune a pretrained Large Language Model.
5. Evaluate the behavior of the fine-tuned model.
6. Save the resulting LoRA adapter.
7. Document the complete workflow and observations.

---

# 3. Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Google Colab | Training environment |
| PyTorch | Deep learning framework |
| Hugging Face Transformers | Model and tokenizer handling |
| Hugging Face Datasets | Dataset loading and processing |
| TRL | Supervised fine-tuning |
| PEFT | Parameter-efficient fine-tuning |
| Unsloth | Efficient LLM fine-tuning |
| Qwen2.5-7B | Base language model |
| LoRA | Parameter-efficient adaptation |
| 4-bit Quantization | Reduced GPU memory usage |

---

# 4. Base Model

The base model used in this experiment was:

**Qwen2.5-7B**

The model was loaded using Unsloth with 4-bit quantization.

This approach significantly reduces GPU memory requirements compared with loading and training the complete model in full precision.

---

# 5. Why LoRA?

Traditional fine-tuning updates a large number of parameters in the pretrained model.

For a 7-billion-parameter model, updating the complete model requires significant computational resources and GPU memory.

LoRA provides a parameter-efficient alternative.

Instead of updating the original model parameters, LoRA introduces small trainable adapter matrices into selected layers.

In this experiment:

- Total model parameters: **7,655,986,688**
- Trainable parameters: **40,370,176**
- Trainable percentage: **0.53%**

Therefore, the majority of the original model parameters remained frozen.

This makes domain adaptation considerably more resource-efficient.

---

# 6. LoRA Configuration

The following LoRA configuration was used:

| Parameter | Value |
|---|---|
| Rank (`r`) | 16 |
| LoRA Alpha | 16 |
| LoRA Dropout | 0 |
| Bias | None |
| Random State | 3407 |
| Rank Stabilization | Disabled |
| LoftQ | Disabled |

The LoRA adapters were applied to the following model modules:

```text
q_proj
k_proj
v_proj
o_proj
gate_proj
up_proj
down_proj
```
## 7. Training Configuration

The model was fine-tuned using Supervised Fine-Tuning (SFT) with the Unsloth framework on a free Google Colab Tesla T4 GPU.

### Training Parameters

| Parameter | Value |
|---|---|
| Base Model | Qwen2.5-7B |
| Quantization | 4-bit |
| Training Method | LoRA / QLoRA |
| Dataset Size | 6,354 examples |
| Number of Epochs | 1 |
| Batch Size | 2 |
| Gradient Accumulation Steps | 4 |
| Effective Batch Size | 8 |
| Maximum Sequence Length | 2048 |
| Learning Rate | 2 × 10⁻⁴ |
| Warmup Steps | 5 |
| Optimizer | AdamW 8-bit |
| Weight Decay | 0.01 |
| Learning Rate Scheduler | Linear |
| LoRA Rank (r) | 16 |
| LoRA Alpha | 16 |
| Random Seed | 3407 |
| GPU | NVIDIA Tesla T4 |

The effective batch size was calculated as:

**2 × 4 = 8**

where 2 is the batch size per device and 4 is the gradient accumulation step count.

---

## 8. Training Results

The model was successfully fine-tuned for one complete epoch.

### Training Statistics

- **Training examples:** 6,354
- **Total training steps:** 795
- **Training time:** approximately 55.62 minutes
- **GPU:** NVIDIA Tesla T4
- **GPU memory available:** approximately 14.56 GB
- **Peak reserved GPU memory:** approximately 7.98 GB
- **Additional memory used for LoRA training:** approximately 0.74 GB

### Training Loss

The training loss decreased during training:

| Step | Training Loss |
|---:|---:|
| 50 | 1.5422 |
| 100 | 1.1773 |
| 150 | 1.1336 |
| 200 | 1.1283 |
| 250 | 1.1092 |
| 300 | 1.0909 |
| 350 | 1.0857 |
| 400 | 1.0761 |
| 450 | 1.0500 |
| 500 | 1.0605 |
| 550 | 1.0476 |
| 600 | 1.0628 |
| 650 | 1.0497 |
| 700 | 1.0398 |
| 750 | 1.0434 |

The decreasing loss indicates that the LoRA adapters successfully learned patterns from the Indian legal question-answer dataset.

---

## 9. Model Evaluation

After training, the fine-tuned model was tested using questions related to Indian criminal law.

The evaluation focused on whether the model could:

1. Understand questions related to the Bharatiya Nyaya Sanhita (BNS), 2023.
2. Generate answers in a legal question-answer format.
3. Identify relevant sections of the BNS.
4. Produce concise domain-specific responses.
5. Include the legal source/section in its responses.

### Test 1 — Theft

**Question:**

> What is the punishment for theft under the Bharatiya Nyaya Sanhita, 2023?

**Model Response:**

> Theft is punishable by up to 3 years in prison, or a fine, or both. If the stolen property is movable and the offender is caught in possession of it, the offender shall be punished with imprisonment up to 1 year, or a fine, or both. [Source: Section 303, BNS 2023]

---

### Test 2 — Voluntarily Causing Hurt

**Question:**

> What is the punishment for voluntarily causing hurt under the Bharatiya Nyaya Sanhita, 2023?

**Model Response:**

> Causing hurt is punishable by up to one year in prison, or a fine, or both. If the hurt is grievous, the punishment increases to up to three years in prison, or a fine, or both. [Source: Section 115, BNS 2023]

---

### Test 3 — Section 1

**Question:**

> What is the purpose of Section 1 of the Bharatiya Nyaya Sanhita, 2023?

**Model Response:**

> Section 1 of the Bharatiya Nyaya Sanhita, 2023, establishes the fundamental principles of the Indian criminal justice system, including the presumption of innocence, the right to a fair trial, and the prohibition of cruel or degrading punishment. [Source: Section 1, BNS 2023]

---

### Test 4 — Offences Outside India

**Question:**

> Does the Bharatiya Nyaya Sanhita apply to offences committed outside India?

**Model Response:**

> No, the Sanhita does not extend to any offence committed outside India, unless the Central Government has made special provisions for it. [Source: Section 1, BNS 2023]

---

### Test 5 — Indian Computer Resource

**Question:**

> What are the consequences of committing an offence against an Indian computer resource from outside India?

**Model Response:**

> Committing an offence against an Indian computer resource from outside India is punishable by up to seven years in prison and a fine. [Source: Section 249, BNS 2023]

---

## 10. Model Features

The resulting fine-tuned model has the following domain-specific capabilities:

- **Indian Criminal Law Focus:** The model was trained using questions and answers related to Indian criminal law.
- **BNS 2023 Knowledge:** The dataset contains information related to provisions of the Bharatiya Nyaya Sanhita, 2023.
- **Legal Question Answering:** The model can respond to questions concerning criminal-law provisions.
- **Section-Based Responses:** The model attempts to associate answers with relevant legal sections.
- **Concise Responses:** Responses are formatted as direct question-and-answer explanations.
- **Parameter-Efficient Fine-Tuning:** Only the LoRA adapter parameters were trained rather than updating all 7.65 billion model parameters.
- **4-bit Quantization:** Quantization reduced GPU memory requirements and made fine-tuning possible on a Tesla T4.
- **Local Adapter Storage:** The trained LoRA adapter was saved separately and can be used with the base model.

---

## 11. Model Artifacts

The trained LoRA adapter and tokenizer were saved locally after training.

The following files were generated:

```text
lora_model/
├── adapter_config.json
├── adapter_model.safetensors
├── tokenizer.json
└── tokenizer_config.json
```
## 12. Technology Stack

The project was implemented using the following technologies:

- Python
- Google Colab
- PyTorch
- Hugging Face Transformers
- Hugging Face Datasets
- Hugging Face TRL
- Unsloth
- PEFT / LoRA
- Qwen2.5-7B
- CUDA
- NVIDIA Tesla T4
- 4-bit Quantization

---

## 13. Project Workflow

The complete workflow followed in this task was:

```text
Indian Legal QA Dataset
          ↓
Dataset Cleaning & Formatting
          ↓
Alpaca-Style Prompt Formatting
          ↓
Qwen2.5-7B Base Model
          ↓
4-bit Quantization
          ↓
LoRA Adapter Configuration
          ↓
Supervised Fine-Tuning
          ↓
Training for 1 Epoch
          ↓
Model Evaluation
          ↓
LoRA Adapter Saving
          ↓
Domain-Specific Indian Legal QA Model

```

## 14. Advantages of the Approach

### Parameter Efficiency

Instead of updating all parameters of the Qwen2.5-7B model, LoRA updates a much smaller set of trainable parameters.

In this experiment:

- Total model parameters: approximately **7.66 billion**
- Trainable parameters: approximately **40.37 million**
- Percentage trained: approximately **0.53%**

This significantly reduces the computational requirements compared with full model fine-tuning.

### Memory Efficiency

The model was loaded using 4-bit quantization. This allowed the fine-tuning process to run on a free Google Colab Tesla T4 GPU with approximately 14.56 GB of VRAM.

### Reusability

The LoRA adapter can be stored separately from the base model. This makes it possible to reuse the same base model with different domain-specific adapters.

---

## 15. Limitations

Although the fine-tuned model demonstrated domain-specific question-answering capabilities, it has several limitations:

- The model should not be treated as a substitute for a qualified legal professional.
- The model may generate incorrect or incomplete legal information.
- The training dataset covers a specific subset of Indian legal information.
- The evaluation was based on a small set of manually selected questions.
- The model does not perform live legal research or verify whether legislation has subsequently changed.
- Generated legal answers should therefore be independently verified against the current official legislation.

---

## 16. Future Improvements

The project can be further improved by:

1. Increasing the size and diversity of the legal training dataset.
2. Including more areas of Indian law beyond criminal law.
3. Adding validation and test datasets for quantitative evaluation.
4. Comparing the base model and fine-tuned model using the same evaluation questions.
5. Testing different LoRA ranks such as 8, 32, and 64.
6. Experimenting with different learning rates and training epochs.
7. Adding Retrieval-Augmented Generation (RAG) so that answers can reference current legal documents.
8. Evaluating factual accuracy using expert-reviewed legal questions.
9. Deploying the model through a simple web interface or API.
10. Maintaining a versioned dataset to account for changes in Indian legislation.

---

## 17. Conclusion

This project demonstrated the process of domain-specific fine-tuning of a large language model using Low-Rank Adaptation (LoRA).

A Qwen2.5-7B model was loaded using 4-bit quantization and fine-tuned on an Indian legal question-answer dataset containing 6,354 examples. LoRA allowed the model to adapt to the legal domain while training only approximately 0.53% of the model's parameters.

The resulting adapter demonstrated the ability to generate responses to Indian criminal-law questions in a structured format and associate responses with relevant legal sections.

The experiment also demonstrated that parameter-efficient fine-tuning can be performed on limited computational resources such as a free Google Colab Tesla T4 GPU.

> **Note:** This project is an educational demonstration of domain-specific LLM fine-tuning and is not intended to provide professional legal advice.
