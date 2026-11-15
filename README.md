# SmartNotify AI

**Personalized AI-powered notification management using RAG, FAISS, and Gemini.**

SmartNotify AI is an intelligent notification routing system that analyzes incoming messages and determines whether they should be delivered immediately, included in a digest, or muted.

Instead of treating every message equally, it uses message content, user preferences, historical interactions, and multimodal information to make personalized notification decisions.

## Key Features

- **Personalized routing:** Classifies messages into Notify, Digest, or Mute.
- **RAG pipeline:** Retrieves relevant user-specific historical messages and interaction events.
- **Semantic retrieval:** Uses Sentence Transformers and FAISS to find similar historical messages.
- **Context-aware decisions:** Considers sender, group, business relationship, notification load, and user history.
- **Image understanding:** Uses Gemini Vision to extract descriptions and text from image attachments.
- **Structured output:** Uses Pydantic to generate consistent routing decisions.
- **Scam awareness:** Identifies suspicious messages and potential credential-theft attempts.

## Architecture

1. Incoming message processing.
2. Structured context retrieval.
3. User-specific semantic retrieval using FAISS.
4. Relevant history and interaction-event retrieval.
5. RAG context construction.
6. Gemini-based message analysis.
7. Structured routing decision.

## Technology Stack

- Python
- Google Gemini 2.5 Flash
- Google Gemini Vision
- Retrieval-Augmented Generation (RAG)
- Sentence Transformers
- FAISS
- Pydantic
- Pandas
- Google Colab

## Routing Categories

| Action | Description |
|---|---|
| Notify | Deliver important or time-sensitive messages immediately |
| Digest | Include lower-priority messages in a summary |
| Mute | Suppress unwanted, irrelevant, or suspicious messages |

## Project Structure

```text
SmartNotify_AI/
├── SmartNotify_AI.ipynb
├── README.md
└── requirements.txt
```

## Running the Project

1. Open the notebook in Google Colab.
2. Configure your `GEMINI_API_KEY` using Colab Secrets.
3. Provide the required datasets and image files in the expected locations.
4. Install the required Python dependencies.
5. Run the notebook cells sequentially.
6. Test incoming messages and inspect their routing decisions.

**Note:** The dataset and image files are not included in this public repository. You must provide the required data separately.

## Security

- API keys are stored using Google Colab Secrets.
- Private datasets and personal message histories should not be committed to the repository.
- Incoming messages and extracted image text are treated as untrusted input.

## Current Status

The project includes text-based routing, user-specific semantic retrieval, RAG-based decision-making, and Gemini Vision integration. Further evaluation focuses on multimodal relevance, routing accuracy, and personalized notification behavior.
