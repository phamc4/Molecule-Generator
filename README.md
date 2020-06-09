<p align="center">
  <img src=https://github.com/phamc4/Molecule-Generator/blob/master/images/title.png></img>
 
  ## Table of Contents

- [Basic Overview](#basic-overview)
  - [Background](#background)
  - [Goal & Motivation](#goal-and-motivation)
- [Exploring the Data](#exploring-the-data)
  - [Molecule Representation](#molecule-representation)
  - [Preprocessing](#preprocessing)
- [Predictive Modeling](#predictive-modeling)
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

### Preprocessing

Here, we will be using a Recurrent Neural Network with a couple layers consisting of LSTMs. 
