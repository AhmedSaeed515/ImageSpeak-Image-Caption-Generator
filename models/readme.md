# Image Caption Generator using Attention Mechanism

## Overview

This project implements an Image Caption Generator that automatically generates natural language descriptions for images. The model combines Computer Vision and Natural Language Processing techniques by extracting visual features from images using a pre-trained VGG16 network and generating captions with an Attention-based Encoder-Decoder architecture.

## Features

* Automatic image caption generation
* VGG16-based image feature extraction
* Bahdanau Attention mechanism
* LSTM-based caption decoder
* Text preprocessing and tokenization
* Training and evaluation on the Flickr8k dataset
* Visualization of generated captions

## Dataset

The model is trained using the Flickr8k dataset, which contains:

* 8,000 images
* 5 captions per image
* Diverse real-world scenes and objects

## Model Architecture

### Encoder

* Pre-trained VGG16 (without classification layers)
* Extracts image feature vectors

### Attention Layer

* Bahdanau Attention
* Enables the model to focus on important image regions while generating captions

### Decoder

* Embedding Layer
* LSTM Network
* Dense Output Layer with Softmax activation

## Technologies Used

* Python
* TensorFlow / Keras
* NumPy
* Pandas
* Matplotlib
* OpenCV
* PIL

## Workflow

1. Load and preprocess image captions.
2. Clean and tokenize text data.
3. Extract image features using VGG16.
4. Train the Attention-based Encoder-Decoder model.
5. Generate captions for unseen images.
6. Evaluate model performance.

## Project Structure

```text
├── Dataset/
│   ├── Flickr8k_Dataset
│   └── Flickr8k.token.txt
├── notebooks/
│   ├── Image_caption_using_attention_V2.ipynb
│   └── BEST_of_Image_caption_using_attention.ipynb
├── saved_models/
├── outputs/
└── README.md
```

## Installation

```bash
git clone <repository-url>
cd Image-Caption-Generator
pip install -r requirements.txt
```

## Running the Project

Open and run the notebook:

```bash
jupyter notebook Image_caption_using_attention_V2.ipynb
```

or

```bash
jupyter notebook BEST_of_Image_caption_using_attention.ipynb
```

## Future Improvements

* Use Transformer-based architectures (ViT, BLIP)
* Train on Flickr30k and MS COCO datasets
* Deploy as a web application
* Add multilingual caption generation
* Improve caption quality with larger language models

## Author

Ahmed Saeed

## License

This project was developed for educational and research purposes.
