# SmartNotify AI

**Personalized AI-powered notification routing using RAG, FAISS, and Google Gemini.**

SmartNotify AI is a continued development of the **Message Notification Router** hackathon challenge. It analyzes incoming messages and supporting context to recommend one of three actions:

- **Notify** — deliver important or time-sensitive messages immediately.
- **Digest** — include lower-priority messages in a summary.
- **Mute** — suppress messages that are unwanted, irrelevant, or assessed as suspicious.

The current implementation supports **text and image messages**. Voice-note transcription and processing are **not implemented**.

## Origin: Hackathon challenge and dataset

This project originated from the HackerRank Orchestrate August 2026 hackathon challenge.

- **Original challenge and dataset repository:** <https://github.com/interviewstreet/hackerrank-orchestrate-august26>
- **Original repository README:** <https://github.com/interviewstreet/hackerrank-orchestrate-august26/blob/main/README.md>

The organizers' repository is the source for the original challenge dataset and associated files. This repository does not redistribute that dataset. Obtain the files from the original source and follow any applicable license, access, and usage terms.

## What this project does

The notebook combines message content with available user and conversation context to produce a structured routing decision.

### Main capabilities

- Text-based message classification and routing.
- Structured context retrieval using user, group, business, relationship, history, events, and notification-load information where available.
- User-specific semantic retrieval using Sentence Transformers and FAISS.
- Retrieval-Augmented Generation (RAG) to provide relevant historical context to the language model.
- Google Gemini 2.5 Flash for structured routing decisions.
- Gemini Vision image analysis to extract visual descriptions and text from image attachments.
- Pydantic-based structured output containing an action, message type, reason, confidence, and supporting evidence identifiers.
- Safety-oriented handling of suspicious messages and potential credential-theft attempts.

## Architecture

1. **Input:** Load a message and identify its media type.
2. **Structured context:** Retrieve relevant user, group, business, relationship, interaction-history, event, and notification-load information.
3. **Semantic retrieval:** Use a user-specific FAISS index to retrieve similar historical messages.
4. **Multimodal enrichment:** For image messages, resolve the associated image and analyze it with Gemini Vision. Image-derived information is treated as supplementary context and should be checked for relevance to the message.
5. **RAG context:** Combine the current message with relevant structured and retrieved evidence.
6. **Decision generation:** Send the grounded context to Gemini 2.5 Flash and parse the structured response.
7. **Output:** Return a `notify`, `digest`, or `mute` decision with its explanation, confidence, message type, and evidence identifiers.

## Technology stack

- Python
- Google Colab / Jupyter Notebook
- Google Gen AI SDK
- Gemini 2.5 Flash
- Gemini Vision
- Sentence Transformers
- FAISS
- Pydantic
- Pandas and NumPy
- Pillow

## Implementation status

| Component | Status |
|---|---|
| Text-based notification routing | Implemented |
| Structured context retrieval | Implemented |
| User-specific semantic retrieval with FAISS | Implemented |
| RAG-based decision generation | Implemented |
| Gemini 2.5 Flash integration | Implemented |
| Image understanding with Gemini Vision | Implemented |
| Historical interaction-based personalization | Implemented |
| Scam and credential-theft risk considerations | Implemented |
| Voice-note transcription and processing | Not implemented |

**Scope note:** The current project supports text and image inputs. It does not claim to process voice notes or audio.

## Repository contents

```text
SmartNotify_AI/
├── SmartNotify_AI.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

The notebook is the primary implementation artifact. The original dataset and media files are intentionally not copied into this repository.

## Run in Google Colab

1. Open `SmartNotify_AI.ipynb` in Google Colab.
2. Obtain the required dataset files from the [original challenge repository](https://github.com/interviewstreet/hackerrank-orchestrate-august26).
3. Upload or mount the dataset in your Colab environment and configure the notebook's data paths.
4. Add a Colab Secret named `GEMINI_API_KEY` containing your Google Gemini API key.
5. Install the dependencies:

   ```python
   %pip install -r requirements.txt
   ```

   If you install dependencies directly in a Colab cell, ensure `requirements.txt` is available in the current Colab working directory, or install the packages listed in that file.
6. Run the notebook cells in order.

### API key handling

The notebook should retrieve the key from Colab Secrets rather than hardcoding it:

```python
from google.colab import userdata

GEMINI_API_KEY = userdata.get("GEMINI_API_KEY")
```

Never commit API keys, `.env` files, credentials, private message histories, or other sensitive data.

## Dataset and media

The dataset is maintained separately by the original challenge organizers. Download it from the original repository and provide the files locally in Colab as required by the notebook. Image processing also requires the corresponding image files to be present at the configured paths.

This GitHub repository intentionally excludes private or bulky dataset and media files. Check the original repository's terms before reusing or redistributing its contents.

## Development notes

This repository documents continued independent development after the hackathon. The original challenge and dataset belong to their respective organizers. The RAG, semantic retrieval, Gemini integration, image-processing workflow, and other implementation work in this repository should be understood in that context.

## Future improvements

Potential future work includes broader evaluation across message categories, controlled comparisons of decisions with and without image context, improved image-message relevance checks, and additional robustness testing.

---

*Built as a continued development of the HackerRank Orchestrate Message Notification Router challenge.*
