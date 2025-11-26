# Personalized-Real-Estate-Agent
🏡 HomeMatch: Real Estate Listing Recommender

HomeMatch is a Python-based project that uses Large Language Models (LLMs) and Vector Databases to perform semantic search on real estate listings and provide personalized home recommendations.

This project simulates a pipeline where:

Synthetic real estate listing data is generated.

The listings are embedded and stored in a vector database (ChromaDB).

User preferences are extracted and used to perform a similarity search.

The top matching listings are augmented by an LLM to create a personalized, tempting recommendation message.

🛠️ Technologies Used

Python: The core programming language.

LangChain: Framework for developing applications powered by language models.

OpenAI: Used for text generation (LLM) and creating embeddings (gpt-3.5-turbo and text-embedding-3-small).

ChromaDB: The vector store used for efficient semantic search.

Pandas: For handling and manipulating the listing data in CSV format.

Pydantic: Used for structured data extraction of user preferences.

🚀 Setup and Installation

Prerequisites

Python 3.8+

An OpenAI API Key

1. Clone the repository (or download the notebook)

git clone <your-repo-url>
cd <your-repo-name>
# If you only have the notebook, ensure you are in the directory containing HomeMatch.ipynb


2. Install Dependencies

The project uses several libraries, which can be installed using pip:

pip install -U -q openai langchain langchain-openai langchain-chroma langchain-core langchain-text-splitters chromadb sentence-transformers pandas pydantic


3. Set Environment Variables

You must set your OpenAI API key and base URL (if applicable) as environment variables.

In the provided Jupyter notebook (HomeMatch.ipynb), this is handled by the first code cell:

%env OPENAI_API_KEY = your_api_key_here
%env OPENAI_API_BASE = your_api_base_url_here


Replace your_api_key_here and your_api_base_url_here with your actual credentials.

Alternatively, you can export these variables in your terminal session:

export OPENAI_API_KEY="your_api_key"
export OPENAI_API_BASE="your_base_url" # e.g., [https://api.openai.com/v1](https://api.openai.com/v1) if not using a proxy


🏃 How to Run

The entire workflow is contained within the HomeMatch.ipynb Jupyter Notebook.

Start Jupyter:

jupyter notebook


Open HomeMatch.ipynb: Navigate to the notebook file in your browser.

Run Cells Sequentially: Execute the cells one by one, paying close attention to the sections for:

Setup: Initializing API keys and installing packages.

Data Generation: The LLM generates a synthetic houselistings.csv file.

ChromaDB Indexing: The data is converted into documents, embedded using OpenAIEmbeddings, and stored in a ChromaDB instance.

Semantic Search: You will be prompted to enter your housing preferences. The system uses Pydantic to structure your input and performs a similarity search.

Recommendation: The top match is passed back to the LLM (gpt-3.5-turbo) to generate a personalized, attractive sales description based on your original preference.

📝 Project Flow Summary

LLM Data Generation: A prompt is sent to the LLM to create 20 realistic, comma-separated real estate listings with specified headers (Neighborhood, Price, Bedroom, Description, etc.).

Data Ingestion: The generated CSV data is loaded into a Pandas DataFrame. Each row is converted into a LangChain Document object, with the original listing details stored in the metadata.

Vectorization: The documents are embedded into vectors using the text-embedding-3-small model and persisted to a Chroma vector store.

Preference Extraction: User input is parsed, and an LLM is used with a Pydantic Buyerpref schema to reliably extract structured preferences (e.g., budget, bedrooms, size).

Retrieval: A query string is formulated from the user's structured preferences and used for a similarity_search in ChromaDB to retrieve the top 3 semantically similar listings.

Augmentation (RAG): The best matched listing is combined with the user's initial preference and sent to the LLM to generate a custom, persuasive, and emotionally engaging property recommendation.
