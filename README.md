# ResumeXtract

ResumeXtract is a professional Django project that extracts key details from resumes like the candidate's first name, email ID, and mobile number. The project utilizes Django REST Framework for the backend API, and the frontend is built with HTML for a simple and user-friendly interface.

##Features
Upload Resumes: Accepts PDF resume files for processing.
Extract Candidate Information: Extracts and displays the candidate's name, email address, and phone number from the uploaded resume.
API Endpoint: Provides a REST API to extract resume data.
User-Friendly Interface: A simple HTML frontend to upload resumes and view extracted details.
##Prerequisites
Make sure you have the following installed:

Python (version 3.8 or above)
PostgreSQL
pip (Python package manager)
##Installation and Setup
1. Clone the Repository
bash

git clone <repository-link>
cd ResumeXtract
2. Create and Activate a Virtual Environment
bash

python -m venv env
source env/bin/activate   # For Linux/MacOS
env\Scripts\activate      # For Windows
3. Install Dependencies
bash

pip install -r requirements.txt
4. Configure PostgreSQL Database
Create a PostgreSQL database named resume_xtract.
Update the DATABASES section in ResumeXtract/settings.py:
python

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'resume_xtract',
        'USER': '<your_db_user>',
        'PASSWORD': '<your_db_password>',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
5. Apply Migrations
bash

python manage.py makemigrations
python manage.py migrate
6. Run the Development Server
bash

python manage.py runserver
The server will start at http://127.0.0.1:8000/.

##API Documentation
Endpoint: /api/extract_resume/
Method: POST
Description: Accepts a resume file (PDF) and extracts the candidate's first name, email, and mobile number.
Request Parameters:
resume (file): The resume file to be processed.
##Response Example:
json

{
  "first_name": "John",
  "email": "john.doe@example.com",
  "mobile_number": "123-456-7890"
}
Example Usage
To test the API, you can use Postman or cURL to upload a resume and get the candidate's details.

##Postman:
Set the method to POST.
URL: http://127.0.0.1:8000/api/extract_resume/.
In the "Body" tab, choose "form-data" and upload a PDF file for the resume field.
cURL:
bash

curl -X POST -F "resume=@<path_to_resume>" http://127.0.0.1:8000/api/extract_resume/
##Frontend (HTML) for Uploading Resume
The frontend of this project is built with HTML, allowing users to upload a resume file and display the extracted candidate information.

html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Resume Extraction</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .container {
            max-width: 600px;
            margin: auto;
            text-align: center;
        }
        #output {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            background: #f9f9f9;
            max-height: 300px;
            overflow-y: auto;
            text-align: left;
        }
        .result-item {
            margin-bottom: 10px;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Resume Extraction</h1>
        <form id="uploadForm">
            <label for="file">Upload Resume (PDF):</label><br>
            <input type="file" id="file" name="file" accept=".pdf" required><br><br>
            <button type="submit">Extract</button>
        </form>
        <div id="output">
            <h3>Extracted Information:</h3>
            <div id="result">
                <p>No data yet...</p>
            </div>
        </div>
    </div>

    <script>
        const form = document.getElementById("uploadForm");
        const result = document.getElementById("result");

        form.addEventListener("submit", async (e) => {
            e.preventDefault(); // Prevent default form submission

            // Hardcoded output for demonstration
            const name = "John Doe";
            const email = "john.doe@example.com";
            const phone = "123456789";

            // Display the fixed output
            result.innerHTML = `
                <div class="result-item"><strong>Name:</strong> ${name}</div>
                <div class="result-item"><strong>Email:</strong> ${email}</div>
                <div class="result-item"><strong>Phone:</strong> ${phone}</div>
            `;
        });
    </script>
</body>
</html>
This simple HTML form lets users upload a resume file, and upon submission, it displays extracted information. The extraction logic will be connected to the backend for dynamic data extraction.

##Project Structure
markdown

ResumeXtract/
├── resume/
│   ├── migrations/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   ├── urls.py
│   ├── views.py
├── ResumeXtract/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
├── manage.py
├── requirements.txt
└── README.md
##Requirements
The requirements.txt file should include the following dependencies:

##shell

Django>=4.2
djangorestframework>=3.14
psycopg2>=2.9
PyPDF2>=3.0
python-docx>=0.8
Resume Parsing Logic
The backend uses Python libraries like PyPDF2 to extract text from PDF resumes and python-docx for Word document resumes. The extracted data is then processed to find patterns for names, emails, and phone numbers using regular expressions.
