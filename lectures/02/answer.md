# Session 2 — LoRA fine-tuning

## 演習 / Exercise

I ran the notebook myself in Google Colab on a Tesla T4 (`executed_training_myself = true`). I used Qwen3.5-0.8B with unquantized LoRA, seed 42, rank 16, and a learning rate of 0.0002.

| Metric on the same 21 questions | Before training | After the original 20-epoch run |
|---|---:|---:|
| Format rate | 2/21 (9.5%) | 21/21 (100%) |
| Content rate | 0/21 (0.0%) | 19/21 (90.5%) |

The notebook reported no regressions. No answer passed both checks before training. After training, the two remaining errors were questions about when grades would be released and whether office hours required a reservation. Both answers used valid JSON but set `needs_review` to `false` even though the FAQ did not provide those details.

In Section 6, all four responses had format errors before training. After training, the model asked for verification about the instructor's name and the next lecture topic. It correctly gave the ordinary assignment deadline, but it reused that date for the final assignment, whose deadline was absent from the FAQ.

## 宿題 / Basic homework

I changed only `num_train_epochs` from 20 to 5. Both runs used the same base model, seed, LoRA settings, data, and evaluation questions. The before-training format and content scores matched across the two runs.

| Metric | Original run (20 epochs) | Modified run (5 epochs) |
|---|---:|---:|
| Post-training format rate | 21/21 (100%) | 21/21 (100%) |
| Post-training content rate | 19/21 (90.5%) | 16/21 (76.2%) |
| Final logged training loss | 0.013774 (step 40) | 1.572838 (step 10) |
| Training time | 234 seconds | 58 seconds |

The 5-epoch run saved 176 seconds of training time (about 75%) and still produced valid JSON for all 21 questions. It passed three fewer content checks overall. It handled both questions the 20-epoch run missed, but it asked for verification on two questions the FAQ could answer, gave an unsupported answer on another question, and missed the required verification wording on two more. The final logged losses cover different parts of training, so I used the same 21-question evaluation to compare the models' responses.

I would use fine-tuning when I need consistent behavior, such as returning a structured answer with a field for human review. For facts that change, such as course deadlines, I would give the model the current source and test whether it asks for verification when the source lacks an answer. Both runs achieved perfect formatting on this exercise, yet both still made content errors.

