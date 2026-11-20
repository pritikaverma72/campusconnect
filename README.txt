CAMPUSCONNECT - FULL STACK LOCAL PROJECT

FILES
- app.py: Flask backend and complete responsive frontend in one file.
- requirements.txt: Python dependency.
- uploads/: uploaded evidence files are stored here (created automatically).
- campusconnect.db: SQLite database, created automatically on first run.

SETUP (Windows / VS Code)
1. Extract this ZIP.
2. Open the CampusConnect folder in VS Code.
3. Open Terminal > New Terminal.
4. Install Flask:
      py -m pip install -r requirements.txt
   If `py` is not recognized, use `python -m pip install -r requirements.txt`.

CREATE AN ADMIN ACCOUNT
Run:
      py app.py --create-admin
Enter the administrator email and a password of at least 8 characters.
Student registration on the website never creates an admin account.

START THE WEBSITE
Run:
      py app.py
Then open:
      http://127.0.0.1:5000

IMPORTANT
- Do NOT open app.py in the browser or use Live Server. Run the Python server.
- Register a student account on the website, then log in.
- To use Admin Management, create an admin account using the command above, stop the server if it is running, run the command, then start `py app.py` again and log in with the admin account.
- Complaints and suggestions are stored in SQLite on this computer.
- This is an educational prototype, not production-ready. Before real deployment, add HTTPS, CSRF protection, rate limiting, stronger upload authorization, secure production configuration, backups and institution-approved privacy/security practices.
