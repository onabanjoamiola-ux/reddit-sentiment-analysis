# Reddit Sentiment Analysis — Social Justice Discourse

A dual-pipeline sentiment analysis system that collects Reddit comments on social justice topics and analyses public sentiment using both **batch processing** and **real-time streaming** architectures.

Built as part of the MSc Data Science programme at Liverpool John Moores University.

---

## Project Overview

This project explores how sentiment around social justice topics — including human rights, refugees, gender equality, and geopolitical discourse — shifts across Reddit communities over time.

Two separate pipelines were built to handle data collection and analysis:

- **Batch Pipeline** — collects large volumes of historical Reddit comments, applies sentiment analysis, and stores results in MongoDB
- **Live Streaming Pipeline** — streams Reddit comments in real time, processes sentiment on the fly, and displays results on an auto-refreshing interactive dashboard

---

## Tech Stack

| Layer | Tools |
|---|---|
| Data Collection | PRAW (Reddit API) |
| Storage | MongoDB, CSV |
| NLP & Sentiment | NLTK, VADER, TextBlob |
| Visualisation | Matplotlib, Plotly |
| Language | Python 3 |

---

## Repository Structure

```
reddit-sentiment-analysis/
│
├── batch_pipeline_sentiment.ipynb     # Full batch data collection + sentiment pipeline
├── live_streaming_sentiment.ipynb     # Real-time streaming + live dashboard
├── reddit_output_sample.csv           # Sample dataset output
├── requirements.txt                   # Python dependencies
└── .gitignore
```

---

## How It Works

### Batch Pipeline (`batch_pipeline_sentiment.ipynb`)
1. Fetches comments from 6 subreddits: `r/socialjustice`, `r/worldnews`, `r/HumanRights`, `r/Palestine`, `r/internationalrelations`, `r/middleeast`
2. Cleans text — removes URLs, punctuation, stopwords, and tokenises
3. Applies two sentiment models in parallel:
   - **VADER** — rule-based, optimised for social media language
   - **TextBlob** — lexicon-based polarity and subjectivity scoring
4. Saves results to **MongoDB** and exports a **CSV**
5. Generates visualisations including hourly sentiment trends and VADER vs TextBlob comparisons

### Live Streaming Pipeline (`live_streaming_sentiment.ipynb`)
1. Streams live comments from `r/HumanRights`, `r/Palestine`, `r/worldnews`, `r/Israel` using PRAW's streaming API
2. Applies VADER and TextBlob sentiment in real time
3. Refreshes an interactive **Plotly dashboard** every 100 seconds showing:
   - Live sentiment bar chart (positive / neutral / negative counts)
   - Rolling average TextBlob polarity line chart over time

---

## Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/reddit-sentiment-analysis.git
cd reddit-sentiment-analysis
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Download NLTK data
```python
import nltk
nltk.download('stopwords')
nltk.download('punkt')
nltk.download('vader_lexicon')
```

### 4. Add your Reddit API credentials
Create a free Reddit app at [reddit.com/prefs/apps](https://reddit.com/prefs/apps), then replace the placeholders at the top of each notebook:

```python
R_CLIENT_ID = "YOUR_REDDIT_CLIENT_ID"
R_CLIENT_SECRET = "YOUR_REDDIT_CLIENT_SECRET"
R_USER_AGENT = "YourAppName/1.0"
```

### 5. (Optional) Set up MongoDB
For the batch pipeline, ensure MongoDB is running locally:
```bash
mongod --dbpath /your/db/path
```
Or update `MONGO_URI` to point to your own MongoDB instance.

---

## Sample Results

The batch pipeline was run across 6 subreddits collecting over 5,000 comments. Key findings:

- **VADER** classified the majority of comments as **neutral**, reflecting the measured tone of longer Reddit posts
- **TextBlob** detected more **positive** polarity overall, consistent with its tendency to score neutral-to-mild language as slightly positive
- Sentiment activity peaked during **evening hours (UTC)**, suggesting higher engagement from European and American users

---

## What I'd Improve

- Add **keyword filtering** to isolate specific topics more precisely (e.g. isolating Gaza-specific discourse from general human rights posts)
- Integrate **Apache Kafka** to replace PRAW streaming for higher-throughput production pipelines
- Add a **Hadoop/HDFS layer** for distributed storage of large-scale data collection runs
- Build a persistent **web dashboard** using Dash or Streamlit instead of Jupyter-only visualisations

---

## Author

**Amiola Onabanjo**  
MSc Data Science — Liverpool John Moores University  
[LinkedIn](https://linkedin.com/in/YOUR_LINKEDIN) | [GitHub](https://github.com/onabanjoamiola-ux)
