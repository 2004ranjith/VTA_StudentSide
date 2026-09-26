# Video Tutor Assist – Student Side

A learning app where students watch a lesson video, read AI-generated notes, take quizzes with AI feedback and chat about the content.

**Live demo (preview):** https://sjy-video-tutor-assist-student-side.streamlit.app/

> **Companion app:** [VTA_CreatorSide](https://github.com/2004ranjith/VTA_CreatorSide) is where teachers create the `VTA_content.json` file used here ([live demo](https://sjy-video-tutor-assist-creator-side.streamlit.app/)).

## The problem

Students often watch lecture videos passively. This app turns each video into an interactive lesson with notes, self-assessment and a Q&A chatbot grounded in the video's content.

## How it works

1. Enter a Cohere API key (validated before use).
2. Upload the `VTA_content.json` file created on the [Creator Side](https://github.com/2004ranjith/VTA_CreatorSide).
3. Watch the video and open one of three tabs:
   - **Description** – summary, notes (downloadable as Word) and additional files.
   - **Quiz** – choose Easy/Medium/Hard and answer MCQs and descriptive questions. MCQs are scored against the answer key, with an AI explanation for wrong answers; descriptive answers get an AI score out of 5 and feedback based on the summary and notes.
   - **Chatbot** – ask questions; answers use the video's summary and transcript as context.

## Tech stack

- **Python**, **Streamlit** (+ streamlit-option-menu) – web UI and chat interface
- **Cohere** (Command models via the Generate API) – explanations, answer evaluation and chatbot
- **python-docx** – Word notes download
- **JSON / base64** – loading content from the creator app

## Project structure

```
stu.py           # Streamlit entry point: video, notes, quiz, evaluation, chatbot
json_upload.py   # Upload and parse the VTA JSON file
api_call.py      # Cohere API key input and validation
requirements.txt
```

## Run locally

Requires a **Cohere API key** ([get one here](https://dashboard.cohere.com/api-keys)), entered in the app. (ffmpeg is only needed for the Creator Side.)

```bash
pip install -r requirements.txt
streamlit run stu.py
```

## Limitations and future improvements

- Each user needs their own Cohere API key; a backend service with login would simplify access.
- Content is shared as a single JSON file; a database with user accounts would enable progress tracking and analytics.
- The chatbot and grader place the full summary/transcript in the prompt; retrieval (RAG) with citations or timestamps would improve grounding for longer videos.
- AI grading of descriptive answers could be calibrated against teacher grades and made more consistent with lower temperature and rubrics.
- Quiz parsing depends on the LLM output format; stricter validation on the creator side would prevent errors.

## Team

Built as a B.Tech team project at SRM Institute of Science and Technology, Ramapuram.

Team: SJ Yogesh ([github.com/sjyogesh23](https://github.com/sjyogesh23)) and B.S Ranjith ([github.com/2004ranjith](https://github.com/2004ranjith)).
