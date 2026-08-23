# Task 2 — Domain-Specific Fine-Tuning using LoRA

This task was completed as part of the Advanced Internship Program on Generative AI conducted by iHUB-Data.

## Objective

The objective of this task was to understand and implement domain-specific fine-tuning of a Large Language Model using Low-Rank Adaptation (LoRA).

## Domain

Indian Criminal Law

## Base Model

Qwen2.5-7B

## Fine-Tuning Method

LoRA with 4-bit quantization using Unsloth.

## Dataset

Indian Legal Question-Answer dataset based on:

- Bharatiya Nyaya Sanhita (BNS)
- Bharatiya Nagarik Suraksha Sanhita (BNSS)
- Bharatiya Sakshya Adhiniyam (BSA)

## Work Completed

- Loaded a quantized Qwen2.5-7B model.
- Applied LoRA adapters.
- Prepared the legal question-answer dataset.
- Fine-tuned the model using supervised fine-tuning.
- Evaluated the fine-tuned model using sample legal questions.
- Saved the trained LoRA adapter.
- Generated inference outputs.

Detailed documentation and results will be added.
