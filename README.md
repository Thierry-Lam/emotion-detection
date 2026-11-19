# Watson NLP Emotion Detection

A small Python application that sends English text to an IBM Watson NLP
EmotionPredict service and returns scores for anger, disgust, fear, joy and
sadness, plus the dominant emotion. A Flask interface exposes the detector.

## Project structure

```text
EmotionDetection/
├── README.md
├── emotion_detection.py
├── server.py
├── test_emotion_detection.py
├── requirements.txt
└── EmotionDetection/
    ├── __init__.py
    └── emotion_detection.py
```

## Setup

Python 3.10 or later is recommended.

```bash
python -m venv .venv
# macOS/Linux:
source .venv/bin/activate
# Windows PowerShell:
# .venv\Scripts\Activate.ps1

pip install -r requirements.txt
```

Configure the Watson NLP service URL supplied by your course/lab environment.
Do not commit credentials or private endpoint details.

```bash
# macOS/Linux
export WATSON_NLP_URL="YOUR_WATSON_NLP_EMOTIONPREDICT_ENDPOINT"

# Windows PowerShell
$env:WATSON_NLP_URL = "YOUR_WATSON_NLP_EMOTIONPREDICT_ENDPOINT"
```

The default model ID is `emotion_aggregated-workflow_lang_en_stock`.
If your lab specifies a different model ID, set `WATSON_NLP_MODEL_ID`.

## Run the detector

```bash
python -c "from emotion_detection import emotion_detector; print(emotion_detector('I am happy today'))"
```

Expected result shape (the numeric values depend on the service response):

```python
{
    "anger": 0.0,
    "disgust": 0.0,
    "fear": 0.0,
    "joy": 0.0,
    "sadness": 0.0,
    "dominant_emotion": "joy"
}
```

## Validate the package

Run this from the repository root:

```bash
python -c "from EmotionDetection import emotion_detector; print(callable(emotion_detector))"
```

Expected output: `True`.

## Run unit tests

The tests mock the HTTP service, so they do not require a live Watson endpoint:

```bash
python -m unittest -v
```

## Run Flask

```bash
python server.py
```

Open `http://127.0.0.1:5000/` in a browser, enter text, and select **Analyze**.
The `/emotionDetector?textToAnalyze=...` endpoint also accepts GET requests.
A blank input returns HTTP 400 with a clear validation message.

## Static analysis

Run Pylint against the requested server module:

```bash
pylint server.py
```

Also useful:

```bash
pylint emotion_detection.py test_emotion_detection.py EmotionDetection/
```

Record the score printed by your own Pylint run. Do not report a 10/10 score
unless your local output actually shows it.

## Submission evidence checklist

- [ ] Public GitHub URL to `README.md`
- [ ] `emotion_detection.py` source
- [ ] Terminal capture of successful import and live service test
- [ ] Formatted detector source and terminal result
- [ ] Public GitHub URL to `EmotionDetection/__init__.py`
- [ ] Terminal capture validating package import
- [ ] `test_emotion_detection.py` source and passing test output
- [ ] `server.py` source and browser screenshot `6b_deployment_test.png`
- [ ] HTTP 400 handling source and blank-input screenshot
      `7c_error_handling_interface.png`
- [ ] `pylint server.py` command and actual terminal score

Screenshots must be captured from your own running application and terminal.
