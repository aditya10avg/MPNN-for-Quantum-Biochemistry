# Predicting Quantum Properties of Organic Molecules using Neural Networks

## Overview

This project explores using neural networks to predict the **Quantum Mechanical Properties** of organic molecules. By leveraging the power of machine learning, we aim to enhance the understanding of molecular interactions and their biochemical behavior, which can have significant applications in **drug discovery** and molecular biology.

Our approach uses **Message Passing Neural Networks (MPNN)** to process molecular graphs and predict quantum properties, focusing on how atoms (nodes) and bonds (edges) in a molecule interact and share information.

### Dataset: QM9

We utilize the **QM9 dataset**, which contains data on **130,000 molecules** with **13 quantum mechanical properties** for each molecule. These properties were predicted using **Density Functional Theory (DFT)**, a popular but computationally expensive quantum mechanics simulation method.

---

## Key Phases of the Neural Network Model

### 1. Message Passing Phase

In this phase, the model simulates the interaction between atoms. Each node (atom) receives and processes messages from its neighboring nodes, updating its **hidden state**. The exchange of information continues over multiple iterations, allowing the network to model how atoms influence one another.

### 2. Readout Phase

Once the message-passing phase completes, the **readout function** aggregates information from all nodes (atoms) and edges (bonds) in the graph. The final prediction, representing a specific **quantum property** of the molecule, is made from the processed data of the entire graph.

---

## Analogy

In the context of the molecular graph representation:

- **Nodes** represent **atoms**.
- **Edges** represent **bonds** between the atoms.

---

## Models Used and Research Papers

### 1. CNN for Learning Molecular Fingerprints
- Learns information from both nodes and edges but separately.
- Fails to capture the interaction between nodes and edges.

### 2. Gated Graph Neural Networks (GGNN)
- Enables nodes in the graph to exchange information with each other over several steps.
- Combines updated node states for final prediction.

### 3. Interaction Networks
- **Message Function:** Generates messages by combining hidden states of connected atoms and bond types.
- **Update Function:** Updates the hidden states of atoms.
- **Molecule-level Output:** Combines all atom and bond information to predict properties like molecular stability and energy levels.

### 4. Molecular Graph Convolutions
- Updates atom info as well as the molecular info during the message phase.
- Helps the model learn how molecules behave by understanding how atoms and bonds influence each other.

### 5. Deep Tensor Neural Networks
- Uses the "tanh" function to pass short, smooth, and manageable messages between atoms.

### 6. Laplacian-based Methods
- Uses CNN on graphs by passing messages through nodes using Eigenvectors.

---

## Accuracy Benchmarks

We measure performance against:
1. **DFT error** – Error compared to DFT predictions.
2. **Chemical accuracy** – Quantum chemical accuracy of predicted properties.


## Virtual Graph Elements

There are two approaches to sending a message --
1. Virtual Edge 
2. Master Node
i. **Virtual Edge** – This allows information to travel long distances during the propagation phase.
ii. **Master Node** – A master is connected to every node in the network and acts like a shared workspace that all nodes can read from and write during communication.

## Readout functions ;-
Two ways of reading are 
1. Gated Graph Neural Network- Gather and sum up/add the information that each node has learned.
2. set2set - It creates a summary of information that doesn't depend on the order of nodes. It takes the final state of each node, and applies transformation (linear projection) to combine each node's state with its features. It  creates a summary of the whole graph.

   ---

### Multiple Towers

- One challenge is that processing large graphs with many nodes & features can become very slow and use a lot of compute power .When graphs has many nodes & each node has many features the number of operations needed ncreases a lot.

- To fix this , we split features of each node in smaller groups. E.g If a node has 100 features split them into 5 groups of 20 features each. 

- We then process each group separately by using its own message passing step. 

- The separate results from each group are combined to form final node representation. 

- This reduces computation cost and time taken for the model to learn while still capturing the necessary information from graphs.


### Input Representation

This deals with different possible ways in which atoms and their bonds are represented in a molecule while building a model and also observe the how fast the model learns using each representation and also to understand the structure of molecule.

1. Atom Features - Each atom in a molecule has certain features like it's electrons , no. of H atoms , bonds with other atoms etc
   One possible way would be to include Hydrogen atoms as separate nodes in the graph but this would slow down the model. (about 10 times slower)

2. Adjacent Matrices
   This matrix shows how atoms are connected (bonds between atoms).
   We can use 3 types of ways to represent edges(bonds) between atoms depending on the model.

3. Chemical bins - When using distance between atoms, group distances into 10 bins.
     These bins cover distance from 0 to infinity and are based on how far apart atoms are in the molecule. Bond types were also included so the matrix shows both bond type and distance.

4. Raw Distance Feature-
    When using a more complex function to pass information information, include the exact distance between atoms and encode the bond type ( using 1 for present and 0 for not present) 



## Next Steps

This project is in its early stages, with the outlined concept and models forming the basis of development. The next step involves building and fine-tuning these models on the QM9 dataset to optimize their ability to predict molecular properties for drug discovery.

Stay tuned for further developments and code implementation!
