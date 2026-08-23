# Training and Evaluation Results

## Training Configuration

| Parameter | Value |
|---|---|
| Base Model | Qwen2.5-7B |
| Fine-Tuning Method | LoRA |
| Quantization | 4-bit |
| GPU | NVIDIA Tesla T4 |
| Dataset Size | 6,354 examples |
| Epochs | 1 |
| Training Steps | 795 |
| Batch Size | 2 |
| Gradient Accumulation Steps | 4 |
| Effective Batch Size | 8 |
| LoRA Rank (r) | 16 |
| LoRA Alpha | 16 |
| Learning Rate | 2 × 10⁻⁴ |
| Trainable Parameters | 40,370,176 |
| Total Parameters | 7,655,986,688 |
| Trainable Parameters | 0.53% |

## Training Performance

The model was successfully fine-tuned for one complete epoch on the Indian legal question-answer dataset.

### Training Loss

| Step | Training Loss |
|---:|---:|
| 50 | 1.542210 |
| 100 | 1.177329 |
| 150 | 1.133592 |
| 200 | 1.128271 |
| 250 | 1.109231 |
| 300 | 1.090912 |
| 350 | 1.085709 |
| 400 | 1.076054 |
| 450 | 1.049952 |
| 500 | 1.060497 |
| 550 | 1.047620 |
| 600 | 1.062775 |
| 650 | 1.049720 |
| 700 | 1.039759 |
| 750 | 1.043431 |

The training loss decreased substantially during training, indicating that the LoRA adapters successfully learned patterns from the domain-specific legal dataset.

## Training Time and GPU Usage

- Training time: **55.62 minutes**
- Peak reserved GPU memory: **7.982 GB**
- GPU memory available: **14.563 GB**
- Peak memory utilization: **54.81%**
- Additional memory used for LoRA training: **0.74 GB**
- Additional training memory: **5.081%**

## Model Testing

After fine-tuning, the model was tested using several questions related to Indian criminal law.

### Test 1 — Theft

**Question:**

What is the punishment for theft under the Bharatiya Nyaya Sanhita, 2023?

**Model Response:**

The model identified the punishment and referenced Section 303 of the BNS 2023.

---

### Test 2 — Voluntarily Causing Hurt

**Question:**

What is the punishment for voluntarily causing hurt under the Bharatiya Nyaya Sanhita, 2023?

**Model Response:**

The model provided a response concerning the punishment for causing hurt and referenced Section 115 of the BNS 2023.

---

### Test 3 — Section 1

**Question:**

What is the purpose of Section 1 of the Bharatiya Nyaya Sanhita, 2023?

**Model Response:**

The model generated a response concerning Section 1 of the BNS 2023 and included a legal section reference.

---

### Test 4 — Offences Outside India

**Question:**

Does the Bharatiya Nyaya Sanhita apply to offences committed outside India?

**Model Response:**

The model generated a response addressing the territorial applicability of the BNS and referenced Section 1.

---

### Test 5 — Indian Computer Resource

**Question:**

What are the consequences of committing an offence against an Indian computer resource from outside India?

**Model Response:**

The model generated a response concerning offences targeting Indian computer resources from outside India and provided a relevant legal section reference.

## Observations

The fine-tuned model demonstrated the ability to:

- Answer questions in the Indian criminal-law domain.
- Follow a legal question-answer format.
- Reference relevant BNS sections.
- Produce domain-specific responses.
- Adapt the general-purpose Qwen2.5-7B model toward the legal QA dataset.

## Conclusion

The experiment successfully demonstrated domain-specific fine-tuning of a large language model using LoRA.

Instead of updating all model parameters, only approximately **0.53% of the model parameters were trained**, significantly reducing the computational requirements while adapting the model to Indian legal question-answering.

The trained LoRA adapter was successfully saved locally for further use.
