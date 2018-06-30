# Building a Recommender System on AWS

## SageMaker overview

1. Notebook instances to manage the data
2. Use a built-in algorithm
3. ML Training service
4. ML Hosting service which expose a RESTful endpoint to make new recommendations

## Process

1. Problem Framing
   - Content-based filtering, generate recommendations based on known user preferences. Easy to understand and implement, but only applicable to domains where user preferences can be captured in full and can't predict new user preferences. Also there is no qualitative layer (it might be a rock song but a bad one).
   - Collaborative filtering, based on Item-to-Item relationship derived from explicit and implicit features (based on user interaction). Recommendations aren't based on a user's individual preferences but by collective preferences.
2. Data Exploration & Preparation
   - Use public dataset to experiment like *Movielens* and play in notebooks.
   - Filter to discard entry point with not enough information (e.g. less than n ratings for a given user, it might create noise otherwise)
   - Binary classification (e.g. liked if rating higher than 4, didn't like otherwise)
   - Matrix Factorisation with Factorisation Machines to simplify sparse datasets.
   - One-Hot encoding. Make a wide table with colums for all users and all movies and an additional one for rating. It will have a lot of zeroes so you can use `scipy.lil_matrix` to reduce the size of the set.
   - SageMaker takes the `lil_matrix` and turns into a *Protobuf* for the Matrix Factorisation engine.
3. Training
   - A few lines of code in the notebook to kick off the jobs
   - Evaluating the model with F1 score.
4. Optimisation
   - Add higher order features
   - Hyperparameters optimisation
     - Can give ranges of values to SageMaker which will apply ML on ML to find out better parameters
   - Use hybrid model
     - *Cluster* individuals users into groups (easier training and still relevant)
     - Sort prediction data sets based on *genres*
     - Generate predictions using the clustered user and filtered prediction data set that aligns best to the *application context*
   - Adding additional feature can improve accuracy (but increase training time)
   - Additional features help with *cold start* suggestions but can also worsen the model.
5. Deployment
   - SageMaker will deploy the container and provide an endpoint
   - Understand the inference *request format* for your algorithm
   - FM supports JSON & Protobuf
   - Use API Gateway and Lambda to convert from human friendly JSON to the One-Hot encoding that the model expects
   - Similarly, response can be enriched back into a friendly format.
   - You can A/B test between models