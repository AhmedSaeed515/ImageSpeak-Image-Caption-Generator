# ImageSpeak – AI Image Caption Generator

> An end-to-end AI system that automatically generates meaningful natural language descriptions for images — combining Computer Vision, Vision Transformers, and NLP into a seamless Flutter-powered experience.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-orange?style=flat-square&logo=pytorch)
![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?style=flat-square&logo=flutter)
![Flask](https://img.shields.io/badge/Flask-REST%20API-lightgrey?style=flat-square&logo=flask)
![GCP](https://img.shields.io/badge/GCP-Cloud%20Deployed-4285F4?style=flat-square&logo=googlecloud)
![License](https://img.shields.io/badge/License-Academic-green?style=flat-square)

---

## Overview

**ImageSpeak** is an AI-powered image caption generation system developed as a graduation project at Ain Shams University (2024). It automatically generates fluent, descriptive captions for any uploaded image using a Vision Transformer encoder and a BERT-based language decoder, deployed via a Flask REST API and consumed through a cross-platform Flutter mobile application.

---

## How It Works

```
User uploads image
       │
       ▼
Flutter App  ──(HTTP POST)──▶  Flask Backend (GCP)
                                      │
                                      ▼
                           Vision Transformer (ViT)
                           Splits image into patches,
                           extracts contextual features
                                      │
                                      ▼
                           Language Decoder
                           (BERT Tokenizer + GloVe Embeddings)
                           Generates caption token-by-token
                           via cross-attention over visual features
                                      │
                                      ▼
                           Caption returned as JSON
                                      │
                                      ▼
                           Displayed in Flutter UI
```

### Vision Encoder (ViT)

The image is divided into fixed-size patches (e.g. 16×16 pixels), linearly embedded, and fed into a Transformer encoder. Multi-head self-attention allows the model to capture global spatial relationships across the entire image — far beyond what local CNNs handle.

### Language Decoder

Image feature vectors from the ViT encoder are passed to an autoregressive decoder initialized with a BERT tokenizer and enhanced with GloVe word embeddings. The decoder generates one token at a time using cross-attention over the visual features to produce fluent, descriptive captions.

---

## Features

- **Automatic caption generation** — Upload any image, receive a human-readable description generated entirely by the AI pipeline
- **ViT patch attention** — Divides images into patches and applies multi-head self-attention for global scene understanding
- **Flutter frontend** — Polished cross-platform mobile UI built with Flutter and designed in Figma
- **GCP cloud deployment** — Flask API hosted on Google Cloud Platform for scalable, reliable inference
- **REST API integration** — Clean endpoint design: POST an image, receive a caption as JSON
- **Large-scale training** — Trained on Flickr30k and MS COCO benchmark datasets

---

## Tech Stack

### AI & Machine Learning
| Component | Description |
|---|---|
| `VisionEncoderDecoderModel` | End-to-end encoder-decoder architecture |
| `Vision Transformer (ViT)` | Image feature extraction via patch embeddings |
| `BERT Tokenizer` | Subword tokenization for caption generation |
| `GloVe Embeddings` | Pre-trained word representations |
| `PyTorch` | Deep learning framework |

### Backend
| Component | Description |
|---|---|
| `Flask` | Lightweight Python web framework |
| `REST API` | JSON-based image upload and caption response |
| `Image preprocessing` | Resize, normalize, patch extraction pipeline |

### Frontend
| Component | Description |
|---|---|
| `Flutter (Dart)` | Cross-platform mobile application |
| `Figma` | UI/UX design and prototyping |
| `HTTP client` | REST API integration for image upload |
| `Image Picker` | Native gallery and camera access |

### Cloud
| Component | Description |
|---|---|
| `Google Cloud Platform` | Hosting and deployment |
| `Cloud Run / App Engine` | Serverless container deployment |
| `Docker` | Containerization for portable deployment |
| `HTTPS` | Secure API exposure |

---

## Datasets

### Flickr30k
- **31,783 images** with **158,915 captions** (5 captions per image)
- Covers everyday scenes: people, animals, activities, and objects
- Diverse natural language annotations written by crowd workers
- Widely used benchmark for sentence-based image description tasks

### MS COCO (Microsoft Common Objects in Context)
- **330,000+ images** with **1.5 million+ captions**
- **80 object categories** across complex real-world scenes
- Standard large-scale dataset for image captioning, detection, and segmentation
- Rich visual diversity across activities, environments, and objects

---

## Project Architecture

```
ImageSpeak/
├── backend/
│   ├── app.py                  # Flask API entry point
│   ├── model/
│   │   ├── encoder.py          # ViT encoder wrapper
│   │   ├── decoder.py          # BERT-based caption decoder
│   │   └── caption_model.py    # VisionEncoderDecoderModel integration
│   ├── utils/
│   │   └── preprocessing.py    # Image resize, normalize, patch extraction
│   └── requirements.txt
├── frontend/
│   └── lib/
│       ├── main.dart           # Flutter app entry
│       ├── screens/
│       │   └── home_screen.dart
│       └── services/
│           └── api_service.dart  # HTTP client for caption API
├── Dockerfile
└── README.md
```

---

## Installation

### Prerequisites

- Python 3.10+
- Flutter SDK 3.x
- pip / virtualenv
- Node.js (optional, for tooling)

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ImageSpeak.git
cd ImageSpeak
```

### 2. Install Python Dependencies

```bash
cd backend
pip install -r requirements.txt
```

### 3. Run the Flask Server

```bash
python app.py
# Server starts at http://localhost:5000
```

### 4. Run the Flutter Application

```bash
cd frontend
flutter pub get
flutter run
```

### 5. Docker Deployment (GCP)

```bash
docker build -t imagespeak-api .
docker run -p 5000:5000 imagespeak-api
```

---

## API Reference

### `POST /caption`

Upload an image and receive a generated caption.

**Request**
```bash
curl -X POST https://<your-api>/caption \
  -F "image=@photo.jpg"
```

**Response**
```json
{
  "caption": "A dog running on a grassy field near a lake.",
  "confidence": 0.87,
  "processing_time_ms": 320
}
```

**Status Codes**
| Code | Meaning |
|---|---|
| `200` | Caption generated successfully |
| `400` | Invalid or missing image file |
| `500` | Internal model inference error |

---

## Future Improvements

- **Multi-language captions** — Extend output to Arabic, French, and other languages via multilingual NLP models
- **Real-time captioning** — Stream live camera frames through the pipeline for on-device or low-latency captioning
- **Voice output** — Text-to-speech integration for accessibility, reading captions aloud to visually impaired users
- **Improved accuracy** — Fine-tune on larger datasets and explore newer encoder-decoder architectures (BLIP, OFA, LLaVA)
- **User history** — Save and manage previous caption generations with cloud sync across devices
- **Caption customization** — Allow users to adjust verbosity, tone (formal / casual), and detail level of generated captions
- **Batch processing** — Support uploading multiple images and generating captions in bulk via API

---

## Authors

**Ahmed Saeed** — Computer Science & Information Systems, Ain Shams University, Class of 2024

---

## License

This project was developed as a Graduation Project for academic purposes.
