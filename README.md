# Academic Research Assistant with Retrieval-Augmented Generation (RAG)

## Overview
This project involves the development of an advanced **Academic Research Assistant** system using **Retrieval-Augmented Generation (RAG)** to enhance the retrieval process for academic literature. The system addresses the limitations of traditional search engines and language models by providing precise, contextually relevant articles, optimizing user queries, and refining responses based on user feedback.

## Key Features
1. **Efficient Query Processing**: Users can input a query to retrieve the top 5 most relevant articles using cosine similarity.
2. **Query Expansion**: The system refines the initial query by generating related keywords and phrases to improve the relevance of the search results.
3. **Ranking Phase**: A ranking mechanism selects the 5 most relevant articles from the combined results of the initial and expanded queries.
4. **User Feedback Integration**: Users can provide feedback on the relevance of retrieved articles. This feedback is used to optimize the system's response by performing arithmetic operations on the query's vector representation.
5. **Abstract Summarization**: Abstracts of retrieved articles are summarized using **OpenAI's GPT-3.5 Turbo** to help users quickly assess relevance.
6. **Advanced Search Options**: Users can upload an article in various formats (ID, link, image, PDF), with OCR technology employed to extract content from images and PDFs for enhanced retrieval.

## Methodology
### Data Preparation
- **Dataset**: The ArXiv dataset from Kaggle was used, containing metadata, titles, and abstracts of academic papers.
- **Preprocessing**:
  - **Date Formatting**: The `update_date` field was converted to datetime format for chronological sorting.
  - **Category Filtering**: Data science-related categories such as `cs.AI`, `cs.LG`, `cs.CL`, `cs.CV`, and others were filtered to tailor results to the data science community.
  - **Text Preparation**: Titles and abstracts were combined into a `prepared_text` field to retain context during embedding generation.

### RAG Pipeline
1. **System Initialization**: The system uses **Pinecone** as the vector database, initialized with an index created using `SentenceTransformer ("all-MiniLM-L6-v2")` for embedding generation.
2. **Document Embedding Storage and Indexing**: Document embeddings and metadata were stored and indexed in Pinecone.
3. **Query Processing**: User queries are transformed into embeddings and compared with document embeddings using cosine similarity to retrieve the top 5 articles.
4. **Ranking and Selection**: The system ranks and selects the 5 most relevant articles from combined initial and expanded query results.
5. **Feedback Optimization**: User feedback is used to optimize the query vector by averaging embeddings of relevant articles and subtracting an adjusted vector for irrelevant ones.
6. **Summarization**: Retrieved article abstracts are summarized using **GPT-3.5 Turbo**.
7. **Advanced Search**: Supports input methods including ID, link, image, and PDF uploads, with OCR technology applied for content extraction.


## Running the Application
### Installation
Install the necessary dependencies by running:
```bash
pip install -r requirements.txt
```
### Running the Streamlit Interface
To run the user interface, execute the following command in your terminal:
```
streamlit run main_ui.py
```
This will start the Streamlit server, and you can access the interface in your web browser. Use the interface to input queries or upload articles and view the retrieved results.

### Future Work
Future development plans include creating a database of user queries and their optimized embeddings to enhance the model's overall performance. This database will be used to compare new queries with previous ones and retrieve associated optimized articles using cosine similarity. A threshold will be implemented to determine sufficient similarity between queries, with further research planned to refine this threshold.

### Notebooks Overview

This project includes three main Jupyter notebooks:

#### 1. **Automated ArXiv Article Update and Pinecone Upsert**
- Automates the retrieval, filtering, and upserting of new data science articles from the ArXiv dataset into Pinecone.
- Ensures the index remains current with recent research by encoding and batch uploading new articles.

#### 2. **Feedback-Adjusted Query Optimization**
- Simulates user feedback to refine query vectors, enhancing the relevance of retrieved articles.
- Shows that incorporating feedback improved retrieval, adding an average of 0.923 new relevant articles to the top 5 results.

#### 3. **Query Extension Evaluation and Optimization**
- Uses GPT for query expansion, broadening search context and improving result relevance.
- Demonstrated that expanded queries increased relevant article retrieval, with 1.65 new articles on average in the top 5.

These notebooks enhance the academic article retrieval system by keeping it updated, expanding queries, and refining results with feedback.
