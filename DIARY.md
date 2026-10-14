# Developer's Diary 

## Week 1 — 29 Sep 2026

Today I set up my project: GitHub repo, diary file and Colab notebook.
I chose a Student Budget Checker because many students don't know
where their money goes each month.

I used Claude to guide me through the setup, since I hadn't used
GitHub much before. I asked it to explain things I wasn't sure about,
like what the "main branch" means.

When I tested Gemini, I got a "503 UNAVAILABLE - high demand" error.
I thought my key was wrong, but it was Google's server being busy.
I asked Claude for a better test. It gave me code with try/except that
retries 3 times and then uses a backup model. I read through it to
understand it before using it. The backup model worked and replied
"Hello, Shanta, I hope you're having a wonderful day!"

What I learned: an API can fail even when my code is right, so my app
needs error handling so it doesn't crash.

<img width="1152" height="816" alt="gemini_test_success" src="https://github.com/user-attachments/assets/c54f4920-a28b-4f35-a2f0-e2cca48ed211" />

Next: write my design steps before Sunday 4 October.

## Week 1 — Session 2 (1 October 2026)

Today, I completed the initial design steps for my Student Budget Checker app before starting the coding.

**Step 1 (Problem):** I identified the target users, their budgeting problems and how my app could help them. I used Claude to review my answers and received suggestions to make the app's purpose clearer. I updated the final version to focus on CSV uploads, spending analysis and AI chat.

**Step 2 (Inputs and outputs):** I listed the main inputs and outputs of my app. After reviewing my initial ideas with Claude, I decided to remove income and savings goals because my app focuses mainly on tracking expenses against a budget. I used Claude's updated version of Step 2, which also included possible errors and issues to consider when testing the app.

**Step 3 (Worked example):** I calculated the spending totals myself using a calculator: Groceries 107.80, Transport 40.00 and Entertainment 41.99, giving an overall total of 189.79. With some help from Claude, I improved the example by showing how much each category was over or under its budget. I also fixed a formatting issue in Google Colab by using `\$` for dollar signs.

**Step 4 (Pseudocode):** I wrote the pseudocode for my app using the suggested starter as a guide. I added the main steps, including starting and ending the program, calculating total expenses and asking users to enter their budgets again when the values are invalid. Claude helped me identify a few issues, and I revised the pseudocode to make the steps clearer and consistent with my app's purpose.

**What I learned:** I learned that planning and calculating a worked example before coding can help me understand how the app should work. The calculated totals will also help me test whether my code produces the correct results.

**Next week:** I plan to start coding the app by loading the CSV file, writing the budget calculation function and connecting the Gemini AI assistant.

## Week 2 — Session 1 (10 October 2026)

Today I started coding my Student Budget Checker, following my Step 4 pseudocode.

**What I built:**
- A sample CSV using the same 6 transactions as my Step 3 worked example.
- `load_transactions`: reads the CSV and checks for the problems from my Step 2 list (no file, empty file, missing column, amount not a number).
- `check_budget`: my custom tool. It adds up spending per category using a dictionary and a loop, then marks each category as OVER, WITHIN BUDGET or No budget set.

**AI use:** I asked Claude to write the code one part at a time and explain each line. I ran every cell myself and checked the results before moving on. I asked questions when I didn't understand something.

**Testing against my worked example:** My code's results matched my Step 3 hand calculations exactly: Groceries 107.80 (OVER by 7.80), Transport 40.00 (10.00 left), Entertainment 41.99 (OVER by 11.99), total 189.79.

<img width="1312" height="582" alt="image" src="https://github.com/user-attachments/assets/a2e4e82d-dcf0-43c1-af9b-dd52e9c18b24" />


**Problem I learned about:** Without rounding, Python calculates 16.99 + 25.00 as 41.989999999999995 instead of 41.99, because computers store decimals slightly imprecisely. Using round(..., 2) fixes this so the money values are correct.

**Bad input checks:** I tested 6 bad inputs (negative budget, text budget, no file, empty file, "twenty" as an amount, and a category with no budget). Each one showed a clear message instead of crashing.

<img width="1247" height="151" alt="image" src="https://github.com/user-attachments/assets/cce23742-0ecd-4862-aa55-d0326a47b46e" />

**Next session:** connect the Gemini AI assistant to my budget results and start the Gradio interface.

## Week 2 — Session 2 (11 October 2026)

Today I connected the AI assistant to my budget results and built the app interface.

**What I built:**
- `format_summary`: turns my check_budget results into readable text with dollar amounts (e.g. "Groceries: spent $107.80 of $100.00 budget (OVER by $7.80)").
- `ask_budget_assistant`: my AI assistant "Budget Buddy" using Gemini. A system instruction gives it a persona and rules, and every question includes the student's spending summary so its answers use their real numbers.
- A Gradio interface where a student can upload a CSV, type their budgets, check their budget and chat with Budget Buddy.

**AI use:** I asked Claude to write each part step by step and explain the code. I ran and tested every part myself and asked questions when I was unsure.

**Testing the assistant:** I tested 3 kinds of questions:
- "Where am I spending too much?" – it used my real numbers correctly.
- "Who won the football last night?" (off-topic) – it politely said it only helps with budgeting and suggested budgeting questions instead.
- "help" (unclear) – it gave a short overview and then asked which category I wanted help with.

> Budget Buddy's answer: "You went over by $11.99 (spending $41.99 instead of your $30.00 budget)."

I checked every number in its answers against my Step 3 worked example and they were all correct. It did not make up any numbers.

**Testing the app:** I used the app like a student would: uploaded the sample CSV, typed my budgets, checked my budget and asked questions. Then I tried to break it with no file, an empty budget box, "Groceries=abc" and a negative budget. Each one showed a friendly ⚠️ message instead of crashing.

**Problem I noticed:** When Gemini was busy, the assistant took a long time to answer because it waits and retries several times before giving up. I will look at making this faster in the final week.

**Next week:** write assert tests, add the README and sample data file, and submit.

## Week 3 — Session 1 (14 October 2026)

Today I started testing my app with awkward input.

**Bug I found and fixed:** I tested what happens if a student types their budget categories in lowercase (e.g. "groceries=100"). The app showed "No budget set" for every category, even though budgets were entered, because Python treats "groceries" and "Groceries" as different words. I fixed this by adding .title() in load_transactions and parse_budgets so category names always match. I ran the test again and it then showed OVER / WITHIN BUDGET correctly.

**AI use:** Claude suggested testing lowercase input and gave me the code for the test and the fix. I ran the test myself, saw the bug happen, made the two edits, and checked that it worked afterwards.

**What I learned:** My app worked perfectly with my own sample data, but a real student could easily type in lowercase. Testing with awkward input finds problems that normal testing misses.

**Next session:** assert tests, README, final reflection and submit.
