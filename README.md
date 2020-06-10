<p align="center">
  <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/title.png></img>
 
  ## Table of Contents

- [Basic Overview](#basic-overview)
  - [Background](#background)
  - [Goal & Motivation](#goal-and-motivation)
- [Exploring the Data](#exploring-the-data)
  - [Molecule Representation](#molecule-representation)
  - [Preprocessing](#preprocessing)
- [Predictive Model](#predictive-model)
  - [Generating New molecules](#generating-new-molecules)
- [Work In Progress](#work-in-progress)
- [Future Considerations](#future-considerations)



## Basic Overview

### Background
In the fields on medicine, biotechnology and pharmacology, developing a new drug from start to finished product is a complex process which can take years and cost billions of dollars. Even before the drug development begins, building up a body of supporting evidence before selecting a target can be costly. The initial research generates data to develop a hypothesis that the inhibition or activation of a protein or pathway will result in a therapeutic effect in a disease. The outcome of this is the selection of a target which ultimately can lead into the discovery phase in order to justify a drug discovery effort. 

Once the root/mechanism of a certain disease is discovered, identifying a compound that effectively treats the disease without serious side effects may make for a long and laborious journey. The candidates for a new drug to treat a disease might include 5,000-10,000 chemical compounds which were picked from millions. On average 2-5% of those candidates will show sufficient promise for further evaluation. The high failure rate associated with pharmaceutical development can be attributed to careful decision making during drug development to avoid costly failures. Also, factors that can make potential compounds considerably difficult to consider as a candidate is toxicity, bioavailability, and other physiochemical features. 

<p align="center">
  <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/Drug-discovery-value-chain-1.jpg></img>
  
 ### Goal and Motivation
 
Neurodegenerative diseases are currently incurable and result in debilitating conditions, Parkinson's and Huntingtons disease being one of the most severe and common ones. Although more rare, spinal muscular atrophy (SMA) is the leading genetic cause of infant mortatlity and childhood disability caused by the loss of function of the survival motor neuron 1 (SMN1). Motivated to expand off of my previous capstone in university, I am looking to see if a neural network is able to generate novel molecules and then ultimately see if it can generate similar molecules to the newest drug in trials to treat SMA, risdiplam. 

In 2017, the drug nusinersen, marketed as Spinraza, by Biogen was released to treat SMA, at the price of $750,000 the first year and then $375,000 anually. Additionally, the drug is painfully administered intrathecally(injected directly into the spinal cord to reach the cerebral spinal fluid) and is an antisense oligonucletide (ASOs) aimed at increasing the amount of functional full lenght SMN protein. For a more in-depth look into the mechanisms and potential treatments for SMA, I will provide a link to my research proposal below.

[Spinal Muscular Atrophy Research Proposal](/https://drive.google.com/file/d/1pST7g_NXvMu7DsCHVog7aexyfkU_-Am3/preview')

Although a naive way of generating molecules, generating novel molecules with the help of machine learning can possibly accelerate the way we identify potential compounds and could drastically reduce the drug discovery cost. 


## Exploring the Data

### Molecule Representation

The goal is to generate molecules with a recurrent neural network. These molecules will most likely not be valid but the idea is to train the model to learn patterns our training molecules to produce some similar molecule. Of course, molecules are traditionally represented with a chemical formula such as C16H18N2O4S (penicillin) or a structural formula. Fortunetely for us, molecules can also be written in string format that is able to be put through a neural network similarly when doing natural language processing. Here is what penicillin would like in its structural format and the string format denoted as SMILES. 

<b>SMILES FORMULA FOR PENICILLIN : CC1=CN2N=C(C=C(C)C2=N1)C1=CC(=O)N2C=C(C=CC2=N1)N1CCNC2(CC2)C1 </b>

<p align="center">
  <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/penicilin_mol.png width='400'></img>


The data was obtained from zinc15.docking.org which contains hundreds of millions of molecules that can be downloaded. Luckily, the have the option of downloading the molecules in SMILES format. 

### Preprocessing

Here, we will be using a Recurrent Neural Network with a couple layers consisting of LSTMs. The first step was to create a mapping of characters to integers to allow the neural network to process the data and in end we can translate the results back to characters to make them readable to humans. In SMILES string, they contained special characters like "/", "=", etc and elements of the periodic table such as "C", "N", "O", etc. Using NumPy, we can reshape the input array into a format for recurrent models. The output variable y was encoded to be the the preceeding atom of the molecule string from X. The molecules were split at random and the next atom was the y variable to be predicted. 

## Predictive Modeling

The recurrent neural network used consisted of two LSTM layers and added a dropout regularization after each layer, followed by a dense output layer that used the softmax activation function. Here, it takes the output vector y and returns a probability distribution with the indices corresponding to the dictionary we used to convert our characters to integers. I used the categorical cross entropy as the loss function and the Adam Optimizer. 

<p align='center'>
          <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/lstm.png></img>

### Generating New Molecules

Generating new molecules after training was more involved than a simple call of predict on the model. First, we can import the checkpoints that were saved from training so that we don't have to retrain the model. As the input, we select a random SMILES string from the dataset as a reference, and then we can generate a specified number of characters. Similarly to mapping the characters to integers we can then map the output back to characters. Ideally, we want to get an output that resembles something like a molecule. 

<p align='center'>
  <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/generate_molecule.png></img>
  
  Here is a SMILES string generated from the neural network! Although it is quite long, at first glance the string looks like it could be a possible molecule comparing it to the penicillin one above. Although it is uncommon for drugs-like compounds to be this big, other molecules can get very large. 
  
  ## Work In Progress
  
  The goal for this project was to generate molecules similar to the newest drug in clinical trials to treat Spinal Muscular Atrophy, risdiplam. Below is the structural formula for risdiplam. 
  
<p align='center'>
  <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/risdiplam.png></img>
  
  Similarly to producing a molecule by starting with a random SMILES string as a reference, we could take a portion of the the risdiplam molecule as a reference point and produce a novel molecule from there. Unfortuntely, the way the neural network was setup it only takes in a specific length of reference string which was longer than the risdiplam molecule itself. A technical point for training I overlooked was not training the neural network of varying sequence length. Future work will focus on generating novel molecules from reference molecules.
  
  ## Future Considerations
  
  This project is an example of a very basic way molecules can be generated with neural networks. Ideally, combining other machine learning such as reinforcement learning would increase the validity of these molecules greatly. One of the pitfalls in this basic model is the complex consideration of the properties molecules have and their restrictions of what make it valid. Another consideration is a way to score and filter out molecules such as classification into active and inactive. 
    - Random Forests could be used for classification of active and inactive molecules
    - Finding the optimal molecular properties and binding to a specific site
    - Transfer learning, refitting the pretrained model with a small data set specific to the target of interest.
