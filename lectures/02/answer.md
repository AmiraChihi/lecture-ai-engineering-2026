# Session 2 — LoRA fine-tuning

## 演習 / Exercise

I started the Colab notebook, and my run was still in progress when I prepared this write-up. The scores below come from the instructor’s T4 run, following the fallback in Section 4b. AI assisted in reviewing the reference outputs. `executed_training_myself = false` for the results reported here.

The reference used Qwen3.5-0.8B with LoRA, 20 epochs, rank 16, learning rate 0.0002 and seed 42.

| Metric on 21 questions | Before training | After training |
|---|---:|---:|
| Format rate | 2/21 (9.5%) | 21/21 (100%) |
| Content rate | 0/21 (0.0%) | 19/21 (90.5%) |

No regressions were recorded. No question passed both checks before training. The two remaining failures were questions about when grades would be released and whether office hours required a reservation. The FAQ covered neither detail, but the tuned model answered both with `needs_review: false`.

In Section 6, all four answers started with a format error. After tuning, the model requested verification for the instructor’s name and the next lecture topic. It gave the FAQ deadline for the ordinary assignment, which the FAQ supports. It also reused that date for the final assignment, whose deadline was absent from the FAQ. That distinction helped me see how an answer can look consistent while applying the wrong fact.

[Instructor’s reference outputs](https://github.com/matsuolab/lecture-ai-engineering-2026/tree/main/lectures/02/reference)

## 宿題 / Homework

**Level:** Basic. The planned comparison changes only `num_train_epochs` from 20 to 10, using the same model, data and evaluation questions. The 10-epoch run and the comparison of final logged loss and training time are pending.

**Reflection.** I would use fine-tuning when I need a model to produce a consistent response format, such as a JSON answer with a `needs_review` field. In this exercise, every tuned answer passed the format check, but two still gave confident answers without support. For information that can change, such as a deadline, I would retrieve the current source and evaluate whether the model asks for verification when the source does not answer the question.
