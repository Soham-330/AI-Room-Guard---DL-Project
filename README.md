# AI-Room-Guard---DL-Project
AI Room Guard – Voice and Vision Based Security System
Overview

This project implements an AI-powered security system that activates through a spoken command, recognizes known individuals, and escalates responses when an unknown person is detected. The system combines voice activation, face recognition, and automated alerts to function as a virtual room guard.

The implementation is divided into three main milestones:

Voice Activation – Speech-based system activation.

Face Recognition – Enrollment and identification of trusted individuals.

Intelligent Escalation – Automated warning and alert system using an LLM and email notifications.

Features
Milestone 1: Activation and Basic Input

Detects a spoken command such as “guard my room”.

Converts uploaded audio to text using the speech_recognition library.

Switches Guard Mode ON or OFF based on recognized commands.

Provides audio feedback using gTTS.

Milestone 2: Face Enrollment and Recognition

Allows enrollment of trusted faces using DeepFace (Facenet model).

Stores extracted embeddings in a pickle file.

Recognizes known vs. unknown faces in uploaded images or videos.

Annotates videos with bounding boxes:

Green for known faces.

Red for unknown faces.

Saves the annotated video for later review.

Milestone 3: LLM-based Escalation and Alerts

Monitors uploaded video and detects persistent unknown faces.

Uses Google Gemini (LLM) to generate context-aware escalation messages.

Converts these messages to speech.

Sends an automated email alert if the unknown person remains in view for a set duration.

Saves the final annotated video with warning text overlays.

Dependencies

Install the required packages before running the script:

pip install speechrecognition pydub gtts mediapipe opencv-python playsound deepface google-generativeai
apt-get install -y ffmpeg mpg123

How It Works
1. Voice Activation

Upload an audio file (e.g., command.m4a or command.wav) that contains the activation phrase.
If the phrase “guard my room” is detected, Guard Mode will activate.

2. Face Enrollment

Upload an image of a trusted individual:

feat, name = enroll_face()
save_faces([feat], [name])


The system extracts embeddings using DeepFace and stores them for future recognition.

3. Guard Mode with Escalation

Once Guard Mode is active:

Upload a video for monitoring.

The system identifies faces in each frame.

Unknown faces trigger escalation:

Initial polite warning.

Stronger message after 5 seconds.

Final escalation with email alert.

The annotated output video is saved in:

/content/Files/guard_out.mp4

Configuration

Before running Milestone 3 (escalation and alerts), set the following credentials in Colab or your environment:

userdata.set('SENDER_EMAIL', 'your_email@gmail.com')
userdata.set('SENDER_PASSWORD', 'app_password')
userdata.set('OWNER_EMAIL', 'recipient_email@gmail.com')
userdata.set('API_KEY', 'your_gemini_api_key')


These values enable the email and LLM integration.
