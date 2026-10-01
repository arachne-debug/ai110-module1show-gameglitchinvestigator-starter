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
|3|20|50|75|99|Would guide me towrads the right number|Would always tell me to go higher|Answer was 25
|25|"Go higher or lower Did not allow me to start a new game |Did not allow me to play the game again afterwards |"Game over, start a new game" |
| | | | |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project? Claude
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result). The file had no #include lines. AI added <stdio.h> and <string.h>.
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: "A good test: enter 1, then 1011 (should give 11), then y, then 2, then 5.5" I did not want the game to allow the system to allow any numbers after the game is completed.
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed? I reran the code and tinkered with the bugs I found in the last phase.
- Describe at least one test you ran (manual or using pytest)and what it showed you about your code. Used pytest to run the game and got the answer after 4 tries. Code is much more efficient and a lot less buggy.
  
- Did AI help you design or understand any tests? How? AI Gave a full range of explanation that helped walked me through the issues I was having in order to help familiarize me with my code.
---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
I would describe Streamlit as a streaming service like Netflix or Hulu, a hub for python coders to create interactive apps.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects? I definitely will be using my AI Assistance to program my AI Debugger. The AI assistant is very helpful in VSCode.
  - This could be a testing habit, a prompting strategy, or a way you used Git. I used git to properly set up the repository and code
- What is one thing you would do differently next time you work with AI on a coding task? Definitely describe my problems and have it clean up code in sticky situations
- In one or two sentences, describe how this project changed the way you think about AI generated code. I see AI Generated code through claude a lot better than ChatGPT or any other open source.
