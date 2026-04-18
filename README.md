# 🥗 Diet Planner Chatbot

> An intelligent AI-powered chatbot designed to provide personalized dietary advice, meal planning, and nutrition guidance through advanced NLP and retrieval-augmented generation (RAG).

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Project Architecture](#project-architecture)
- [Directory Structure & File Explanations](#directory-structure--file-explanations)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Project Overview

The **Diet Planner Chatbot** is a sophisticated conversational AI system that combines multiple NLP techniques to answer dietary questions, suggest meal plans, and provide nutritional insights. It leverages a hybrid retrieval system combining BM25 (sparse) and dense vector search (semantic), with advanced query rewriting, intent detection, and multimodal analysis capabilities.

### Architecture Highlights:
- **Hybrid Retrieval**: BM25 + Dense vector search for comprehensive information retrieval
- **Advanced Query Processing**: Intent detection and query rewriting for better understanding
- **RAG Pipeline**: Retrieval-Augmented Generation with reranking and deduplication
- **Multimodal Support**: Image-based food analysis for portion size estimation
- **Stateful Conversation**: Session management for context-aware responses

---

## ✨ Key Features

✅ **Smart Query Understanding** - Intent detection and query rewriting  
✅ **Hybrid Search** - Combines BM25 and semantic search  
✅ **AI-Powered Responses** - LLM-based answer generation with RAG  
✅ **Conversation Memory** - Maintains state across interactions  
✅ **Food Image Analysis** - Multimodal analysis for portion estimation  
✅ **Deduplication & Reranking** - Ensures quality and relevance  
✅ **RESTful API** - Easy integration with web/mobile applications  

---

## 🏗️ Project Architecture

```
diet-chatbot/
│
├── config/                 # Configuration Files
├── data/                   # Data Storage
├── utils/                  # Utility Functions
├── src/                    # Core Application Logic
├── tests/                  # Testing Suite
├── notebooks/              # Experimental Notebooks
├── requirements.txt        # Dependencies
├── .env                    # Environment Variables
└── README.md              # This File
```

---

## 📂 Directory Structure & File Explanations

### 📁 **config/** - Configuration Management

Centralized configuration files for all major system components.

| File | Purpose |
|------|---------|
| **chunking.py** | Defines text chunking strategies (size, overlap, method) for document splitting |
| **embedding.py** | Configuration for embedding models (model name, dimensions, batch size) |
| **retrieval.py** | Settings for retrieval systems (BM25 parameters, similarity thresholds, reranking config) |
| **api_config.py** | API settings (endpoints, authentication, rate limiting, model parameters) |

---

### 📁 **data/** - Data Storage & Processing

Organized data pipeline following standard ML conventions.

| Directory | Purpose |
|-----------|---------|
| **raw/** | Original, unprocessed diet/nutrition data from various sources |
| **interim/** | Intermediate processing results (cleaned, partially processed) |
| **processed/** | Final processed data ready for embeddings and retrieval |

---

### 📁 **utils/** - Utility & Helper Functions

Reusable utility modules shared across the application.

| File | Purpose |
|------|---------|
| **text_utils.py** | Common text operations (tokenization, normalization, formatting) |
| **logger.py** | Centralized logging configuration for debugging and monitoring |

---

### 📁 **src/** - Core Application Logic

#### 🔄 **src/ingestion/** - Data Ingestion & Text Cleaning

Handles raw data input and initial text processing to prepare data for embedding.

| File | Purpose |
|------|---------|
| **text_extractor.py** | Extracts text from various file formats (PDF, DOCX, TXT) |
| **word_normalizer.py** | Normalizes words (stemming, lemmatization, case conversion) |
| **special_char_cleaner.py** | Removes special characters, URLs, emails, and formatting artifacts |
| **number_normalizer.py** | Standardizes numerical representations (e.g., "5kg" → "5 kilograms") |
| **date_normalizer.py** | Parses and standardizes date formats for temporal queries |

#### 🔧 **src/preprocessing/** - Data Preprocessing

Transforms cleaned text into structured formats optimized for retrieval.

| File | Purpose |
|------|---------|
| **json_builder.py** | Converts processed text into structured JSON format with metadata |
| **parser.py** | Parses structured data and extracts key information (nutrients, ingredients, etc.) |
| **chunking.py** | Splits documents into optimal-sized chunks for embedding and retrieval |

#### 🧬 **src/embeddings/** - Embedding & Vector Storage

Converts text to dense vectors and manages vector database operations.

| File | Purpose |
|------|---------|
| **embedder.py** | Uses embedding models (e.g., Sentence-Transformers) to generate text embeddings |
| **vector_store.py** | Interface for vector storage backends (FAISS for local, Pinecone for cloud) |

#### 🔍 **src/retrieval/** - Information Retrieval

Advanced retrieval system combining multiple strategies for comprehensive information access.

| File | Purpose |
|------|---------|
| **bm25.py** | BM25 sparse retrieval for keyword-based search (statistically proven relevance) |
| **dense_retriever.py** | Dense vector similarity search for semantic understanding |
| **hybrid_retriever.py** | Combines BM25 and dense retrieval, merges results intelligently |
| **reranker.py** | Re-ranks retrieved documents using cross-encoders for better relevance |
| **deduplication.py** | Removes duplicate or highly similar documents from results |
| **context_builder.py** | Assembles final context by organizing and formatting retrieved documents |

#### ❓ **src/query/** - Query Processing

Analyzes and optimizes user queries for better retrieval and understanding.

| File | Purpose |
|------|---------|
| **intent_detector.py** | Classifies query intent (e.g., "meal_suggestion", "nutrition_info", "diet_plan") |
| **query_rewriter.py** | Reformulates queries to improve retrieval (expands, clarifies, decomposes) |

#### 💬 **src/prompts/** - Prompt Engineering

Manages LLM prompts for various tasks in the pipeline.

| File | Purpose |
|------|---------|
| **system_prompt.py** | Core system prompt defining chatbot personality and behavior guidelines |
| **query_rewrite_prompt.py** | Prompt template for query rewriting tasks |
| **output_prompt.py** | Prompt template for final response generation |

#### 🚀 **src/pipeline/** - Orchestration Pipelines

Coordinates multi-step workflows for end-to-end processing.

| File | Purpose |
|------|---------|
| **ingestion_pipeline.py** | Orchestrates entire data ingestion, cleaning, and processing workflow |
| **query_pipeline.py** | Orchestrates query processing, retrieval, and response generation pipeline |

#### 🤖 **src/chatbot/** - Chatbot Core Logic

Central chatbot intelligence and conversation management.

| File | Purpose |
|------|---------|
| **orchestrator.py** | Main coordinator managing all chatbot components and workflow |
| **response_generator.py** | Generates final LLM responses based on retrieved context and user query |
| **state_manager.py** | Maintains conversation history and session state for context-aware responses |

#### 📸 **src/multimodal/** - Multimodal Capabilities

Extends chatbot to handle image inputs for food recognition and analysis.

| File | Purpose |
|------|---------|
| **image_analyzer.py** | Detects food items, estimates portions, and analyzes nutritional content from images |
| **nutrition_mapper.py** | Maps detected food items to nutritional databases |

#### 🌐 **src/api/** - REST API

Exposes chatbot functionality through HTTP endpoints.

| File | Purpose |
|------|---------|
| **routes.py** | Defines API endpoints (e.g., `/chat`, `/meal-plan`, `/nutrition-analysis`) |
| **controllers.py** | Handles request processing, validation, and response formatting |

#### 🎬 **src/main.py**

Entry point for running the application (CLI or API server initialization).

---

### 🧪 **tests/** - Testing Suite

Comprehensive test coverage for critical components.

| File | Purpose |
|------|---------|
| **test_retrieval.py** | Tests for retrieval systems (BM25, dense, hybrid) accuracy and performance |
| **test_pipeline.py** | Integration tests for complete ingestion and query pipelines |

---

### 📓 **notebooks/** - Experimental Notebooks

Jupyter notebooks for exploration, prototyping, and analysis (not part of production).

---

### 📄 **Root Level Files**

| File | Purpose |
|------|---------|
| **requirements.txt** | Python package dependencies and versions |
| **.env** | Environment variables (API keys, model names, database credentials) |
| **README.md** | Project documentation (this file) |
| **LICENSE** | Software license and usage terms |

---

## 🚀 Installation

### Prerequisites
- Python 3.9+
- pip or conda

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd diet-planner
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   venv\Scripts\activate  # On Windows
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys and settings
   ```

5. **Run the application**
   ```bash
   python src/main.py
   ```

---

## 💡 Usage

### As a Chatbot
```python
from src.chatbot.orchestrator import ChatbotOrchestrator

bot = ChatbotOrchestrator()
response = bot.chat("What's a good meal plan for weight loss?")
print(response)
```

### As an API
```bash
# Start the server
python src/api/routes.py

# Query the API
curl http://localhost:5000/chat -X POST -d '{"query": "Vegan meal ideas"}'
```

### Data Ingestion
```python
from src.pipeline.ingestion_pipeline import IngestionPipeline

pipeline = IngestionPipeline()
pipeline.ingest("data/raw/nutrition_data.txt")
```

---

## 🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📞 Contact & Support

For questions or issues, please open an issue on the repository or contact the development team.

**Happy meal planning! 🍽️**
