EECS 6895 Information Processing Final Project - Emotional Nuitionist Chatbot With RAG and Agent

Author: Dongbing Han (UNI: DH3071)
Author: Ziyao Zhou (UNI: ZZ2915)
Author: Yigang Meng (UNI: YM3068)

Project Focus:
Build an Emotion-Aware Nutritionist Chatbot that combines emotion classification with retrieval-augmented generation (RAG) to deliver personalized and contextually relevant dietary advice.

Core Model:

Leverages OpenAI's GPT-4o for high-quality natural language understanding
and response generation.
Responses are enriched using context retrieved from a domain-specific vector store of nutrition articles.
BEAM Fine-Tuning Process:

Fine-tunes a roberta-base model on the GoEmotions (simplified 27-label) dataset to build a domain-specific emotion classifier.
The trained model detects the user's emotional state from each query, enabling prompt rewriting for emotionally-aware and empathetic GPT responses.
Emotion Integration:

Incorporates the BEAM Emotion Classifier to detect the user's emotional state from each query.
Ensures the chatbot can generate responses that are both relevant and informative within the nuition field.
Retrieval Mechanism:

Automatically fetches the most pertinent articles from the NCBI database.
Uses these articles as a knowledge base for the RAG component.
Hybrid Search Based on Similarity Threshold

Leverages a two-step retrieval process by first searching a local FAISS index for relevant documents.
If the similarity score of retrieved documents meets or exceeds a defined threshold (e.g., 0.65), the system returns the results directly. Otherwise the system do realtime queries NCBI to fetch new articles, which are then embedded and indexed.
By maintaining pmids.json, we effectively filters out the duplicates, making sure the efficiency of our retrieval system.
Integrated Approach:

Combines fine-tuned language generation with dynamic retrieval from NCBI.
Delivers context-aware recommendations and insights.
Working Flow:

When a user asks a question about the impact of a surge for diabetes, if it is the first question:

Search and retrieve relevant articles from the NCBI database.
Generate a response based on the retrieved articles and the query.
If it is not the first question:

Perform a cosine similarity search across all the articles already retrieved from the NCBI database.
Check if the existing materials provide enough support for answering the question.
If sufficient material is available → Directly generate the response based on retrieved articles.
If material is insufficient → Search the NCBI database for more relevant articles to support the question.
This retrieval-augmented generation (RAG) method follows a stack RAG approach:

Newly retrieved materials are added to the original articles.
The system continuously expands the knowledge base to ensure stronger evidence for responses.
This dynamic retrieval ensures more comprehensive and accurate answers to evolving queries.
