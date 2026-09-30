# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
|Guess of 50(answer is 62) | "go higher" hint|"go lower" hint | wrong hint`app.py`, `check_guess()`, lines 37–40 |
|new game | game restart |answer randomly reset, but no attempt to try |`app.py`, lines 134–145; `status` is not reset|
|change difficult from easy to normal |"Guess a number between 1 and 50" |text didn't change, still|`app.py`, line 96 and lines 109–111 |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?

  - I use ChatGPT for this project.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

  - AI suggest a change of difficulty, I did and actually find problem about UI which didn't show the new range of the number. 
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count.
  - I reject the suggest thattreat the secret number changing after every Submit click as the main state bug. The suggestion came from the original README, but after inspecting `app.py` and testing the game, I found that `st.session_state.secret` actually preserves the secret between normal submissions. I rejected that suggestion because it did not match the current code behavior. Instead, I focused on the confirmed issues: the unchanged UI range, reversed hints, incorrect attempt display, and the New Game button failing to reset the game state. I verified my decision by checking the Developer Debug Info after multiple submissions.
  
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  - I try the same thing when it had bug and compare with old result and the requirment, if that satisfy the requirment, then it fixed. I also double check the code on my own to see if there is any hidden bug.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  - I ran pytest, and all four tests passed. My new test checks that when the secret is 50 and the guess is 60, the result is "Too High" and the hint contains "LOWER". This showed that the hint gives the correct direction for this case. The original tests only checked the result, so they could not catch the reversed hint.
- Did AI help you design or understand any tests? How?
  - Yes. ChatGPT helped me add a test for the reversed hint. It explained why checking only "Too High" was not enough and suggested also checking that the message contains "LOWER". It also helped me understand that check_guess returns a tuple containing both the result and the hint, so the original tests needed to check the first item.
  
---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  - When a user interacts with a widget, Streamlit reruns the script from top to bottom. Normal variables can be recreated, but st.session_state keeps values between reruns in the same session. In this game, it stores the secret number, attempts, score, and history. The New Game button needs to explicitly reset those values to start a fresh game.
  
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - I want to keep the habit of reproducing a bug before changing the code and repeating the same steps after the fix. I also want to add a regression test for the bug, so I can check whether it comes back after future changes.
- What is one thing you would do differently next time you work with AI on a coding task?
  - Next time, I will ask AI to help with one small change at a time and explain why it is needed. I will review and test each change before moving on, so I can understand the code instead of getting overwhelmed by a complete solution.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  - This project showed me that AI-generated code can run and still have bugs in its behavior. I need to understand and test the code before trusting it.
