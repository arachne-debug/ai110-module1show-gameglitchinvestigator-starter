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

- [x] Describe the game's purpose.
- [x] Detail which bugs you found.
- [x] Explain what fixes you applied.

### Game Purpose

Glitchy Guesser is a number guessing game built with Streamlit. The game picks a secret number in a range set by the difficulty (Easy 1–20, Normal 1–100, Hard 1–50). The player has a limited number of attempts to find it (Easy 6, Normal 8, Hard 5). After each guess the game says whether to go higher or lower and updates the score. A correct guess wins the game. Using up every attempt loses it.

### Bugs Found

| # | Bug | Symptom |
|---|-----|---------|
| 1 | Hints were backwards | A guess above the secret said "Go HIGHER!" and a guess below it said "Go LOWER!" |
| 2 | Secret compared as text on even attempts | On every second guess the secret was turned into a string, so numbers were compared character by character (e.g. `9` counted as higher than `48`) and the result was wrong |
| 3 | New Game didn't restart | New Game left `status` as `"won"`/`"lost"`, so the "Game over" message kept showing and you couldn't play again |
| 4 | Guessing was allowed after the game ended | The guess box and Submit button stayed active after a win or loss |
| 5 | New Game ignored difficulty | New Game always picked the secret from 1–100, even on Easy or Hard |
| 6 | Attempt counter off by one | Attempts started at 1 on first load but 0 after New Game, so the first game gave one fewer guess |

Known issues not yet fixed:
- The prompt always says "between 1 and 100," whatever the difficulty.
- Hard (1–50) has a smaller range than Normal (1–100).
- A "Too High" guess adds 5 points on even attempts and subtracts 5 on odd ones, while "Too Low" always subtracts 5.
- Non-numeric input still uses up an attempt.

### Fixes Applied

1. **Hints:** swapped the messages in `check_guess` so "Too High" says "Go LOWER!" and "Too Low" says "Go HIGHER!"
2. **Comparison:** removed the code that turned the secret into a string, so `check_guess` always compares two integers.
3. **Restart:** New Game now runs a `start_new_game()` callback that resets the attempts, score, status and history, picks a new secret from the current difficulty's range, and clears the guess box.
4. **Locking after game end:** the guess box and Submit button are disabled whenever `status` isn't `"playing"`. After a win or loss the app calls `st.rerun()` so they lock right away, then shows the final message with the secret and score.
5. **Attempt counter:** attempts now start at 0 on both first load and New Game.

## 📸 Demo Walkthrough

A sample game on Normal difficulty (range 1–100, 8 attempts), with a secret of **58**:

1. The game starts with the message "Guess a number between 1 and 100. Attempts left: 8". Score is 0.
2. User enters a guess of **40** → "📈 Go HIGHER!" (Too Low). Score: **-5**. Attempts left: 7.
3. User enters a guess of **70** → "📉 Go LOWER!" (Too High). Score: **0** (a Too High guess on an even attempt adds 5). Attempts left: 6.
4. User enters **abc** → error "That is not a number." Score stays at **0**, but the attempt is still used. Attempts left: 5.
5. User enters a guess of **55** → "📈 Go HIGHER!" (Too Low). Score: **-5**. Attempts left: 4.
6. User enters a guess of **58** → balloons, and "You won! The secret was 58. Final score: 35. Click New Game to play again." A win on attempt 5 adds 100 − 10 × 6 = 40 points.
7. The guess box and Submit button are now disabled, so no more numbers can be entered. New Game is the only available action.
8. User clicks **New Game 🔁** → the score resets to 0, attempts left go back to 8, the guess box is cleared and unlocked, and a new secret is chosen.

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
# ========================= X passed in 0.XXs =========================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
