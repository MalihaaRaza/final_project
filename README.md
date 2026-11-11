# Emotion Detector (Flask + Watson NLP)

A Python web app that detects the emotions in a piece of text. Enter a sentence and the app returns scores for **anger, disgust, fear, joy and sadness**, along with the **dominant emotion**.

Built as the final project for IBM's *Developing AI Applications with Python and Flask* course, starting from the [course starter repo](https://github.com/ibm-developer-skills-network/oaqjp-final-project-emb-ai). The emotion detection package, Flask server, error handling and tests are my own work.

## How it works

1. The user enters text in the web UI (`templates/index.html`).
2. The Flask server (`server.py`) receives it on the `/emotionDetector` endpoint.
3. The `EmotionDetection` package sends the text to the **Watson NLP Emotion Predict** model over a REST API.
4. The JSON response is parsed, the five emotion scores are extracted, and the highest-scoring emotion is picked as the dominant one.
5. The result is returned to the UI.

Example: for the input *"I am glad this happened"*, the app returns all five scores and reports **joy** as the dominant emotion.

## Error handling

Blank or invalid input makes the Watson API return a `400` status. The app catches this and returns `None` for every score, and the server shows *"Invalid text! Please try again!"* instead of crashing.

## Tests

`test_emotion_detection.py` uses `unittest` to check that the correct dominant emotion is detected for a sample sentence of each type (joy, anger, disgust, sadness and fear).

```bash
python -m unittest test_emotion_detection.py
```

## Project structure

```
EmotionDetection/
  __init__.py
  emotion_detection.py     # Calls Watson NLP and processes the response
server.py                  # Flask app and routes
templates/index.html       # Web UI
static/mywebscript.js      # Sends the request from the UI
test_emotion_detection.py  # Unit tests
```

## Running locally

```bash
pip install flask requests
python server.py
```

Then open [http://localhost:5000](http://localhost:5000).

> **Note:** The Watson NLP endpoint used here is hosted in the IBM Skills Network lab environment, so the emotion API calls only work from inside that environment.

## Tech stack

- **Python**, **Flask**
- **IBM Watson NLP** (Emotion Predict model) via REST API
- `requests`, `json`
- `unittest`
