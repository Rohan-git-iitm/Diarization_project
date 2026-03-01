# Diarization_project

Here is a comprehensive GitHub repository description and README draft for your SpeechSeek project, highlighting its advanced multimodal capabilities.

SpeechSeek: End-to-End Speaker Diarization & Conversational Analysis
SpeechSeek is a robust, AI-powered audio processing pipeline that performs speaker diarization, multilingual Automatic Speech Recognition (ASR), Language Identification (LID), and emotion detection. Built with a focus on code-switched Indian languages, it leverages state-of-the-art acoustic models and LLM-based contextual correction to generate highly accurate, rich conversation transcripts.

✨ Key Features
Intelligent Speaker Diarization: Uses Naturalspeech3's FACodec for acoustic feature extraction, combined with adaptive angular distance clustering and chunk-based reassignment to accurately track who is speaking.

Multilingual LID & ASR: Integrates a custom 6-Language Identification model (English, Hindi, Tamil, Telugu, Marathi, Kannada) to dynamically prompt openai/whisper-medium, ensuring accurate transcription even during complex code-switching.

Segment-Level Emotion Detection: Utilizes a custom QFormerBridge mapped to CLAP embedding space to classify the speaker's emotional state (Happy, Sad, Anger, Fear, Disgust, Surprise) for every utterance.

LLM-Powered Contextual Refinement: Passes the raw segment metadata and the full audio to Gemini 2.0 Flash to intelligently verify speaker identities based on conversational turn-taking, correct minor ASR hallucinations, and seamlessly format the final output.

Interactive Web UI: Includes a deployed Gradio interface for easy microphone recording or file uploading.

🧠 Model Architecture & Tech Stack
Acoustic & Semantic Extraction: Amphion FACodec, SpeechTokenizer

Transcription: Hugging Face Transformers, Whisper-Medium

Emotion & Language Custom Models: PyTorch, Custom Q-Former, Custom CNN-based LID Classifier

LLM Integration: Google GenAI SDK (Gemini API)

UI: Gradio
