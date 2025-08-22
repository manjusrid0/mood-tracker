import tkinter as tk
from tkinter import messagebox, ttk
import sqlite3
from datetime import date
import matplotlib.pyplot as plt
import sqlite3

conn= sqlite3.connect('mood_tracker.db')
cursor = conn.cursor()
cursor.execute(''' CREATE TABLE IF NOT EXISTS mood_log( id INTEGER PRIMARY KEY AUTOINCREMENT, date TEXT NOT NULL, mood TEXT NOT NULL, note TEXT)''')
conn.commit()
conn.close()
# Connect to database
def connect_db():
    conn = sqlite3.connect('mood_tracker.db')
    return conn

# Save entry
def save_mood():
    mood = mood_var.get()
    note = note_entry.get()
    today = date.today().strftime("%Y-%m-%d")

    if not mood:
        messagebox.showerror("Error", "Please select a mood.")
        return

    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("INSERT INTO mood_log (date, mood, note) VALUES (?, ?, ?)",
                   (today, mood, note))
    conn.commit()
    conn.close()
    messagebox.showinfo("Saved", "Your mood has been saved!")
    mood_var.set("")
    note_entry.delete(0, tk.END)

# View entries
def view_entries():
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT date, mood, note FROM mood_log ORDER BY id DESC")
    rows = cursor.fetchall()
    conn.close()

    view_win = tk.Toplevel(root)
    view_win.title("Mood History")

    tree = ttk.Treeview(view_win, columns=("Date", "Mood", "Note"), show="headings")
    tree.heading("Date", text="Date")
    tree.heading("Mood", text="Mood")
    tree.heading("Note", text="Note")

    for row in rows:
        tree.insert("", tk.END, values=row)

    tree.pack(fill=tk.BOTH, expand=True)

# Show chart
def show_chart():
    conn = connect_db()
    cursor = conn.cursor()
    cursor.execute("SELECT mood, COUNT(*) FROM mood_log GROUP BY mood")
    data = cursor.fetchall()
    conn.close()

    if not data:
        messagebox.showinfo("No Data", "No mood data to display.")
        return

    moods = [d[0] for d in data]
    counts = [d[1] for d in data]

    plt.figure(figsize=(6, 4))
    plt.bar(moods, counts, color="skyblue")
    plt.title("Mood Frequency Chart")
    plt.xlabel("Mood")
    plt.ylabel("Count")
    plt.tight_layout()
    plt.show()

# GUI setup
root = tk.Tk()
root.title("Daily Mood Tracker")
root.geometry("400x300")

tk.Label(root, text="Select your mood:").pack(pady=5)
mood_var = tk.StringVar()
mood_menu = ttk.Combobox(root, textvariable=mood_var)
mood_menu['values'] = ["Happy", "Sad", "Angry", "Excited", "Calm", "Anxious"]
mood_menu.pack()

tk.Label(root, text="Optional Note:").pack(pady=5)
note_entry = tk.Entry(root, width=40)
note_entry.pack()

tk.Button(root, text="Submit", command=save_mood).pack(pady=10)
tk.Button(root, text="View History", command=view_entries).pack(pady=5)
tk.Button(root, text="View Mood Chart", command=show_chart).pack(pady=5)

root.mainloop()
