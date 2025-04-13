# Take Home Exam by Richmond Tetteh Djwerter and Kwaku Adou @apeakoadou

# **ABSTRACT**

This Multi-Modal Movie Recommendation System leverages a combination of structured numerical features and deep text embeddings to provide accurate and personalized movie recommendations. Unlike traditional recommender systems that rely solely on user ratings or metadata, this model integrates numerical attributes (such as popularity and ratings) with semantic information extracted from movie overviews.

The system precomputes numerical representations using feature normalization and text embeddings using the SentenceTransformer model (all-MiniLM-L6-v2). At inference time, it calculates cosine similarity across both modalities and returns a ranked list of the most relevant movie suggestions.

The use of a precomputed embedding cache ensures fast query response times, making this approach suitable for real-time applications such as movie streaming platforms and content recommendation engines. The system is deployed as an interactive Gradio application, allowing users to input a movie title and receive a list of recommended movies.

# **Model Card: Autoencoder-Based Multi-Modal Movie Recommendation System**

**Model Overview**

This model is a multi-modal movie recommendation system that suggests movies based on both numeric metadata (e.g., popularity, average rating) and semantic similarity (based on movie descriptions). The combination of structured and unstructured data allows for more context-aware recommendations.

**Intended Use**

Primary Purpose: Recommends similar movies based on user input.

**Target Users:**

Movie enthusiasts
Streaming platforms (Netflix, Disney+, etc.)
AI researchers in recommendation systems

**Inputs:**
Movie Title: Finds movies with similar attributes and descriptions.
Number of Recommendations: Defines how many similar movies to return.
Outputs: A ranked list of recommended movies.

**Model Architecture**

The system consists of two primary components:

**Numeric Feature Processing:**

Uses popularity and vote average as key numerical features.
Data is normalized using StandardScaler for similarity computation.
Text-Based Feature Extraction:

Uses SentenceTransformer (all-MiniLM-L6-v2) to encode movie overviews into 384-dimensional vectors.
Embeddings are precomputed and cached for fast retrieval.

**Similarity Computation:**

Uses cosine similarity on both numeric and text features.
A weighted combination of both similarities determines final recommendations.

**Dataset Used**  
- **Source:** TMDB Movies Dataset 2023 (Kaggle)  
- **Size:** About **930,000 entries movie entries**

**Performance & Optimization**

**Fast Inference:**
Uses precomputed embeddings for text features to avoid API calls and reduce runtime.
Numerical data is vectorized and normalized for efficient similarity search.

**Batch Processing:**
Text embeddings are generated in batches of 512 for optimized memory usage.
Parallelized processing enables embedding computation in under 15 minutes for 50K movies.

**Performance Metrics**  
- **Mean Squared Error (MSE):** Evaluated reconstruction loss of the autoencoder.  
- **Cosine Similarity:** Measures recommendation accuracy based on similarity scores.  

**Limitations & Risks**  
- **Limited Image Understanding:** Movie posters are **not yet integrated** into recommendations.  
- **Bias in Data:** Popular movies may dominate recommendations due to dataset imbalances.  
- **Cold Start Problem:** New movies without sufficient metadata may not be well recommended.  

**Deployment**  
- **Gradio App:** Provides an interactive UI for testing recommendations.  
