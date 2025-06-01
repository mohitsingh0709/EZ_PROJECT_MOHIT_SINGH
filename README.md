Secure File Sharing System
<hr>
Backend Engineering Assessment – EZ Works
This project is a secure file sharing platform built as part of the backend developer assessment for EZ Works.
You can view the live instance here: TODO (Note: This deployment will be removed post-assessment).

It features a REST API that enables secure file upload, download, and management for two distinct user roles: Operation Users and Client Users.

<hr>
🔧 Tech Stack
Backend Framework: Flask (Python)

Database: MongoDB

Authentication: JSON Web Tokens (JWT)

File Validation: python-magic
Detects file types based on content rather than file extensions alone.

<hr>
🔐 Security Measures
Files are validated by examining their actual content, not just the extension.

Download URLs are encrypted and expire shortly after generation.

Passwords are hashed before being saved to the database.

<hr>
📌 API Overview
🔑 Authentication
POST /signup: Register a new user

GET /verify-email/<token>: Confirm a user's email

POST /login: Authenticate an existing user

📁 File Management
POST /upload: Upload a new file (restricted to Operation Users)

GET /files: Retrieve a list of uploaded files

GET /download/<file_id>: Generate a secure download link

GET /secure-download/<token>: Download file via secure token

<hr>
🚀 Potential Enhancements
Add rate limiting for API protection

Encrypt uploaded files while at rest

Define more granular role-based permissions

Integrate logging and monitoring systems

<hr>
✅ Testing
To execute the test suite:

bash
Copy
Edit
pytest -v tests/
View a previous test log: tests/test_results.log

Check the Postman run summary: assets/Secure File Sharing System.postman_test_run.json

Postman Collection: assets/Secure File Sharing System.postman_collection.json

<p align="center"> <img width="700" src="assets/Postman%20Test%20Summary.png"> </p> <hr>
⚙️ Setup Instructions
Ensure you are using Python 3.12 or higher.

Clone the repository:

bash
Copy
Edit
git clone https://github.com/yashanksingh/Secure-File-Sharing-System.git
cd Secure-File-Sharing-System
Create and activate a virtual environment:

bash
Copy
Edit
python -m venv venv
./venv/Scripts/activate  # Use `source venv/bin/activate` on Linux
Install required packages:

bash
Copy
Edit
pip install -r requirements.txt
pip install python-magic-bin~=0.4.14  # For Windows
sudo apt update && sudo apt install -y libmagic-dev  # For Linux
Environment configuration:
Create a .env file in the root directory with:

env
Copy
Edit
SECRET_KEY=your_secret_key
MONGO_URI=your_mongodb_uri
UPLOAD_FOLDER=path_to_upload_folder
SMTP2GO_API_KEY=your_smtp2go_api_key
SMTP2GO_SENDER='sender_name <sender_email>'
BASE_URL=  # Optional: base URL or leave empty for localhost
Run the app:

bash
Copy
Edit
python run.py
<hr>
📦 Docker Deployment
Dockerfile
Add a Dockerfile in the root folder:

dockerfile
Copy
Edit
FROM python:3.12-slim
WORKDIR /SFSS
COPY . .
RUN pip install -r requirements.txt
RUN apt update && apt install -y libmagic-dev
RUN pip install waitress
RUN mkdir uploads
EXPOSE 5000
CMD ["waitress-serve", "--port=5000", "--call", "app:create_app"]
.dockerignore
Prevent unnecessary files from being copied:

markdown
Copy
Edit
.idea/
venv/
.pytest_cache
*.pyc
__pycache__/
.git/
.gitignore
uploads/
tests/
README.md
Dockerfile
.dockerignore
Build the image:

bash
Copy
Edit
sudo docker build -t sfss .
Run the container:

bash
Copy
Edit
sudo docker run --name sfss -d -p 5000:5000 -v $(pwd)/uploads:/uploads sfss
-d: Run in detached mode

-p: Expose port 5000

-v: Mount local uploads/ to container

Access the App:
Visit: http://localhost:5000

<hr>
🤝 Contributing
While this project was developed for a one-time assessment, feel free to raise issues or suggest improvements via pull requests.

<hr>
📄 License
This project is open-sourced under the MIT License.