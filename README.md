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
    "photo_description": "magical sunset hues across the ocean",
    "photographer_first_name": "Sérgio",
    "photographer_last_name": "Rola"
  },
  {
    "photo_id": "psIMdj26lgw",
    "photo_url": "https://unsplash.com/photos/psIMdj26lgw",
    "photo_image_url": "https://images.unsplash.com/photo-1440773310993-8660d1577dcd",
    "photo_width": "3872",
    "photo_height": "2176",
    "photo_description": "seagull",
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

> NOTE : Not ALL the images and feature vectors generated by the code in `setup_openAI_CLIP.ipynb` is uploaded to github due to github size issues. Only 5 samples of each can be found in `curated-data`'s `features` and `photos` folder

## Features 
- **Cross-Modal Understanding** : CLIP understands both images and text enabling diverse query capabilities.
- **Versatility & Adaptability**: The engine can generalize to new concepts with minimal training examples and leverage diverse data sources makes it versatile and adaptable to various retrieval tasks without specific datasets.
- **Rich Metadata Annotation** : Each Unsplash image is annotated with separate metadata
- **Complex Query Execution**: Perform complex queries such as "snowy peaks rivers and animals grazing" and receive highly relevant results.

## How it works?
### Unsplash Image Annotations 
The dataset is curated from opensource unsplash images. Each image has an associated metadata with 8 fields namely `photo_id`,`photo_url`,`photo_image_url`,`photo_width`,`photo_height`,`photo_description`,  `photographer_first_name`,`photographer_last_name`. This annotated data serves as additional descriptors and context for the images contributing to a more refined and accurate search experience. The annotated json data is converted into consumable dataframe to retrieve the unsplash images from its descriptors/metdata fields.

### CLIP Model Integration
The engine uses OpenAI's CLIP model. This integration (in the file `setup_openAI_CLIP.ipynb`) allows the search engine to bridge the gap between text and images effortlessly using powerful embeddings. Leveraging CLIP's unique architecture, the engine encodes and understands the semantic relationships between images and text, enabling cross-modal comprehension. This integration fundamentally transforms the search paradigms we know, like elastic search, enabling a sophisticated understanding of visual and textual content further buidling on revolutionizing information retrieval.

### Generating feature vectors and embeddings 
 Each image and text query undergoes an encoding process resulting in the generation of feature vectors and embeddings. For images, these feature vectors encapsulate the visual characteristics and semantic representations abstracted into a high-dimensional space. Text queries are transformed into embeddings, capturing their semantic essence and contextual information. These feature vectors and embeddings, derived from CLIP's encoding mechanism, facilitate the creation of a unified space where images and text converge allowing for efficient comparison and similarity measurements. 

 ```python
 def encode_search_query_with_text(search_query):
    with torch.no_grad():
        # Encode and normalize the search query using CLIP
        text_encoded = model.encode_text(clip.tokenize(search_query).to(device))
        text_encoded /= text_encoded.norm(dim=-1, keepdim=True)

        # Retrieve the feature vector from the GPU and convert it to a numpy array
        return text_encoded.cpu().numpy()


def encode_search_query_with_img(source_image):
    with torch.no_grad():
      image_feature = model.encode_image(preprocess(Image.open(source_image)).unsqueeze(0).to(device))
      image_feature = image_feature / image_feature.norm(dim=-1, keepdim=True)

      return image_feature.cpu().numpy()
 ```

### Multi-Modal search Image/text queries 
```python

#Samples text and Image queries 
#text2img
search_query = "evening colourful skies with trees and people"

#img2img
source_image = "/content/drive/My Drive/unsplash-dataset/curated-data/photos/01ZeHnK3F_4.jpg"

#tag2img
search_tag1 = "tower"
search_tag2 = "night"

#img2img&text

source_image = "/content/drive/My Drive/unsplash-dataset/curated-data/photos/0Hr2m3V_w1Q.jpg"
search_text = "leaves"
```
ModaCLIP excels in executing complex multi-modal querie seamlessly intertwining image and text information. Whether it's searching for specific visual attributes within images or finding textual descriptions of visual content ModaCLIP search engine excels in multi-modal information retrieval. This capability expands the horizons of conventional keyword-based searches offering a nuanced and comprehensive search experience.

## Results and Sample Queries
#### Text-to-Image Retrieval
- search_query 1 = "colourful skies with trees"
- search_query 2 = "snowscape mountains peaks"
<table>
  <tr>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/txt2img-query1.png" alt="Image 1" style="width: 300px;"></td>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/txt2img-query2.png" alt="Image 2" style="width: 300px;"></td>
  </tr>
</table>


#### Image-to-Image Retrieval
- source_image 1
<img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/img2imgsample.png" alt="modaCLIP Logo" width="100" height="100" />
- source_image 2
<img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/img2imgsample2.png" alt="modaCLIP Logo" width="100" height="100" />

<table>
  <tr>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/img2img-query1.png" alt="Image 1" style="width: 300px;"></td>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/img2img-query2.png" alt="Image 2" style="width: 300px;"></td>
  </tr>
</table>

#### Tag+Text-to-Image Retrieval
- Query-Tags 1 = "trees"
- Query-Tags 2 = "tower", "night
<table>
  <tr>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/tag2img-query1.png" alt="Image 1" style="width: 300px;"></td>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/tag2img-query2.png" alt="Image 2" style="width: 300px;"></td>
  </tr>
</table>

#### Image+Text-to-Image Retrieval
- source_image 1 & search_query 1 = "leaves"
<img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/curated-data/photos/Agwkkxw0JY.jpg" alt="modaCLIP Logo" width="100" height="100" />


- source_image 2 & search_query 2 = "rocky mountians"
<img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/curated-data/photos/3FAzLYaj_4.jpg" alt="modaCLIP Logo" width="100" height="100" />

<table>
  <tr>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/img2txtimg-query1.png" alt="Image 1" style="width: 300px;"></td>
    <td><img src="https://github.com/ashutoshtiwari13/ModaCLIP/blob/main/docs/img2txtimg-query2.png" alt="Image 2" style="width: 300px;"></td>
  </tr>
</table>

## Acknowledgements

This project was inspired by these projects:

- [Beyond tags and entering the semantic search era on images with OpenAI CLIP](https://towardsdatascience.com/beyond-tags-and-entering-the-semantic-search-era-on-images-with-openai-clip-1f7d629a9978) by [Ramsri Goutham Golla](https://twitter.com/ramsri_goutham)
- [OpenAI's CLIP](https://github.com/openai/CLIP)
- [Unsplash](https://unsplash.com/)

