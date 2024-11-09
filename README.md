# Varta.Ai - Walmart Hackathon 2024 Submission Project

## Problem Statement:
Build a next-generation multi-lingual virtual customer service solution powered by Large Language models (LLM) and Deep learning algorithms. The goal is to enable seamless, natural communication over the phone, offering quicker query resolution without the limitations of traditional chatbots. Implement sentiment analysis to understand customer emotions better and adjust the agent's responses accordingly, improving the overall experience and service quality. By implementing LLM, Gen AI, IVR, and Text-to-Speech capabilities, **Walmart** can streamline customer support while optimizing costs.

#### Video Demo Link:
[Video]([https://youtu.be/1stubbPNa3Y](https://www.youtube.com/watch?v=ajDkF7C_yow])

#### Team: Varta.Ai (Walmart Hackathon 2024)
- Aditya Garg
- Mehul Gupta
- Parteek Goyal
- Harshit

---

## Features:
- Provides seamless, natural conversational flow over the phone with a live conversational agent.
- Can fetch data from real-time Walmart databases and input it into LLM for rich outputs.
- Implements sentiment analysis on the go, transferring the call to an agent if the sentiment becomes negative.
- Provides enriched data for analysis, including call transcripts, conversation trackers, feedback, interactive charts, and more.
- Available 24x7 with multi-lingual support.
- Easily configurable to adapt to Walmart-specific requirements and integrate with existing systems.
- Streamlines customer support for Walmart while optimizing operational costs.

---

## Technologies Used:
- **Large Language Model (LLM):** Powered by Gemini, providing intelligent responses.
- **Python:** Primary programming language used for developing the backend.
- **React:** Used for developing the frontend interface.
- **Socket.IO:** For real-time, bidirectional communication between the client and server.
- **Google Text-to-Speech and Speech-to-Text:** For converting text to speech and vice versa.
- **FFmpeg:** For audio processing.
- **Streamlit:** For building the agent analysis dashboard.
- **Sentiment Analysis:** Using the Hubert-base-superb model to analyze sentiments.
- **MongoDB:** Used as a temporary backend solution, to be integrated with existing systems.
- **FAISS Embeddings:** For handling text embeddings efficiently and quick querying.
- **AWS Services:** For hosting and scaling the application. (To be implemented)

---

## Implementation Details:

Our project architecture is designed to efficiently handle customer queries through a seamless integration of various services. Here's a detailed walkthrough:

### 1. Customer Query Initiation:
   - The process begins when a customer makes a query, which is captured as an audio input.

### 2. Parallel Processing Services:
   - The customer's audio is simultaneously passed to three key services:
     - **LLM Agent Service**
     - **Logging Service**
     - **Sentiment Analysis Service**

### 3. LLM Agent Service:
   - **Speech-to-Text Conversion:** The user's speech is converted to text using advanced Speech-to-Text technology.
   - **Text Processing by LLM:** The transcribed text is processed by our pre-trained Large Language Model (LLM), which has been trained on customer call recordings and Walmart help documents to generate accurate and relevant responses.
   - **Text-to-Speech Conversion:** The AI-generated response is then converted back into speech and sent to the customer's phone.

### 4. Sentiment Analysis Service:
   - **Sentiment Detection:** The system performs sentiment analysis on the user's speech. If negative sentiment (such as frustration or anger) is detected, the call is forwarded to a human agent.
   - **Positive/Neutral Sentiment Handling:** If the sentiment is positive or neutral, the automated system continues to interact with the customer to resolve their query.

### 5. Logging Service:
   - **Conversation Logging:** All conversations are logged with conversational trackers that monitor and store keywords and phrases used during the call, tracking the customer's topics of interest.
   - **Keyword Tracking:** For example, tracking words like "sale," "great," or "Indian" helps us analyze interest in Walmart events like the Great Indian Sale.
   - **Data Storage:** The logging service stores call recordings and transcriptions in a database for future analysis.

---

### Low-Level Process:
The architecture follows a two-step process:

#### 1. *Verification Chain*:
This step ensures that the agent is speaking to the account owner. It can call three different functions:
   - If the user fails verification, the call is terminated.
   - If the user is successfully verified, the call is transferred to the **During Call Chain**.
   - If real-time data is required, the Verification Chain can query Walmart's database in real time.

#### 2. *During Call Chain*:
This step is responsible for addressing and resolving the user’s query. It can call four different functions:
   - Requesting user data from the database.
   - Fetching documents from the vector store, handled by **FAISS**.
   - Transferring the call to the agent.
   - Terminating the call.

All of this happens in real time.

---

## Audio Demos with Different Scenarios:

### 1. Good Case Complete Call:
   - [Audio Link](https://github.com/aditygrg2/ivr-llm/raw/main/sample-audios/MainSampleTechnicalAudio.mp3)

### 2. Intelligent Model:
   - [Audio Link](https://github.com/aditygrg2/ivr-llm/raw/main/sample-audios/7AnUnderstandingAgent.mp3)

### 3. Call with an Angry/Frustrated Customer:
   - [Audio Link](https://github.com/aditygrg2/ivr-llm/raw/main/sample-audios/Frustration1.mp3)

### 4. Crucial Operations Handled by a Real Agent:
   - [Audio Link](https://github.com/aditygrg2/ivr-llm/raw/main/sample-audios/6Successful_Termination.mp3)

---

---

## Setting Up Project


- Clone the project
  
```
git clone https://github.com/aditygrg2/ivr-llm

cd ivr-llm
```
- Create environment file

```
cp .sample.env .env
```

### For Linux/MacOS

#### Starting Frontend Server

- follow steps given in `amazon-frontend` [here](https://github.com/aditygrg2/ivr-llm/blob/main/amazon-frontend/README.md)

#### Starting Call Analysis Dashboard Server

- follow steps given in `amazon-streamlit` [here](https://github.com/aditygrg2/ivr-llm/blob/main/amazon-streamlit/README.md)


#### Starting backend Server

- Go to the root directory of the project

- Install the python libraries

```
pip install -r req.txt
```
> Note: The recommended python version is 3.10.x

- Install `ffmpeg`

In linux run:
```
sudo apt-get install ffmpeg
```

In Mac run:
```
brew install ffmpeg
```

- Start the server

```
python app.py
```
- Server will be started at http://localhost:8000

### Creating Credentials for Gemini API

- Steps:

1. Setup Vertex AI: https://cloud.google.com/vertex-ai/docs/start/cloud-environment
2. Create ADC Credentials: https://cloud.google.com/docs/authentication/provide-credentials-adc
3. Setup the environment variable. An example Application Developer Credentials file is present as an example [here](.sample.application_default_credentials.json)
