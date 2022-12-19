# DeepMirror Task (ML Engineer)

[1.Task and Thought Process](doc:link-to-pages#1.Task and Thought Process).

[Markdown - Link](#Link)

## Requirements
* Train a supervised graph neural network, a tree model and a transformer model
* Choose a dataset(s) from the TDC to train the models with
* Benchmark the performance of the models and choose an appropriate metric to compare them
* Summarise your findings in a format that can be clearly understood by the sales team

## 1.Task and Thought Process

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




