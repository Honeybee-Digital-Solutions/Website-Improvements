A dynamic post recommendation engine that categorizes users into three segments to ensure relevant content delivery:

1. Warm Users: Personalized suggestions driven by User Embedding Matrices (based on explicit interactions). 
2. Semi-Warm Users: Tailored content based on implicit signals (views/browsing) when explicit data is limited.
3. Cold Users: Discovery-focused recommendations featuring trending, recent, and localized content.



The system follows a high-performance pipeline to ensure users see the most relevant content in real-time.


Stage 1: Retrieval (Candidate Generation)
This stage acts as a wide-net filter. It retrieves a pool of ~100–500 candidate posts from the entire database using lightweight heuristics:

Recency: Prioritizing the latest "CityHangAround" updates.

Location: Filtering for posts within the user's immediate vicinity or city.

Trending: Leveraging global engagement signals to surface "viral" content for discovery.


Stage 2: Scoring (LGBM Ranker)
For "Known" (Warm/Semi-Warm) users, the LGBM Ranker takes over. It uses LambdaRank logic to re-order the candidates based on predicted engagement probability.

Objective: Optimized for NDCG (ranking quality) rather than just accuracy.

Features: It weighs user-post category affinity, author history, and interaction types (likes, shares) to output a personalized final feed.

Fallback: For new (Cold) users, the ranked order is derived directly from the weighted Trending and Local scores from Stage 1.
