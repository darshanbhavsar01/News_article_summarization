# News Article Summarization (English + Hindi)

Automatic summarization of news articles in **English and Hindi**. The repository contains
three approaches developed as a semester-7 project, plus a small Django web app for
storing articles and reading their summaries.

![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-FF6F00?logo=tensorflow&logoColor=white)
![spaCy](https://img.shields.io/badge/spaCy-NLP-09A3D5?logo=spacy&logoColor=white)
![Django](https://img.shields.io/badge/Django-web%20app-092E20?logo=django&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

## Why

News readers rarely have time for full articles, and most summarization tools only
support English. This project explores summarization for both English and Hindi news,
comparing a lightweight extractive method with trained abstractive models.

## Approaches

| Notebook | Method | Language |
|---|---|---|
| [`Extractive_summarization.ipynb`](Extractive_summarization.ipynb) | **Extractive.** spaCy tokenisation, stop-word filtering, normalised word-frequency scoring of sentences; the top 30% of sentences form the summary. | English |
| [`EnglishArticlesSummaryFinal.ipynb`](EnglishArticlesSummaryFinal.ipynb) | **Abstractive.** Sequence-to-sequence encoder–decoder with stacked LSTMs and an attention layer (TensorFlow/Keras), trained on article–summary pairs. | English |
| [`HindiArticlesSummaryFinal.ipynb`](HindiArticlesSummaryFinal.ipynb) | **Abstractive.** The same LSTM encoder–decoder architecture, trained on Hindi article–summary pairs. | Hindi |

[`darshan_project/model.py`](darshan_project/model.py) also tries a pretrained
Hugging Face `transformers` summarization pipeline as a reference point.

Both abstractive notebooks follow the same steps: text cleaning (HTML stripping,
contraction expansion for English, stop words), tokenisation and padding, model building, training
with early stopping, and inference with a separate decoder model.

## Web app

A Django app (`darshan_project/`) with:

- user registration and login
- a form to save an article (title, URL, full text and summary)
- an **Articles** page listing every saved article with its summary

## Repository layout

```
EnglishArticlesSummaryFinal.ipynb   # abstractive model, English
HindiArticlesSummaryFinal.ipynb     # abstractive model, Hindi
Extractive_summarization.ipynb      # extractive baseline (spaCy)
darshan_project/                    # Django web app (app: termwork)
G16-news_article_summarization-SRS.pdf          # software requirements specification
G16_sem7_news_article_summarization (1).pptx    # project presentation
```

## Run it locally

**Notebooks**

```bash
pip install tensorflow pandas numpy nltk beautifulsoup4 matplotlib scikit-learn spacy
python -m spacy download en_core_web_sm
jupyter notebook
```

The abstractive notebooks expect `English_train.csv` / `Hindi_train.csv`
(article–summary pairs) next to them. The datasets are not included in this repository
because of their size.

**Web app**

```bash
pip install django
cd darshan_project/darshan_project
python manage.py migrate
python manage.py runserver
```

Then open http://127.0.0.1:8000/.

## Tech stack

Python · TensorFlow / Keras · spaCy · NLTK · pandas · scikit-learn · Hugging Face
Transformers · Django · SQLite · Bootstrap

## Possible next steps

- Wire the trained models into the web app so summaries are generated, not typed in
- Evaluate with ROUGE scores on a held-out set
- Compare against modern multilingual models such as mT5 or IndicBART

## Author

**Darshan Bhavsar** · [LinkedIn](https://www.linkedin.com/in/darshan01/) ·
[GitHub](https://github.com/darshanbhavsar01)

## License

[MIT](LICENSE)
