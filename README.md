# 🎓 Student Budget Checker

**ISYS2001 Introduction to Business Programming — Assessment 2**
**Author:** Shanta Basak

## What it does

Many university students run out of money before the end of the month without knowing where it went. The Student Budget Checker helps them see where their money goes and how to stay within budget.

A student can:
1. **Upload a CSV file** of their transactions.
2. **Enter a monthly budget** for each spending category.
3. **See a spending summary** — total spent per category, whether each category is OVER or WITHIN BUDGET, how much over or left, and the overall balance.
4. **Chat with "Budget Buddy"**, an AI assistant (Google Gemini) that gives personalised saving tips based on the student's real numbers.

## Features

| Requirement | How my app meets it |
|---|---|
| R1 – AI assistant with a persona | "Budget Buddy" uses Google Gemini with a system instruction that sets its persona and rules, and handles off-topic or unclear questions. |
| R2 – Uses the user's own data | Every question includes the student's spending summary, so answers use their real numbers. |
| R3 – Custom tool | `check_budget` adds up spending per category with a dictionary and loop and compares it with each budget. It handles bad input with friendly messages. |
| R4 – Interface | A Gradio interface: upload a file, type budgets, check the budget, and chat. |
| R5 – Tests | Assert tests for normal cases, edge cases and bad inputs (section 6.2 of the notebook). |
| R6 – Six-step method | Steps 1–6 are in the notebook, with design steps written before the code. |

## Sample input

**File:** `sample_transactions.csv`

| date | description | category | amount |
|---|---|---|---|
| 01/09/2026 | Coles | Groceries | 45.50 |
| 03/09/2026 | Transperth | Transport | 20.00 |
| 05/09/2026 | Netflix | Entertainment | 16.99 |
| 10/09/2026 | Woolworths | Groceries | 62.30 |
| 15/09/2026 | Movies | Entertainment | 25.00 |
| 20/09/2026 | Transperth | Transport | 20.00 |

**Budgets typed in the app:** `Groceries=100, Transport=50, Entertainment=30`

## Sample output

```
Spending summary:
- Groceries: spent $107.80 of $100.00 budget (OVER by $7.80)
- Transport: spent $40.00 of $50.00 budget (within budget, $10.00 left)
- Entertainment: spent $41.99 of $30.00 budget (OVER by $11.99)
Total spent: $189.79 of $180.00 total budget
Overall: OVER budget by $9.79
```

**Example chat question:** "Where am I spending too much?"
**Example answer (shortened):** "You're spending too much in Entertainment and Groceries. Entertainment: you went over by $11.99 (spending $41.99 instead of your $30.00 budget)…"

(AI answers are different each time, but they always use the student's real numbers.)

## How to run it

1. Open `finance_assistant.ipynb` in **Google Colab** (click the "Open in Colab" badge at the top of the notebook on GitHub).
2. Get a free Gemini API key from [Google AI Studio](https://aistudio.google.com/).
3. In Colab, click the **🔑 Secrets** icon on the left, add a secret named **`GEMINI_API_KEY`** with your key, and turn on **Notebook access**.
4. Click **Runtime → Run all**.
5. Scroll to section **5.8** — the app appears under the cell.
6. Upload `sample_transactions.csv` (or your own CSV with the columns `date, description, category, amount`), type your budgets like `Groceries=100, Transport=50`, and click **Check my budget**.
7. Ask Budget Buddy a question in the chat box.

**Note:** If Gemini is busy, the assistant may take up to a minute or show a "please try again" message. The budget summary still works without the AI.

## Repository contents

| File | What it is |
|---|---|
| `finance_assistant.ipynb` | The full project: six-step design, code, interface and tests |
| `DIARY.md` | My Developer's Diary — weekly progress and how I used AI |
| `sample_transactions.csv` | Sample data to try the app |
| `README.md` | This file |

## Privacy note

Please don't upload real bank statements. The free Gemini tier may use inputs to improve Google's services, so use sample or made-up data.

## AI use

I used Claude (an AI assistant) to guide me step by step and to help write and explain the code. I ran, tested and checked everything myself. All AI use is recorded in `DIARY.md`.
