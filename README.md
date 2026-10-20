# Lindy's Pharmacy — Online Appointment & Services System

Flask app prepared for a class-project deployment.

## Deploy on PythonAnywhere (quick path)
1. Create/sign in to a PythonAnywhere account.
2. Upload this ZIP and extract it into a folder such as `/home/YOURUSERNAME/lindys_pharmacy`.
3. Open a Bash console and run:
   `cd /home/YOURUSERNAME/lindys_pharmacy`
   `python3 -m pip install --user -r requirements.txt`
4. Open the **Web** tab, choose **Add a new web app**, select Manual configuration and a Python version.
5. Edit the WSGI configuration file to add the project folder to `sys.path` and import the app (example below).
6. In the Web tab, set a virtualenv if you created one, then click **Reload**.

Example WSGI configuration (replace YOURUSERNAME):
```python
import os, sys, secrets
project = '/home/YOURUSERNAME/lindys_pharmacy'
if project not in sys.path:
    sys.path.insert(0, project)
os.environ.setdefault('FLASK_SECRET_KEY', secrets.token_hex(32))
os.environ.setdefault('STAFF_USERNAME', 'staff')
os.environ.setdefault('STAFF_PASSWORD', 'CHANGE-THIS-TO-A-LONG-UNIQUE-PASSWORD')
from app import app as application
```
Use a long, unique `FLASK_SECRET_KEY` value and a strong staff password. Keep these out of public source control. After changing WSGI settings, reload the web app.

## Important
- The original `database.db` was intentionally **not included** in this package because it may contain patient information. A fresh database is created automatically on first app import. If you need existing demo records, import only sanitized/fake data after deployment.
- This is a classroom demo, not ready for real patient information. Before real use, add stronger authentication, CSRF protection, privacy/security review, backups, and a persistent database strategy.
- The app's staff portal is configured with environment variables; login is disabled until `STAFF_PASSWORD` is set.
- Use a persistent host/storage for SQLite. Do not rely on ephemeral container storage for appointment records.
