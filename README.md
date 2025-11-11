# Multi-Modal-Intelligent-Fault-Detection-System-for-Electric-Grids-
Multi-Modal Intelligent Fault Detection System for Electric Grids using Graph Neural Networks and Large Language Models
1. Introduction
This project, titled “Multi-Modal Intelligent Fault Detection System for Electric Grids using Graph Neural Networks (GNNs) and Large Language Models (LLMs)”, was developed as a proof of concept (POC) during my tenure at Saudi Electricity Company (SEC).
The primary goal was to create an intelligent and explainable AI-based system capable of identifying, localizing, and diagnosing faults in complex electrical grids. Traditional fault detection systems rely heavily on threshold-based methods or physical models, which often fail to generalize under dynamic load conditions. This project combines the strengths of graph-based learning and language-based reasoning to bridge that gap.

2. Project Objective
The objectives of this work were:
Represent the electric power grid as a graph structure, where buses are nodes and transmission lines are edges.


Use Graph Neural Networks to predict abnormal behavior and localize potential faults in the grid.


Integrate GNNExplainer for interpretability to identify the most influential nodes and transmission lines contributing to faults.


Develop a domain-tuned LLM that interprets GNN outputs and generates a human-readable fault diagnosis report.


Build a unified and scalable pipeline deployable in real-time grid monitoring systems.



3. Methodology
3.1 Graph Representation
The IEEE 24-bus system was used to model the electrical grid. Each node represented a bus with voltage and load parameters, and each edge represented a transmission line with impedance and power flow features. The data was preprocessed into a PyTorch Geometric (PyG) graph structure for downstream analysis.
3.2 Graph Neural Network (GNN) Model
A GraphSAGE model was trained for node-level regression, predicting fault-related values such as voltage deviation and reactive power imbalance.
 Hyperparameter tuning using Optuna was performed across 30 trials, with the best configuration as follows:
Parameter
Value
Hidden Size
128
Layers
4
Learning Rate
6.55e-4
Dropout
0.0
Weight Decay
1.6e-6
Epochs
30

The model achieved a Test MSE of 0.7319 and a Test MAE of 0.183, demonstrating strong predictive accuracy for fault-prone nodes.
3.3 Explainability with GNNExplainer
To make the predictions interpretable, GNNExplainer was implemented to identify critical nodes and transmission lines affecting a faulted bus.
 For each detected anomaly, the explainer visualized the subgraph region and highlighted how voltage instability propagated through the network. This step enhanced model transparency and provided engineering insights into inter-bus dependencies.
3.4 LLM for Fault Diagnosis
The next stage focused on generating natural language fault explanations.
 Outputs from the GNN and GNNExplainer modules were converted into structured text prompts containing:
Top affected nodes and their scores


Implicated transmission lines


Severity of the fault


Influential components from GNNExplainer


A LoRA (Low-Rank Adaptation) fine-tuned model, based on Phi-3 Mini and OPT-1.3B, was trained on these prompts.
 The LLM learned to transform the GNN outputs into concise and domain-specific diagnostic summaries. Each response followed a structured format:
Diagnosis:
- Most probable fault location:
- Evidence from GNN output:
- Impact on grid stability:

This allowed the model to generate technically accurate fault descriptions and suggest corrective measures such as load shedding, relay verification, and line isolation.
3.5 Integration and Pipeline
A full pipeline was created that:
Accepts graph data of the grid.


Performs GNN-based fault prediction.


Uses GNNExplainer for interpretability.


Passes structured summaries to the fine-tuned LLM for natural language diagnosis.


The integrated system was developed in Python, using PyTorch Geometric, Transformers, and Optuna, and tested on Azure AI Foundry for deployment feasibility.

4. Results
Model Performance:


Test MSE: 0.7319


Test MAE: 0.183


Explainability:


GNNExplainer successfully identified key subgraph structures affecting faults.


LLM Diagnostic Output:


The fine-tuned model generated context-aware, technically sound fault reports.


Example:

 “Most probable fault location: Bus 14. The GNNExplainer shows high influence from buses 15 and 16, indicating a localized voltage collapse risk. Suggested action: verify line 58 and isolate Bus 14 temporarily.”




5. Key Contributions
Designed and trained a GraphSAGE-based GNN for electrical fault localization.


Implemented explainable AI using GNNExplainer to ensure transparency.


Created a domain-aligned prompt generation framework for LLM fine-tuning.


Fine-tuned a lightweight transformer (Phi-3 Mini) for fault report generation.


Built a fully integrated, multi-modal AI pipeline deployable for real-time grid analytics.



6. Conclusion
This project demonstrates how graph learning and language modeling can be effectively combined for fault detection and interpretation in electric power systems.
 The GNN provided numerical precision for fault prediction, while the LLM added explainability and human-level reasoning to the diagnosis process.
This multi-modal integration can serve as a foundation for autonomous grid management systems, AI-assisted control centers, and digital twins of power networks in the near future.
