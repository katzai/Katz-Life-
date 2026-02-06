# KATZ LIFE - Flask App for PythonAnywhere

This Flask application hosts the KATZ LIFE interactive web experience.

## Project Structure

```
katz-life-flask/
├── flask_app.py          # Main Flask application
├── requirements.txt      # Python dependencies
├── templates/
│   └── index.html       # Main HTML template
└── README.md            # This file
```

## Local Testing

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Run the app:
```bash
python flask_app.py
```

3. Open browser to: `http://127.0.0.1:5000`

## PythonAnywhere Deployment

### Step 1: Upload Files

1. Log in to your PythonAnywhere account
2. Go to the "Files" tab
3. Create a new directory (e.g., `katz-life`)
4. Upload all files maintaining the structure:
   - `flask_app.py`
   - `requirements.txt`
   - `templates/index.html`

### Step 2: Set Up Virtual Environment

Go to a Bash console and run:

```bash
cd ~/katz-life
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Step 3: Configure Web App

1. Go to the "Web" tab
2. Click "Add a new web app"
3. Choose "Manual configuration" (not the Flask wizard)
4. Select Python 3.10 (or latest available)
5. In the "Code" section:
   - Source code: `/home/yourusername/katz-life`
   - Working directory: `/home/yourusername/katz-life`

6. In the "Virtualenv" section:
   - Enter: `/home/yourusername/katz-life/venv`

7. Edit the WSGI configuration file (click the link under "Code"):

Replace the contents with:

```python
import sys
import os

# Add your project directory to the sys.path
project_home = '/home/yourusername/katz-life'
if project_home not in sys.path:
    sys.path.insert(0, project_home)

# Set environment variable for Flask
os.environ['FLASK_APP'] = 'flask_app.py'

# Import the Flask app
from flask_app import app as application
```

**Important:** Replace `yourusername` with your actual PythonAnywhere username!

8. Click "Reload" at the top of the Web tab

### Step 4: Access Your App

Your app will be available at:
`http://yourusername.pythonanywhere.com`

## Troubleshooting

### Error Logs
Check the error log on the Web tab if something goes wrong.

### Common Issues

1. **Import errors**: Make sure the virtual environment is correctly set up and requirements are installed
2. **404 errors**: Verify the template is in the `templates/` directory
3. **Path issues**: Double-check all paths in the WSGI file use your correct username

### Static Files (if needed)

The app currently uses CDN links for external resources. If you need to serve static files:
1. Create a `static/` folder
2. Add this to your WSGI file:
```python
# Static files configuration
static_folder = os.path.join(project_home, 'static')
```

## Features

- Interactive onboarding experience
- Birthday insights generation
- Future story writing
- Life movie script creation
- User profile with achievements
- PDF export functionality
- File management system
- Experience points and leveling

## Notes

- All user data is stored in browser localStorage
- No backend database required
- The app is client-side focused with Flask serving the static content
- External dependencies are loaded via CDN (jsPDF, html2canvas)

## Support

For PythonAnywhere-specific issues, check:
- [PythonAnywhere Help](https://help.pythonanywhere.com/)
- [PythonAnywhere Forums](https://www.pythonanywhere.com/forums/)
