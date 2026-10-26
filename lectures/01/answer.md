# Day 1 Homework - Basic

## Method
I used the same prompt for both models:
"What is LoRA? Explain briefly in English."

I ran gemini-3.5-flash-lite three times. I also attempted three runs with gemini-3.8-flash. Raw outputs and the final attempt's exit status are recorded in basic_results.txt. I did not change temperature.

## Results and comparison
All three Flash-Lite runs returned answers. They consistently defined LoRA as Low-Rank Adaptation and explained freezing the base model while training additional parameters. Their wording, structure, and examples varied:
- Run 1 included a notebook-versus-textbook analogy.
- Run 2 emphasized file size and consumer hardware.
- Run 3 used numbered points and claimed savings of up to 90%.

Flash run 1 returned a more technically specific explanation: it named parameter-efficient fine-tuning (PEFT), described a pair of low-rank adapter matrices, and discussed swapping adapters. It did not use the textbook analogy.

Flash run 2 returned a 503 model-busy error. Run 3 was attempted separately with a 20-second time limit; its outcome is recorded in the raw-results file.

## What I learned
Repeated requests can differ in presentation while retaining the same central explanation. In this example, the successful Flash response included more technical terminology and architectural detail.

Service availability also affected the experiment. The 503 response is a failed request, not an answer to compare.

## Limitations
One question and this small number of successful responses cannot establish which model is generally better. Numerical savings and file-size claims were not independently verified. Small adapter files do not replace the need for the base model.

## Setup and assistance
All 11 supplied tests passed. The API key was stored as a Codespaces secret. I used AI assistance for setup, commands, and drafting the report from my outputs.
