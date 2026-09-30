# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] Describe the game's purpose.: - [x] Explain what fixes you appli：Led.
：: The hints pointed in the wrong direction, New Game did not fully reset the game, and the player had fewer attempts than expected. I also found problems with scoring and the displayed guess range.
## 📸 Demo Walkthrough：: I corrected the hints, reset the game state when starting a new game, and initialized attempts to zero. I fixed the scoring and updated the display after processing each guess. I moved four helper functions into logic_utils.py and added a regression test. All four tests passed.

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. Select Normal difficulty and click New Game. The range is 1–100, with 8 attempts available and a score of 0
2. In this example, the secret number is 51. The secret is randomly generated, so it may differ in another game 
3. Enter 81 and click Submit Guess. The game shows "Too High" and "Go LOWER!". The score becomes -5, with 7 attempts left
4. Enter 51 and submit again. The game shows "Correct!" and ends with a win. The final score is 75, with 6 attempts left
5. Click New Game. The score resets to 0, attempts return to 8, history is cleared, and a new secret number is generated

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
PS E:\Python Code\ai110-module1show-gameglitchinvestigator-starter> .\.venv\Scripts\python.exe -m pytest
=================================================================================================== test session starts ===================================================================================================
platform win32 -- Python 3.12.10, pytest-9.1.1, pluggy-1.6.0
rootdir: E:\Python Code\ai110-module1show-gameglitchinvestigator-starter
collected 4 items                                                                                                                                                                                                          

tests\test_game_logic.py ....                                                                                                                                                                                        [100%]

==================================================================================================== 4 passed in 0.02s ====================================================================================================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
