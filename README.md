Zaisha - web nfc memory upload
------------------------------
#1. Project Structure
=====================
mysite/
├── core/                    # Django app handling logic
├── templates/
│   ├── index2.html          # Landing Page
│   ├── audio.html           # Memory Upload Page (Photo, Video, Audio)
│   ├── result.html          # NFC Write Confirmation Page
│   ├── setpasswordnfc.html  # NFC Password Setup Page
├── static/                  # Static files (images, icons)
├── settings.py              # Django settings file
├── .env                     # Environment Variables (not included)
└── manage.py


#2. Features
============
    1. NFC memory storage via Web NFC API.
    2. Upload Photo, Video, or Audio files.
    3. Live audio recording and uploading.
    4. NFC Password setup for extra security.
    5. Secure and CSRF-protected Django backend.
    6. User-friendly error handling and popups.
    7. SweetAlert integration for elegant modals.

#3. Page Descriptions
=====================
1. index2.html - Landing Page
    Purpose: Introduction screen for the NFC memory upload process.
    Shows jewelry image with a "Let's Make Memories!" button.
    On click, redirects to the Memory Upload Page (audio.html) passing the IMEI via URL.
    Checks for NFC API support.
    Displays an "Access Denied" popup if required (show_popup variable).

2. audio.html - Memory Upload Page
    Upload or record one of the following:
    Photo, Video, Audio (Live recording supported)
    Preview feature for selected or recorded media.
    Slick carousel used for media selection (Photo/Video/Audio).
    Handles file inputs and dynamically injects IMEI as a hidden input.
    Supports form submission to the Django backend.
    If NFC is supported, initializes NFC scanning to read data (for potential enhancement).
    Custom loader displayed during form processing.

3. result.html - NFC Write Confirmation Page
    Writes uploaded data (photo/video/audio URL) to the NFC Tag.
    Uses Web NFC API's NDEFReader for NFC writing.
    SweetAlert popup for write success/failure.
    Displays a custom popup: "Memory Saved! Now, the memory will be unveiled by tapping Zaisha to an NFC-enabled smartphone."
    Handles NFC permission requests and error reporting.

4. setpasswordnfc.html - NFC Password Setup Page
    Allows setting or modifying NFC password linked to the jewelry (via IMEI).
    Password is stored securely in the backend.
    Toggle switch enables or disables the password requirement.
    Fetches existing password status on load (/checkpasswordstatus/ API).
    CSRF-protected password saving (/savepasswordnfc/ API).
    Back button redirects to the Landing Page (index2.html) with IMEI in URL.

#4. Django Backend Overview (Based on settings.py)
==================================================
    1. Framework: Django 5.1.1
    2. Database: PostgreSQL
    3. Static & Media files: AWS S3 Bucket
    4. Apps: core, rest_framework, corsheaders
    5. Logging: Enabled (logs saved to upload_logs.log)
    6. CORS: Configured via environment variables (.env)
    7. Cron Jobs: Daily cleanup task via django-crontab
    8. CSRF Protection: Trusted Origin https://feelings.zaisha.co.in

#5. How to Run
==============
git clone <repo-url>

cd <project-folder>

pip install -r requirements.txt

python manage.py migrate

python manage.py runserver

#6. Notes
==========
    NFC Support Required: Use latest Chrome (Android) or Edge (Windows) with NFC hardware.
    AWS S3: Used for storing uploaded media.
    Security: CSRF protection, AWS credential management via environment variables.
    IMEI: Passed in all pages for device identification.
    PostgreSQL: Database in use (zaisha_memory_db).
