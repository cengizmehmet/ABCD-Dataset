# Architecture-Based Consumption Dataset (ABCD)

## Overview

The **Architecture-Based Consumption Dataset (ABCD)** is a large-scale experimental dataset capturing power, current, and voltage measurements collected during the execution of deep neural network architectures under diverse configurations.

The dataset was generated as part of a PhD thesis at Newcastle University and is intended to support research on power estimation, architectural generalisation, and continual learning for deep neural networks, particularly in resource-constrained or edge-computing settings.

Due to its size, this repository focuses on **documentation, metadata, and representative structure**, rather than hosting the full dataset directly.

---

## Dataset composition

The dataset consists of two complementary data representations:

1. **Raw experimental runs (CSV files)**  
2. **Processed, aggregated summaries (JSON files)**  

Together, these capture both fine-grained measurements and higher-level architectural abstractions.

---

## Raw CSV files (individual runs)

Each CSV file corresponds to **one experimental run** of a specific neural network architecture under a particular configuration (e.g. optimiser, batch size, weight initialisation).

### File naming convention

CSV filenames encode the experimental configuration, for example:

conv_1x3_maxpool_untrained_10x16_constant_adamw.csv

The folder structure used during data collection was designed for experimental convenience and does **not** carry semantic meaning for reuse.

### CSV structure

All CSV files follow a consistent schema with **10 columns**, including:

- A timestamp column  
  - Recorded at approximately 20 ms intervals in the original measurements  
  - Converted to milliseconds during processing  
- Power, current, and voltage measurements  
- Minimum, maximum, and average statistics for each signal  

These files represent the raw measurement level of the dataset.

---

## Processed JSON files (aggregated summaries)

To facilitate analysis and reuse, raw CSV runs are aggregated into **processed JSON files**, each corresponding to a **specific architecture family**.

### JSON structure

Each JSON file is organised as follows:

- **Root key**: architecture identifier (e.g. `conv_1x3_maxpool`)
- **`layers`**: a fixed topological description of the neural network architecture  
- **`configuration_outputs`**: a collection of experimental runs for that architecture  

Each entry in `configuration_outputs` contains:
- A reference to the original CSV file
- Training and configuration parameters (e.g. optimiser, batch size, learning rate)
- A set of derived statistical descriptors computed from the raw measurements

### Example structure (simplified)

```json
{
  "conv_1x3_maxpool": {
    "layers": [
      {
        "category": "dense",
        "type": "input",
        "shape": [224, 224, 3]
      }
      // following layer information omitted
    ],
    "configuration_outputs": [
      {
        "Path": "conv_1x3_maxpool_untrained_10x16_constant_adadelta.csv",
        "Weights": "untrained",
        "LR": "Constant",
        "Num_Batches": 10,
        "Batch_Size": 16,
        "Optimizer": "Adadelta",
        "Stats": {
          "Avg_Current_mean": 976.62,
          "Avg_Voltage_mean": 5.28,
          "Avg_Power_Simpson": 38.08
          // additional statistics omitted
        }
      },
      // additional outputs with various metrics omitted
    ]
  }
}
```

In total, the dataset comprises **over 1,000 raw CSV files** and **fewer than 50 processed JSON files**, which provide a compact, structured representation of the experimental results.

---

## Data availability

The full dataset exceeds several hundred gigabytes in uncompressed form and therefore cannot be hosted directly in this repository.

This repository serves as a **documentation and metadata record**, and may include representative samples illustrating the structure of the data.

The complete dataset is stored internally at Newcastle University and can be made available on reasonable request under institutional and supervisory oversight.

## Contact

For access requests or further information:

**Mehmet CENGIZ**

Email: [REDACTED]

---

##Related work

- PhD Thesis:

Generalising Performance Prediction via Incremental Topology Exploration of Deep Neural Networks and Continual Learning

Mehmet CENGIZ, Newcastle University

---

##Licence

This repository is distributed under the MIT License. Please see the [`LICENSE`](LICENSE) file for details.


