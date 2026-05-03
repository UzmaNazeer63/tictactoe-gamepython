 My Tic Tac Toe – README

📌 Project Overview

My Tic Tac Toe is a simple and interactive desktop game built using Python Tkinter. It allows two players to play the classic Tic Tac Toe game turn by turn with a clean graphical interface.

This project is beginner-friendly and demonstrates how to create GUI applications in Python using buttons, labels, functions, loops, and game logic.

---

 Features:
. User-friendly graphical interface
. Two-player gameplay (X and O)
. Automatic turn switching
. Win detection system
. Draw game detection
. Winning boxes highlighted in pink
. Result popup message
. Clean and simple code structure

---
 Technologies Used:

- Python 3
- Tkinter (Built-in Python GUI Library)
- Messagebox for result alerts

---

📂 How the Game Works

1. The game starts with Player X.
2. Players click empty boxes to place their mark (X or O).
3. The program checks after every move:
   - If a player wins
   - If the match is a draw
4. Winning row/column/diagonal turns pink.
5. Result is shown in a popup message.

---

🏆 Winning Conditions

A player wins if they complete:

- Any horizontal row
- Any vertical column
- Any diagonal line

---

 How to Run the Project:

Step 1:

Install Python on your computer.

Step 2:

Save the code in a file named:

tic_tac_toe.py

Step 3:

Run the file using terminal:

python tic_tac_toe.py

---

📸 Interface Preview

 X | O | X
-----------
 O | X | O
-----------
 X |   | O

Turn label appears below board:

Turn: X

---

Concepts Used in This Project

- Functions
- Lists
- Loops
- Conditions
- GUI Buttons
- Labels
- Event Handling
- Lambda Functions

---

 Future Improvements:

You can upgrade this project by adding:

- Restart Button
- Score Board
- Sound Effects
- AI Computer Opponent
- Dark Mode Theme
- Timer Mode

---
 Author:
Uzma Nazeer(12-3-1-039-2025)
Sawaira Mubashir(12-3-1-037-2025)

 Why This Project is Good:

This project is excellent for students and beginners because it improves understanding of:

- Python programming
- GUI development
- Logic building
- Problem solving


 Final Note:

This Tic Tac Toe game is simple, attractive, and a great mini project for academic submission or portfolio showcase.
                                     -----------------------
python code:
import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.title("My Tic Tac Toe")

player = "X"
end = False
boxes = []

def check():
    global end

    # all possible wins written in simple way
    wins = [
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
    ]

    for w in wins:
        a,b,c = w
        if boxes[a]["text"] != "":
            if boxes[a]["text"] == boxes[b]["text"] and boxes[b]["text"] == boxes[c]["text"]:
               
                boxes[a].config(bg="pink")
                boxes[b].config(bg="pink")
                boxes[c].config(bg="pink")

                end = True
                messagebox.showinfo("Result", boxes[a]["text"] + " wins")
                root.quit()
                return

    # check draw
    filled = True
    for b in boxes:
        if b["text"] == "":
            filled = False

    if filled and not end:
        messagebox.showinfo("Result", "Draw game")
        root.quit()

def play(n):
    global player

    if boxes[n]["text"] == "" and end == False:
        boxes[n]["text"] = player

        check()

        if end == False:
            if player == "X":
                player = "O"
            else:
                player = "X"

            turn_label.config(text="Turn: " + player)

# create buttons
i = 0
while i < 9:
    btn = tk.Button(root, text="", width=5, height=2, font=("Arial",18),
                    command=lambda x=i: play(x))
    boxes.append(btn)
    btn.grid(row=i//3, column=i%3)
    i += 1

turn_label = tk.Label(root, text="Turn: X", font=("Arial",14))
turn_label.grid(row=3, column=0, columnspan=3)

root.mainloop()


