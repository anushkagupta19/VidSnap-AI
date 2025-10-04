🎬 VidSnap AI: Automated Video Reel Generator
VidSnap AI is a full-stack Python application that automatically transforms user-submitted images and text descriptions into engaging, ready-to-share social media video reels. This project leverages AI-powered text-to-speech and powerful media manipulation tools to create a seamless, end-to-end content creation pipeline.

✨ Features
Web-Based Interface: A simple and intuitive web interface built with Flask for users to upload images and enter text.

AI-Powered Narration: Integrates the ElevenLabs API to generate high-quality, human-like audio from user-provided text.

Automated Video Assembly: Uses FFmpeg to programmatically combine the generated audio with uploaded images, creating a vertically formatted (1080x1920) video reel.

Asynchronous Background Processing: A dedicated script handles the heavy lifting of audio generation and video encoding in the background, ensuring the web interface remains fast and responsive.

Unique Project Management: Assigns a unique UUID to each submission, creating an organized and robust file management system for handling multiple projects simultaneously.

🛠️ Tech Stack
Backend: Python, Flask

AI Services: ElevenLabs API (for Text-to-Speech)

Media Processing: FFmpeg

Frontend: HTML, CSS, JavaScript (implied for the web interface)

Core Libraries: uuid, werkzeug

📂 Project Structure
├── main.py                 # Main Flask web server for handling uploads
├── generate_process.py     # Background script for processing the queue
├── text_to_audio.py        # Module for interacting with the ElevenLabs API
├── config.py               # Configuration file for API keys
├── requirements.txt        # Python dependencies
│
├── user_uploads/           # Directory where user content is stored temporarily
│   └── [UUID]/
│       ├── image1.jpg
│       ├── desc.txt
│       └── ...
│
├── static/
│   └── reels/              # Directory where final videos are saved
│       └── [UUID].mp4
│
└── templates/
    └── index.html          # HTML for the user interface
⚙️ How It Works
A user visits the web application and uploads one or more images and a text description.

The Flask (main.py) server receives the files, generates a unique UUID for the project, and saves the images and text into a new directory within user_uploads/.

The background script (generate_process.py) runs continuously, scanning the user_uploads/ directory for new projects that haven't been processed yet.

When a new project is found, the script calls the text_to_audio.py module, which sends the user's text to the ElevenLabs API to generate an audio file.

Once the audio is generated, the script uses a powerful FFmpeg command to combine the audio with the user's images, creating a properly formatted video reel.

The final video is saved in the static/reels/ directory, and the project's UUID is marked as "done" to prevent reprocessing.

🚀 Installation and Setup
Prerequisites
Python 3.x

FFmpeg installed and accessible from the command line.

An API key from ElevenLabs.

Local Setup
Clone the repository:

Bash

git clone https://github.com/your-username/vidsnap-ai.git
cd vidsnap-ai
Create and activate a virtual environment:

Bash

python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
Install the required dependencies:

Bash

pip install -r requirements.txt
Configure your API Key:

Open the config.py file.

Replace the placeholder with your actual ElevenLabs API key:

Python

ELEVENLABS_API_KEY = "your_elevenlabs_api_key_here"
Run the application:

You will need to run two processes in separate terminal windows.

Terminal 1 (Flask Web Server):

Bash

python main.py
Terminal 2 (Background Processor):

Bash

python generate_process.py
Access the application:

Open your web browser and navigate to http://127.0.0.1:5000.

📈 Future Improvements
Implement a Robust Task Queue: Replace the done.txt system with a more scalable solution like Celery and Redis for managing background tasks.

User Accounts: Add user authentication to allow users to view and manage their past creations.

More Customization: Allow users to choose different voices, background music, or video transition effects.

Error Handling: Implement more robust error handling for API failures or issues during video processing.








