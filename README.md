# tfm-fraud-detection

# Project overview
The project models transactional data as a graph and applies Graph Neural Networks to detect fraudulent behaviour in banking and insurance transactions. The workflow follows the typical lifecycle of a graph ML project:

* Load and explore the IEEE‑CIS fraud dataset.
* Transform tabular data into a graph structure.
* Load the graph into Amazon Neptune as an OLTP graph store.
* Train a GNN model with GraphStorm.
* Deploy the trained model as a real‑time inference endpoint on Amazon SageMaker.

Each step is documented in a separate notebook, exported here as PDF files for easier viewing and reproducibility.

Repository structure:
* 1_Data_Loading_and_EDA.pdf
Exploratory Data Analysis notebook.
Describes the IEEE‑CIS fraud dataset and its main tables.
Performs data cleaning, basic feature inspection and visualization (class imbalance, amount distributions, correlations).
Motivates which attributes will later be used to construct the graph and the ML features.

* 2_Create_Graph_Dataset.pdf
Graph construction notebook.
Shows how tabular transaction data is transformed into a heterogeneous graph of transactions, cards, devices, emails, etc.
Defines node and edge types, IDs and feature schemas.
Exports node and edge CSV files in the format required by GraphStorm and Amazon Neptune.

* 3_Loading_to_Neptune.pdf
Graph loading and OLTP setup.
Describes the creation of the Neptune cluster and the configuration used in the experiments.
Demonstrates how the vertex and edge CSVs are bulk‑loaded from Amazon S3 into Neptune.
Includes example Gremlin queries to inspect the resulting graph and to retrieve neighbourhoods around a transaction.

* 4_Model_Training.pdf
GraphStorm model training notebook.
Configures and trains the GNN model on the graph dataset (hyperparameters such as learning rate, dropout, batch size, number of layers).
Logs training loss and ROC AUC per epoch.
Compares different regularisation settings and selects the best model based on validation ROC AUC.
Saves the trained model artifacts for deployment.

* 5_SageMaker_Inference_Endpoint_Creation.pdf
Deployment and real‑time inference.
Packages the trained GNN model and uploads it to Amazon SageMaker.
Creates a real‑time inference endpoint and connects it to Neptune for graph queries.
Shows example requests that send a transaction, retrieve its neighbourhood from Neptune, invoke the endpoint and obtain a fraud probability score.
