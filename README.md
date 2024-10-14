#developing stopwatch using tkinter in python 
# project3
stopwatch

import tkinter as tk

root = tk.Tk()
root.geometry('400x400')
root.title("Stopwatch")

label1 = tk.Label(root, text="00:00:00")
label1.grid(row=0, column=1)

running = False
sec = 0
min = 0
hour = 0

def concatenate_zero(a):
    if a < 10:
        return '0' + str(a)
    return str(a)

def start_stopwatch():
    global running
    running = True
    update_stopwatch()

def stop_stopwatch():
    global running
    running = False

def reset_stopwatch():
    global sec, min, hour
    sec = 0
    min = 0
    hour = 0
    update_label()

def update_stopwatch():
    global sec, min, hour
    if running:
        sec += 1
        if sec == 60:
            sec = 0
            min += 1
            if min == 60:
                min = 0
                hour += 1
        update_label()
        root.after(500, update_stopwatch)

def update_label():
    time = f"{concatenate_zero(hour)}:{concatenate_zero(min)}:{concatenate_zero(sec)}"
    label1.config(text=time)

tk.Button(root, text="Start", command=start_stopwatch).grid(row=1, column=0)
tk.Button(root, text="Stop", command=stop_stopwatch).grid(row=1, column=1)
tk.Button(root, text="Reset", command=reset_stopwatch).grid(row=1, column=2)

root.mainloop()
