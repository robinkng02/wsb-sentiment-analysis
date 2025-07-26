# WallStreetBets Sentiment Analysis Pipeline

A fully automated system for real-time extraction, NER analysis, and sentiment evaluation of Reddit data from r/wallstreetbets with an interactive dashboard.

## The Problem & Motivation

The r/wallstreetbets subreddit has enormous influence on financial markets but generates thousands of comments daily with specialized jargon, memes, and sarcasm. Manual analysis of this data volume is impossible, while automated standard tools fail at the unique WSB language style. My goal was to develop an intelligent pipeline that transforms this "noise" into precise, actionable market sentiment insights for specific financial entities.

## The Solution & Core Features

• **Fully Automated Pipeline**: Continuous data collection every 15 minutes with intelligent historical backfilling during downtime

• **Specialized AI Models**: Custom trained spaCy NER (F1-Score: 0.8) and T5 sentiment models, optimized for financial jargon and WSB language

• **Aspect-Based Sentiment Analysis**: Precise sentiment assignment to specific entities instead of blanket comment evaluation

• **Modern Interactive Dashboard**: Glassmorphism design with real-time visualizations, entity deep-dives, and performance metrics

• **Database-Centric Architecture**: Single source of truth with intelligent status tracking and duplicate prevention

## Architecture & Pipeline

📥 **Data Extraction**: Python script uses Reddit API (PRAW) for continuous post and comment collection with automatic text cleaning on SQLite database insert.

🧠 **Named Entity Recognition**: Custom trained spaCy model with transformer architecture (roberta-base) identifies financial tickers, persons, organizations, and other relevant entities.

💭 **Sentiment Analysis**: Fine-tuned T5 model performs Aspect-Based Sentiment Analysis - evaluates sentiment specifically for each recognized entity with realistic confidence scores.

📝 **Status Management**: Intelligent `processing_status` fields in the database prevent duplicate processing and enable incremental updates.

📊 **Visualization**: Streamlit dashboard with Plotly charts reads processed analysis results directly from the database with performance-optimized SQL queries and 5min caching.

## Technical Decisions & Challenges

• **T5 Confidence Score Problem**: Standard T5 implementations delivered constant 1.0 confidence values. Solution through development of custom confidence calculation methods with label-loss comparison and perplexity-based fallback, enabling realistic scores (0.26-0.41 range).

• **Database-Centric vs. File-Based Approach**: Deliberate decision against CSV/PKL intermediate steps in favor of SQLite single-source-of-truth. This eliminated synchronization problems, enabled atomic transactions, and significantly reduced complexity.

• **Custom AI Training for WSB Context**: Standard NLP models failed at sarcastic WSB jargon ("diamond hands", "to the moon", ticker variations). Custom model training on manually annotated WSB data increased recognition accuracy by approximately 35% compared to standard financial NER models.

• **Production Readiness & Maintainability**: Comprehensive code cleanup (15-20GB legacy code / data removed), Unicode handling for Windows compatibility implemented, and warning suppression for clean log outputs integrated.

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![spaCy](https://img.shields.io/badge/spaCy-09A3D5?style=for-the-badge&logo=spacy&logoColor=white)
![Transformers](https://img.shields.io/badge/🤗_Transformers-FFD21E?style=for-the-badge)
![T5](https://img.shields.io/badge/T5-FF6F00?style=for-the-badge)
![RoBERTa](https://img.shields.io/badge/RoBERTa-FF6F00?style=for-the-badge)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)
![PRAW](https://img.shields.io/badge/PRAW-FF4500?style=for-the-badge&logo=reddit&logoColor=white)
![HuggingFace](https://img.shields.io/badge/🤗_HuggingFace-FFD21E?style=for-the-badge) 
