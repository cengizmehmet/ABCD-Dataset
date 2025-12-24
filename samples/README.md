# Representative Samples

This directory contains **representative sample files** illustrating the
structure and content of the Architecture-Based Consumption Dataset (ABCD).

The files provided here are **not exhaustive** and are intended solely to
demonstrate the data format, naming conventions, and level of detail present
in the full dataset.

---

## Contents

### CSV sample (single run)

The CSV file represents **one experimental run** of a deep neural network
architecture under a specific configuration.

Each CSV file:
- corresponds to a single execution
- contains timestamped measurements of power, current, and voltage
- follows the same column schema as all other raw runs in the dataset

The filename encodes the architectural configuration and training parameters
(e.g. optimiser, batch size, weight initialisation).

---

### JSON sample (aggregated runs)

The JSON file represents a **processed aggregation** of multiple experimental
runs belonging to a single architecture family.

Each JSON file contains:
- a fixed topological description of the architecture
- multiple configuration-specific results
- derived statistical descriptors computed from the raw measurements
- references to the original CSV files

This format provides a compact and structured abstraction over many individual
runs.

---

## Notes

- The folder structure used during data collection was for experimental
  convenience and does not carry semantic meaning.
- The full dataset contains additional architectures and runs following the
  same structure shown here.
- The complete dataset is available on reasonable request, as described in the
  main repository README.

These samples are provided to support transparency and reproducibility while
avoiding unnecessary duplication of large-scale experimental data.
