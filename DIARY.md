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
