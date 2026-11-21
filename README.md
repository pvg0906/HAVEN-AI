# Haven AI – Emotional Support Chatbot

Haven AI offers supportive conversations, guided breathing exercises, and calming music. The web interface uses HTML, Tailwind CSS, and JavaScript. Flask serves the pages, MySQL stores user accounts, and Ollama runs Llama 3 locally.

## First-time setup on Windows

Install Git, Python, [MySQL Community Server](https://dev.mysql.com/downloads/mysql/), and [Ollama for Windows](https://ollama.com/download/windows). Configure MySQL to run as a Windows service on port `3306`.

### 1. Download the project and install Python packages

Open PowerShell and run:

~~~powershell
cd ([Environment]::GetFolderPath('MyDocuments'))
git clone https://github.com/pranav2004cyber/EMOTIONAL-SUPPORT-AI-CHATBOT.git
cd EMOTIONAL-SUPPORT-AI-CHATBOT
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install flask flask-bcrypt flask-cors mysql-connector-python ollama
~~~

If you already cloned the project, open your existing project folder and start with the virtual environment command.

### 2. Download Llama 3

Open Ollama from the Windows Start menu, then run:

~~~powershell
ollama pull llama3
~~~

### 3. Create the database

Open **MySQL Command Line Client** from the Start menu and enter the root password you chose during MySQL setup. At the `mysql>` prompt, run:

~~~sql
CREATE DATABASE IF NOT EXISTS haven_db;
USE haven_db;

CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL
);
~~~

### 4. Configure the database connection

Open `app.py` and find the database settings near the top. Use `localhost` for the host, `root` for the user if you followed the setup above, and `haven_db` for the database. Replace the existing password value with your own MySQL password in your local copy. Keep this password out of GitHub and out of this README.

## Run Haven AI on Windows

1. Make sure the MySQL service is running. Press **Win + R**, enter `services.msc`, and start your MySQL service if it is stopped. The service name depends on your installation.
2. Open Ollama from the Start menu.
3. Open PowerShell in the project folder, where `app.py` and `.venv` are located, and run:

   ~~~powershell
   .\.venv\Scripts\python.exe .\app.py
   ~~~

4. When Flask prints its local address, open [http://127.0.0.1:5000/](http://127.0.0.1:5000/). Keep PowerShell open while using Haven.
5. Sign up or log in, then open the chat and send a test message.

Press **Ctrl+C** in the Flask PowerShell window to stop Haven.

## Troubleshooting

| Error | What to check |
| --- | --- |
| MySQL error 2003 or connection refused | Check that the MySQL service is running on port `3306`. |
| Access denied | Check that the user and password in your local `app.py` match your MySQL account. |
| Unknown database or missing `users` table | Run the SQL in step 3 against the same MySQL instance Haven uses. |
| Ollama connection or model error | Open Ollama and run `ollama list` to check that `llama3` is installed. |
| PowerShell cannot find `app.py` or the virtual environment | Open the project folder and complete the Python setup in step 1. |
