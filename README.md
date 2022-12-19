# DeepMirror Task (ML Engineer)

Table of contents:

1. [Task and Thought Process](#1-task-and-thought-process)
2. [Benchmarks](#2-benchmarks)
3. [Key Metrics for Sales Team][#3-key-metrics-for-sales-team]

## Requirements
* Train a supervised graph neural network, a tree model and a transformer model
* Choose a dataset(s) from the TDC to train the models with
* Benchmark the performance of the models and choose an appropriate metric to compare them
* Summarise your findings in a format that can be clearly understood by the sales team

## 1 Task and Thought Process

### Stage 1: Dataset and learning about stuff
* Initially the very first thing I did was to take a look at the dataset, and I realised I have to get familiar with the terms and understand the data, so that I know what I am doing at all times.  
* So I went ahead and studied about ADME properties, Drug discovery, SMILES, molecular property prediction and understood how ADME works, this took me about *an hour* to catch on to terms.  
* At this stage I chose the HIA dataset since in my opinion the most common type of drug absorption is through the intestine, and the drug is taken orally most of the time, such as syrups, tablets etc.

### Stage 2: Training and tree model - Decision Trees
* The first hurdle was to extract features from the SMILES Strings, the first thing I found in google for "Extract features of SMILES Strings python" was a kaggle notebook where I came across PubChem, I decided to look more into this and I came across RDKit, which was a wonderful library, later i came across deepchem and followed the docs to extract features from SMILES Strings (link to docs - https://deepchem.readthedocs.io/en/latest/api_reference/featurizers.html#circularfingerprint)
* Since this was the easiest of all 3 models, and since I already have knowledge about decision trees (link to my blog: https://medium.com/@beekiran00/tree-algorithms-decision-trees-1c18d9fe429c), it took me about *15 mins* to prepare a model and train and test it.
* The code can be found in the repository at *Decision Tree Classifier.ipynb*

### Stage 3: A supervised graph neural networks
* This idea of building models with graph neural networks is totally new to me, as I have never come across this before. Therefore, I set out to stdy about graph neural networks in depth, and I started off by googling "graph neural networks"
* I followed this link - https://distill.pub/2021/gnn-intro/ and found it amazing as I understood the entire theory and concept. This took me *2 hours* as I was making notes along the way.
* Now that I have all the theory I Started looking for libraries to implement GNN. Surpsisingly DeepChem had a library to implement GNN which can be found in their docs, and they have featurisers, but I felt like it lacked something.
* PyTorch Geometric was a more robust and efficient way to implement a GNN with lots of help online, but all of them use an existing dataset which is MUTAG, TUdatses etc, which are already imported as graph objects. The hurdle here was to convert pandas DataFrame objects into graph data objects.
* I struggled with this for a few days (2 days) and it was a blocker. Soon I came across this link - https://www.blopig.com/blog/2022/02/how-to-turn-a-smiles-string-into-a-molecular-graph-for-pytorch-geometric/ that shows how to turn SMILES into a graph data object (gotta love open source!!)
* I followed their tutorial, and I now have a graph data object, Next I use the PyTorch Geometric to implement the GNN with the help of this documentation - https://uvadlc-notebooks.readthedocs.io/en/latest/tutorial_notebooks/tutorial7/GNN_overview.html#PyTorch-Geometric
* I then used Pytorch metrics to get the metrics of the model
* overall implementing this took 3 days

### Stage 4: Transformer Model - ChemBERTa
* I have worked with transformer models before, but I had to refresh my memory, therefore I went to do some research and brush up on the theory.
* Most of the use case for transformer models is NLP based, hence I searched for a way to extract features for SMILES Strings as they are.
* This is when I came across ChemBERTa - https://arxiv.org/abs/2010.09885 this model has been pretrained on PubChem 10M (glorious jackpot)
* To train the transformer model, I simply used this pre trained model, and used the HIA dataset to predict.
* this took me about 1 hours to do do.

### Stage 5: Benchmarks
* I took all the metrics, and created a document for model summary and sales team metrics
* This document also has the metrics for sales team to close the sale


## 2 Benchmarks

* The benchmarks for the models are compared on the following dataset:
* 
HIA (Human Intestinal Absorption), Hou et al.
Dataset Description: When a drug is orally administered, it needs to be absorbed from the human gastrointestinal system into the bloodstream of the human body. This ability of absorption is called human intestinal absorption (HIA) and it is crucial for a drug to be delivered to the target.

Task Description: Binary classification. Given a drug SMILES string, predict the activity of HIA.

Dataset Statistics: 578 drugs.

Dataset Split: Random Split Scaffold Split

### Time vs Model

* The models took time varying with eachother, below is a graph that shows time taken to trian and test a model


![image](https://user-images.githubusercontent.com/63056373/208525051-28882e50-c605-46c2-a69b-6e4b84aeac8a.png)

* The transformer model took about 45 mins to train and test, this is presumably because this is a pre-trained model.

### Metrics

* the chart below shows the metrics comparision across the three models. Since this was a classification task, the classification metrics are benchmarked


![image](https://user-images.githubusercontent.com/63056373/208525339-b54841c9-a237-41b8-961c-ce6cbb74076d.png)

* Overall GNN model had the best ROC-AUC score to time. Although transformer model had the best ROC-AUC score, it took a lot of time to run, where as the GNN model had a decent ROC-AUC score, where the threshold was 0.80 along with the highest accuracy, it makes it the best model

## 3 Key Metrics for Sales Team
* when the sales team is making the sales, ideally nobody wants to hear numbers that do not make sense to them, therefore the sales team can close the deal with accuracy - which indicates how good the model predicts, and ROC-AUC score - closer to 1 the better 


![image](https://user-images.githubusercontent.com/63056373/208525782-7263daba-6557-4e2c-bec3-6207f13b88de.png)

* Accuracy shows how accurately the model predicts the output, in this case the HIA of
a drug - Decision tree has the lowest accuracy and low ROC-AUC score
* Transformer model has the best ROC-AUC score, around 0.98 and decent accuracy
but takes unoptimal amount of time
* GNN is the best model overall with the best metrics considering accuracy and
ROC-AUC, the main trade-off made here is time, and ROC-AUC score with a
threshold of .80



