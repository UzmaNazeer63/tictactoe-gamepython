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
