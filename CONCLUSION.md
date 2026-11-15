# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

I think Layer 1 made the biggest difference in my experiment. Without any protection, the agent answered 16 out of 24 questions correctly, gave 4 wrong answers, and left 4 unanswered. After adding Layer 1, the results changed to 18 correct, 6 wrong, and 0 unanswered.

I expected this layer to help because it allows the model to see tool errors and try again instead of stopping immediately. The results showed that the agent became better at completing questions, especially when it had problems with tool arguments or region names. However, I was surprised that the number of wrong answers also increased.

Layer 2 did not change the results, while Layer 3 reduced wrong answers from 6 to 4 by rejecting answers that could not be verified. For me, Layer 1 changed what

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

One interesting failure was q18, where the agent had to calculate how many percentage points the CPI in Jambyl fell between 2022 and 2025. Even with all three protection layers, it could not give a verified answer.

The problem started during the calculation. The model received the values 16.1 and 10.6 from the tool, but instead of simply subtracting them, it divided the difference by 100. The calculate tool returned 0.055, while the model answered 0.55 percentage points.

Layer 3 noticed that 0.55 was not supported by the tool results and rejected the answer. However, the model repeated the same calculation and still gave the wrong answer. Finally, the system returned UNVERIFIED.

I would add a separate check for percentage point calculations to make sure the correct formula is used. This could improve accuracy, but it would require extra checks and processing time.




## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

One interesting failure was q18, where the agent had to calculate how many percentage points the CPI in Jambyl fell between 2022 and 2025. Even with all three protection layers, it could not give a verified answer.

The problem started during the calculation. The model received the values 16.1 and 10.6 from the tool, but instead of simply subtracting them, it divided the difference by 100. The calculate tool returned 0.055, while the model answered 0.55 percentage points.

Layer 3 noticed that 0.55 was not supported by the tool results and rejected the answer. However, the model repeated the same calculation and still gave the wrong answer. Finally, the system returned UNVERIFIED.

I would add a separate check for percentage point calculations to make sure the correct formula is used. This could improve accuracy, but it would require extra checks and processing time.



---

I wrote this file myself, without any AI tool.
