# DSCI-8950 GraphSAGE Project

2025/05/11 - This version of the project organized into discrete files and folders for clarity and organization. All prior commits or previously uploaded data or files were moved to (and are still accessible from) the folder >>> 99.1 - Previous Commits <<<.

---
The purpose of this model is to test the application of three different data sets to one heterogenous graph model in node-and-edge format for the purpose of investigating the impacts of suspected environmental health hazards and contaminant movement pathways on local population health outcomes. To achieve this, nodes are constructed from data sets consisting of county, superfund and river data within the continental United States. 

## Introduction
---
The project applies GraphSAGE to model the potential relationships between Superfund sites, rivers and counties to predict the target variable: county cancer incidence (per 100,000 and age-adjusted). The goal is to identify correlations between environmental factors and local population health outcomes using graph-based, node-and-edge representations constructed from multiple data sets, and to test the utility of GraphSAGE is identifying and investigating the extent to which environmental hazards influence population level health outcomes. 

## Folder Structure
- .git: project history (please no one fiddle with .git)
- 1_data: folders for raw data, processed data, and unprocessed, unused files intended for future additions to project
- 2_notebooks: the notebooks created for the project. Create nodes, assemble heterodata object, test with Optuna, final model Tuning/Testing/Train/Evaluate
- 3_scripts: Scripts
- 4_models: Model weights, model Parameters
- 5_results: Results for final model tune/train/eval; additional folders for running multiple tests with different seeds/GPUs
- 6_docs: Meeting records, references, final report
- 7_.gitignore: .gitignore
- 8_README.ms: contains the README
	.gitattributes
	LICENSE

## Installation
---
(personal repository) The repository resides at: https://github.com/jsdriscoll/DSCI-8950-GraphSAGE-Project---jsdriscoll_branch
(group repository) The repository resides at: https://github.com/JeswanthReddy78/DSCI-2025-TEAM-F

```

## Usage
---
- Load the notebook: 1. DSCI8950_GraphSAGE_FINAL_MODEL_jDriscoll
- run the 'pip install' commands in Cell 01 to set up the environment.
- All necessary data is found in the github using the following paths:
  1. "001. GraphSAGE_Environmental_Model\02. Data\County_Mappings"
  2. "001. GraphSAGE_Environmental_Model\02. Data\CSV"
  3. "001. GraphSAGE_Environmental_Model\02. Data\River_Mappings"
  4. "001. GraphSAGE_Environmental_Model\02. Data\z. SingleFolderLoader"
  5. "001. GraphSAGE_Environmental_Model\02. Data\zz. Raw Input Data"
- Upload the files numbered 1, 2 and 3 in the bullet point above - or - upload the z. SingleFolderLoader file. 
- Review the Optuna Study settings in Cell 03 and the parameter space in Cell 10.  
  - The notebook is configured to perform an Optuna study with the following characteristics:

```
  - 300 trials
  - 500 epochs
  - patience number = 25
- the notebook defines the parameter space as:
```
  - The notebook is configured to perform an Optuna study with the parameters:

```
hidden_channels = trial.suggest_categorical("hidden_channels", [320, 384, 448])
lr = trial.suggest_float("lr", 3.2e-3, 4.6e-3, log=True)
dropout = trial.suggest_float("dropout", 0.16, 0.18)
weight_decay = trial.suggest_float("weight_decay", 4e-5, 6e-5, log=True)
num_layers = trial.suggest_int("num_layers", 3, 4)
aggr = trial.suggest_categorical("aggr", ["mean"])
activation = trial.suggest_categorical("activation", ["relu"])
batch_norm = trial.suggest_categorical("batch_norm", [False])
residual = trial.suggest_categorical("residual", [True])
accumulation_steps = trial.suggest_categorical("accumulation_steps", [10, 12])
```
  - Change the settings or parameters if necessary.
- The notebook is configured to do the following:
  - Create the node and edge graph form heterodata object form the files uploaded
  - conduct an Optuna study testing the parameter space for ideal parameters
  - conduct a single trial run of the GraphSAGE model using the best parameters found in the Optuna study
  - Perform ablation testing on features in each node
  - create runtime directories
  - deposit logs, plots, .jsons of Optuna results, final model results, ablation testing results and best parameters into the runtime directories

## Results 
---
Results will vary. It has been difficult to enforce deterministic behavior when transition into and out of PyTorch applications. The official final model run achieved an RMSE of **51.44** and an R2 of .22 using:

* Hidden channels: 384
* Learning rate: 0.00455
* Dropout: 0.170
* Residual connections: Enabled
* Aggregation: Mean

## Citing
---
If you use this work please cite my references, which can be found in the github folder: "001. GraphSAGE_Environmental_Model\05. Reference List"

## License
---
GraphSAGE Superfund Analysis  
Copyright (C) 2025 Jason Driscoll, University of Nebraska-Omaha

This program is free software: you can redistribute it and/or modify  
it under the terms of the GNU General Public License as published by  
the Free Software Foundation, either version 3 of the License, or  
(at your option) any later version.

This program is distributed in the hope that it will be useful,  
but WITHOUT ANY WARRANTY; without even the implied warranty of  
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the  
GNU General Public License for more details.

You should have received a copy of the GNU General Public License  
along with this program. If not, see <https://www.gnu.org/licenses/>.

## Usage Restrictions:
---
This project is hosted in a **private repository** to restrict access  
to authorized users. 

If you modify or redistribute this code, **you must make your modifications open source** and distribute them under the same license (GPL v3.0).  

If you wish to use this code outside of the university context,  
please contact **jdriscoll@unomaha.edu**. 