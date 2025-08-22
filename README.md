📝 Daily Mood Tracker

A simple Python Tkinter application to help you log, track, and analyze your daily moods.
It uses SQLite to store entries and Matplotlib to visualize mood trends.

✨ Features

✅ Log your daily mood with an optional not
✅ View your mood history in a table
✅ Generate a mood frequency chart with Matplotlib
✅ Data stored locally in SQLite database (mood_tracker.db)

🛠️ Requirements

Make sure you have Python installed (>=3.7).
Install the required dependencies:

pip install matplotlib

(tkinter and sqlite3 are included in Python by default)

🚀 How to Run

Clone or download the project.
Save the code into a file (e.g., mood_tracker.py).

Run the program:

python mood_tracker.py

📌 Usage

Select your mood from the dropdown menu.
Optionally add a note about your day.
Click Submit to save the entry.
Use View History to see past moods.
Use View Mood Chart to visualize mood distribution.

📂 Database Structure

The app uses a SQLite database named mood_tracker.db with one table:

mood_log

Column	Type	Description
id	INTEGER (PK)	Auto-incremented ID
date	TEXT	Date of entry
mood	TEXT	User’s mood
note	TEXT	Optional note
📊 Example Chart

When you log moods, you can view a bar chart showing how often each mood occurred.

🤝 Contributions

Feel free to fork and improve this app by adding:
Export to CSV / PDF
More moods & emojis
Weekly/monthly trend analysis

📜 License

This project is open-source and free to use.
