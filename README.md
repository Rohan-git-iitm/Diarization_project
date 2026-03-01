# 🎙️ SpeechSeek

**SpeechSeek** is an advanced, end-to-end audio processing pipeline designed for comprehensive conversational analysis. It combines state-of-the-art acoustic modeling, multilingual Automatic Speech Recognition (ASR), and Large Language Models (LLMs) to perform robust speaker diarization, transcription, language identification, and emotion detection—specifically optimized for code-switched Indian languages.

## ✨ Key Features

* **Intelligent Speaker Diarization:** Utilizes Naturalspeech3's FACodec for high-dimensional acoustic feature extraction, paired with an adaptive angular distance clustering algorithm and chunk-based reassignment to accurately track distinct voices.
* **Multilingual LID & ASR:** Features a custom 6-Language Identification model (English, Hindi, Tamil, Telugu, Marathi, Kannada) that dynamically prompts `openai/whisper-medium`. This ensures highly accurate transcription, even during complex code-switching scenarios.
* **Segment-Level Emotion Detection:** Employs a custom `QFormerBridge` mapped to the CLAP embedding space to classify the speaker's emotional state across 6 categories (Happy, Sad, Anger, Fear, Disgust, Surprise) for every single utterance.
* **LLM-Powered Contextual Refinement:** Passes raw segment metadata and complete audio context to **Google Gemini** to intelligently verify speaker identities based on turn-taking, correct minor ASR hallucinations, and seamlessly format the final output.
* **Interactive Web UI:** Includes a deployed Gradio interface for seamless microphone recording or audio file uploading.

## 🧠 Architecture & Tech Stack

* **Acoustic & Semantic Extraction:** [Amphion FACodec](https://github.com/open-mmlab/Amphion), [SpeechTokenizer](https://github.com/ZhangXInFD/SpeechTokenizer)
* **Transcription:** Hugging Face `transformers`, `openai/whisper-medium`
* **Custom Models:** PyTorch-based Q-Former, CNN-based LID Classifier
* **LLM Integration:** Google GenAI SDK (Gemini 2.0 Flash / 2.5 Pro)
* **UI & Deployment:** Gradio

## ⚙️ How It Works

1. **Audio Ingestion:** The user uploads or records audio via the Gradio UI. The audio is normalized and resampled to 16kHz mono.
2. **Feature Extraction:** The audio is chunked into sliding windows. FACodec extracts high-dimensional speaker embeddings.
3. **Clustering:** Embeddings are clustered using a custom adaptive angular distance algorithm to map out raw speaker segments.
4. **Diarized Processing:** * The LID model detects the language of each segment.
    * Whisper transcribes the audio using the detected language as a prompt.
    * The Q-Former model assigns an emotion label.
5. **LLM Formatting:** Gemini acts as the final adjudicator, listening to the full audio context to merge broken segments, fix transcription anomalies, and output a clean, readable transcript in the format: `(start-end) speaker: text (emotion)`.
