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
 import tkinter as tk
from tkinter import messagebox

# Initialize main window
root = tk.Tk()
root.title("Tic Tac Toe")
root.resizable(False, False)
root.configure(bg="#f0f0f0")

# Game variables
current_player = "X"
buttons = []
game_active = True

# All possible winning combinations
WIN_COMBINATIONS = [
    (0, 1, 2),  # Row 1
    (3, 4, 5),  # Row 2
    (6, 7, 8),  # Row 3
    (0, 3, 6),  # Column 1
    (1, 4, 7),  # Column 2
    (2, 5, 8),  # Column 3
    (0, 4, 8),  # Diagonal 1
    (2, 4, 6),  # Diagonal 2
]


def check_winner():
    for combo in WIN_COMBINATIONS:
        a, b, c = combo
        if (buttons[a]["text"] == buttons[b]["text"] == buttons[c]["text"] != ""):
            return combo
    return None


def check_draw():
    for btn in buttons:
        if btn["text"] == "":
            return False
    return True


def button_click(index):
    global current_player, game_active

    if not game_active:
        return

    if buttons[index]["text"] != "":
        return

    buttons[index]["text"] = current_player
    buttons[index]["fg"] = "#e74c3c" if current_player == "X" else "#2980b9"

    winning_combo = check_winner()
    if winning_combo:
        for i in winning_combo:
            buttons[i].configure(bg="#f1948a")
        game_active = False
        messagebox.showinfo("Game Over", f"Player {current_player} Wins!")
        return

    if check_draw():
        game_active = False
        messagebox.showinfo("Game Over", "It's a Draw!")
        return

    current_player = "O" if current_player == "X" else "X"
    turn_label.config(text=f"Player {current_player}'s Turn")


def reset_game():
    global current_player, game_active
    current_player = "X"
    game_active = True
    for btn in buttons:
        btn.config(text="", bg="#ffffff", fg="#000000")
    turn_label.config(text="Player X's Turn")


# Title
title_label = tk.Label(
    root,
    text="Tic Tac Toe",
    font=("Helvetica", 24, "bold"),
    bg="#f0f0f0",
    fg="#2c3e50"
)
title_label.pack(pady=(20, 5))

# Turn label
turn_label = tk.Label(
    root,
    text="Player X's Turn",
    font=("Helvetica", 14),
    bg="#f0f0f0",
    fg="#555555"
)
turn_label.pack(pady=(0, 10))

# Board frame
board_frame = tk.Frame(root, bg="#2c3e50", padx=3, pady=3)
board_frame.pack(padx=20)

# 3x3 buttons
for i in range(9):
    btn = tk.Button(
        board_frame,
        text="",
        font=("Helvetica", 28, "bold"),
        width=4,
        height=2,
        bg="#ffffff",
        fg="#000000",
        relief="flat",
        cursor="hand2",
        command=lambda idx=i: button_click(idx)
    )
    btn.grid(row=i // 3, column=i % 3, padx=3, pady=3)
    buttons.append(btn)

# Reset button
reset_btn = tk.Button(
    root,
    text="Reset Game",
    font=("Helvetica", 12, "bold"),
    bg="#2c3e50",
    fg="#ffffff",
    padx=20,
    pady=8,
    relief="flat",
    cursor="hand2",
    command=reset_game
)
reset_btn.pack(pady=20)

# Footer
footer = tk.Label(
    root,
    text="By Sawaira Mubashir & Uzma Nazeer | MME",
    font=("Helvetica", 9),
    bg="#f0f0f0",
    fg="#aaaaaa"
)
footer.pack(pady=(0, 10))

root.mainloop()
