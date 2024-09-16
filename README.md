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

---

## Next Steps

This project is in its early stages, with the outlined concept and models forming the basis of development. The next step involves building and fine-tuning these models on the QM9 dataset to optimize their ability to predict molecular properties for drug discovery.

Stay tuned for further developments and code implementation!
