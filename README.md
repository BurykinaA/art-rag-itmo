# 🦜️🔗 ART RAG


## Setup

This project uses [Poetry](https://python-poetry.org/) for dependency management.

```shell
# Create Python environment
$ poetry install

# Install git pre-commit hooks
$ poetry shell
$ pre-commit install
```

## Running

```shell
# Run app.py
$ streamlit run app.py
```

## Running with Docker

```shell
# Run docker-compose
$ docker-compose up --build
```

## Description

The project is focused on developing a RAG system capable of answering various questions about art. The primary domain of the project is artists and their works.

## Dataset Description

This project utilizes two large datasets on artists:

- **WikiArt** (https://www.wikiart.org/en) – 80,984 artworks and 3,518 artist names. Scraping was conducted using code from this repository: https://github.com/michaelvin1322/scrapWikiArt/tree/master. Total scraping time: 12 hours.
- **Open Data at the National Gallery** (https://github.com/NationalGalleryOfArt/opendata/tree/main) – a dataset containing descriptions of 130,000 artworks, with detailed information about all works in the National Gallery, including the methods of acquisition.

As a result, we compiled a dataset of 81,000 objects with descriptions (both artists and their works). These were chunked into pieces of 384 characters and used to create embeddings.

### Testing

The project focuses exclusively on data about various artists and uses information in English. Therefore, during the testing phase, only English-language queries should be used. Questions used for metric evaluation can be found in the `exps` directory in a Jupyter notebook.

## Technical Project Overview

The following tools and models were used in the project:

- **RAG Dev**: LangChain  
- **Embedder**: E5-Large  
- **Database**: FAISS  
- **LLM**: Azure OpenAI GPT-4 Small  
- **Dev**: Streamlit, Docker  

## Metrics and Validation

Various art- and artist-related questions were generated using GPT o1, as well as manually created questions. The final validation dataset contains 21 questions.  

Two metrics were used to compare hypotheses: **Answer Relevance** and **Context Relevance**, both rated on a scale from 1 to 4. The evaluation employed the **LLM-as-a-Judge** technique, where a prompt was used to assess the proposed responses from 1 to 4. The average score was then calculated.

|   |AR|CR|
|---|---|---|
|Only FAISS v3|3.19|3.26|
|**FAISS + LLM v3**|**3.52**|**3.26**|
|BM25 + LLM v3|3.42|1.62|
|FAISS + LLM v1|3.41|2.76|

## Appearance

![image](https://github.com/user-attachments/assets/d409cb94-3221-402a-bb62-893e3b0b7039)

