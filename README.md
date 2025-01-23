# Repository for the Master Thesis: _GMR-ND: A Graph Neural Network Approach for Novel and Diverse Music Recommendations_

Master Thesis by Timo Rodinger


## Project Context

With the growing size of musical
content on digital music streaming services, users can be overwhelmed
by the number of possible songs to choose from. Music recommendation models help to make personalized song recommendations based
on users’ preferences. Many traditional approaches in music recommendation systems focus on providing recommendations that bring
the highest click rates and revenue, but neglect the importance of recommending novel and diverse songs in order to broaden the user’s
listening horizon. Hence, it is important to introduce recommendation
models that focus on recommending novel and diverse songs. 

The work of Tomasel et al. (https://github.com/tommantonela/umap2022-mrecuri), proposes MRecuri (Music RECommender for
filter bUbble diveRsIfication), a model that employs mechanisms such
as a Hybrid Graph-Neural Networks and a customized loss function,
as well as specific evaluation metrics which aim to increase aspects of
novelty and diversity in the model’s recommendations.

## Project Objectives

This Master thesis project had two main parts. First, the reproduction of the MRecuri music recommender model for results verification was conducted. The replication model can be found in notebook number 6, "6. MRecuri_Replication.ipynb". 

Second, a novel music recommendation system using Graph Neural Networks (GNNs) built with PyTorch Geometric was implemented, which used the same data and similar methods as the MRecuri model. The novel GMR-ND approach analyzes user-song interactions, user friendships, and song-artist relationships to generate personalized music recommendations. 

The goal was to find out if an extension of the MRecuri model in a full GNN approach using PyGeometrics was possible at all, and second, if the performance could be increased compared to the MRecuri model. Furthermore, since the reproduction of the MRecuri model proved very difficult due to missing data and documentation, this thesis provides full transparency in the scientific process to enable results verification and re-use of the provided methods.

## Evaluation Data

All models, including the replicated MRecuri model, the novel GMR-ND models and benchmark models are evaluated on data collected from Last.fm. For auxilary information tags and audio features data from last.fm were used. Note that the same user-track listening relations as in the MRecuri study are used. For tags and feature data, the data was scraped seperately.

## Notebooks Overview

A brief overview on the functionality of each notebook and how their artifacts relate to each other. The notebook structure is designed to be run sequentially, with data and model artifacts being passed between them.

### 1. Data Inspection and Preprocessing.ipynb
- Re-uses graph data from the MRecuri study (https://github.com/tommantonela/umap2022-mrecuri/blob/main/README.md)
- Processes raw listening history data and corrects user, song, and artist information
- Prepares data for PyGeometrics graph creation

### 2. Train, Test, Full Graph_Transformation.ipynb
- Constructs the heterogeneous graph structure as PyTorch Geometric data objects that are used in Notebook 5
- Manages data splitting into full, training and testing sets
- Outputs input graphs for model training and inferences used in Notebook 5
- #### Heterogeneous Data Structure
  - Node Types:
    -  Users
    -  Songs (with audio and tag features)
    -  Artists (with tag features)
  - Edge Types:
    - User-Song (listens_to)
    - User-User (is_friends_with)
    - Artist-Song (makes)


### 3. Embeddings, Distances and Cosines.ipynb
- Creates the pre-computed cosine distances for a customized loss function that aims to increase novelty and diverstiy. Used by the custom loss function in the replicated MRecuri model (Notebook 6) and in the novel GMR-ND models (Notebook 5)

### 4. Novelty and Diversity Setup.ipynb
- Sets up the structural and content-based embeddings 
- Necessary for the calculation of novelty and diversity metrics (Notebook 7)
- Outputs the structural and content-based embeddings

### 5. GCN_Music_Recommender_PyG.ipynb
- Contains the extension models (GMR-ND)
- Holds 4 GMR-ND model variation to test architectural features. Rich vs Shallow node features and custom vs binary-cross entropy loss are tested. 
    - Shallow GNN with binary loss
    - Shallow GNN with custom loss
    - Rich GNN with binary loss
    - Rich GNN with custom loss
- Implements model training and prediction 
- Outputs GMR-ND recommendations for users

### 6. MRecuri_Replication.ipynb
- Contains the replicated MRecuri code
- Adjustments had to be made to the original code by Tomasel et al. 
- Outputs MRecuri recommendations for users

### 7. Benchmark Models and Results.ipynb
- Contains the final model evaluations
- Sets up benchmark models and their predictions
- Sets up all relevant metrics
    - Precision
    - nDCG
    - structural Novelty 
    - structural Diversity
    - content-based Novelty
    - content-based Diversity
- Creates results evaluation of all model recommendations
- Creates statistical analysis of results
- Outputs final results and significance tables


### 8.1 LastFM_API_Call.ipynb
- Collects tag data

## Data Folder Structure

The data for this work can not be shared publically due to copyright reasons. 
To run the notebooks sequentially you can use the input data as provided by Tomasel et al. (https://github.com/tommantonela/umap2022-mrecuri).
For quesionts regarding code or data please reach out to me. 

## Requirements for the MRecuri Replication Model
- Python 3.11.8
- Spektral 1.3.1
- Keras 2.15.0
- NetworkX 3.2.1

## Requirements for the GMR-ND (Extension Model)
- Python version 3.12.2
- PyTorch 2.2.2+cu118
- PyTorch Geometric 2.5.3
- NetworkX 3.2.1
