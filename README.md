# Rule mining over large knowledge graphs: two case studies in biosciences

This repository contains the data, Jupyter notebooks, and configuration pipelines for the paper **"Rule mining over large knowledge graphs: two case studies in biosciences"**. 

Our research demonstrates the application of a graph-based rule mining system, RDFRules (an extension of the AMIE approach), to discover interpretable patterns within two large-scale knowledge graphs: KG-COVID-19 and KG-Microbe. By avoiding the stochastic nature of model-agnostic explainers, our approach ensures that each prediction can be traced to a specific logical rule[cite: 2].

---

## 📂 Repository Structure

The repository is divided into two main directories corresponding to the two case studies presented in the paper.

### 1. `kg-microbe/`
This directory contains the resources for identifying cultivation media for microbes based on their phenotypic traits. The rule-based approach enabled multi-relational path extraction, allowing for the prediction of media for organisms where direct links were missing in the source data[cite: 2].

* **`data/`**: Contains the unfiltered dataset `kg-microbe.ttl` (tracked via Git LFS due to its size).
* **`notebooks/`**: 
  * `train_test_split.ipynb`: Handles the data partitioning into distinct training, validation, and testing sets while preventing data leakage.
  * `ruleset_request_generator.ipynb`: Automates the generation of rule mining tasks.
  * `rulemaker.json` & `support_rulemaker.json`: Templates used for rule generation.
* **`pipelines/`**:
  * `pruning.json`: Configuration for the data coverage pruning process to refine the candidate rules.
  * `prediction.json`: Pipeline configuration for generating predictions for microbes without a specified medium.
  * `evaluation.json`: Contains the complete evaluation metrics for the classification task.
  * `display_rules.json`: Used for extracting and visualizing the discovered rules.

### 2. `kg-covid19/`
This directory contains the resources for finding drug repurposing candidates and exploring mechanistic pathways, such as how Telmisartan affects the Renin-Angiotensin System via the AGTR1 receptor[cite: 2].

* **`data/`**: 
  * `kg-covid-19_nometa_shortened_20200925.nt`: The preprocessed snapshot of the KG-COVID-19 graph with metadata removed and URIs abbreviated.
  * `kg-covid-19_nometa_shortened_20200925.completed_withconst.nt`: The dataset after the rule-based knowledge graph completion phase.
* **`pipelines/`**: Contains the specific RDFRules JSON configurations used to run the exploratory analyses and pathway discoveries.
  * `kg_completion_high_confidence_rules.json`: Pipeline for imputing missing triples during preprocessing.
  * `find_drugs_ace1_ace2_via_intermediary.json`: Identifies drugs interacting with ACE1 and indirectly with ACE2.
  * `explore_indirect_drug_interactions_ace1_ace2.json`: Searches for indirect network connections for dual-target drugs.
  * `identify_shared_mechanistic_drug_targets.json`: Performs a mechanistic deep-dive to find common third-protein interactions (e.g., AGTR1).
  * `analyze_general_entities_co_interacting_ace1_ace2.json`: Analyzes the common characteristics of entities interacting with both ACE1 and ACE2.
  * `identify_gene_intermediaries_ace1_ace2.json`
  * `explore_alternative_interaction_paths.json`
  * `find_pathways_ace1_ace2_no_category_filter.json`

---

## 🚀 Getting Started

### Prerequisites
* **RDFRules**: The rule mining framework is open-source and can be accessed at [GitHub](https://github.com/propi/rdfrules) or the [RDFRules Website](https://rdfrules.vse.cz/index.html).
* **Git LFS**: Required to download the large `.ttl` and `.nt` graph datasets successfully. 
* **Hardware**: Successful replication of the experiments requires an environment with at least 64 GB of RAM.

### Usage
1. Clone the repository and ensure Git LFS pulls the large data files located in the `data/` directories.
2. For **KG-Microbe**, run the notebooks in `kg-microbe/notebooks/` to split the data, then feed the JSON configurations in `kg-microbe/pipelines/` to the RDFRules API.
3. For **KG-COVID-19**, use the pre-completed graphs in `kg-covid19/data/` alongside the JSON configurations in `kg-covid19/pipelines/` to replicate the rule discovery processes via RDFRules.

---

## 📖 Citation

If you use this repository or its data in your research, please cite our paper:

> **Hrudková, K., Kliegr, T., Ludvíková, D., Šimečková, J., & Joachimiak, M. P. (2025).** Rule mining over large knowledge graphs: two case studies in biosciences.
