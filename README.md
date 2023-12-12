<p align="center">
  <img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/logo.png" alt="modaCLIP Logo" width="350" height="350" />
</p>

# Overview
ModaCLIP is a smart multimodal Information and image retrieval engine fueled by OpenAI's [CLIP](https://openai.com/blog/clip/)  that effortlessly connects text and images for lightning-fast info retrieval. This implementation combines the prowess of OpenAI's CLIP model with a curated dataset from Unsplash (1000 Images from various themes) to enable an innovative information retrieval system that comprehends the relationships between images and text.

# Project Summary 
In this project, OpenAI's CLIP model is used which is a neural network designed to understand the intricate connections between images and text. Unlike conventional keyword-based approaches the system's strength lies in its cross-modal understanding, enabling seamless matching of images with textual queries and vice versa. This unique capability offers a more nuanced and context-aware retrieval process.

Summary of the codes in each of the project files - 

- `prepare_unsplash_dataset.ipynb` - Use the curated metadata of unsplash images from `unsplash-metadata.json`to create a dataframe of images with these metadata - 
```
[
  {
    "photo_id": "wud-eV6Vpwo",
    "photo_url": "https://unsplash.com/photos/wud-eV6Vpwo",
    "photo_image_url": "https://images.unsplash.com/photo-1439246854758-f686a415d9da",
    "photo_width": "4273",
    "photo_height": "2392",
    "photo_description": "",
    "photographer_first_name": "Sérgio",
    "photographer_last_name": "Rola"
  },
  {
    "photo_id": "psIMdj26lgw",
    "photo_url": "https://unsplash.com/photos/psIMdj26lgw",
    "photo_image_url": "https://images.unsplash.com/photo-1440773310993-8660d1577dcd",
    "photo_width": "3872",
    "photo_height": "2176",
    "photo_description": "",
    "photographer_first_name": "Alec",
    "photographer_last_name": "Weir"
  },..
]
```
- `setup_openAI_CLIP.ipynb` - Setting up the OpenAI CLIP model for generation of embeddings, feature vectors for comparison
- `TEXT_to_IMAGE_Retrieval.ipynb` - Given a text query retrieve the best results from the available set of unsplash images
- `IMAGE_to_IMAGE_Retrieval.ipynb` - Given a source image retrieve the best results of similar images
- `TAG_to_IMAGE_Retrieval.ipynb` - Given tags (one or multiple) retrieve the images from the datasets
- `IMAGE_and_TEXT_to_IMAGE_Retrieval.ipynb` - Given some text query, serches for the relevant images and an additonal tagged images

## Features 
- Cross-Modal Understanding: CLIP understands both images and text enabling diverse query capabilities.
- Versatility & Adaptability: The engine can generalize to new concepts with minimal training examples and leverage diverse data sources makes it versatile and adaptable to various retrieval tasks without specific datasets.
- Rich Metadata Annotation: Each Unsplash image is annotated with separate metadata
- Complex Query Execution: Perform complex queries such as "snowy peaks rivers and animals grazing" and receive highly relevant results.

## How it works?

## Results and Sample Queries

## Acknowledgements

