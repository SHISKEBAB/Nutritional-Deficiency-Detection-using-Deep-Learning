---
description: API Documentation – Nutritional Deficiency Detection Using Deep Learning
---

# README.md

Welcome to the API documentation for the **Nutritional Deficiency Detection** project. This guide provides detailed reference material for the internal Python modules and classes used in the system, particularly focusing on data handling and preparation.

***

### Overview

This project aims to detect nutritional deficiencies using a deep learning pipeline that leverages both image and tabular data.

This documentation is divided into:

* 📂 `custom_data_generator.py` – Multi-modal Keras data generator
* 📂 `data_manager.py` – Dataset preparation, mapping, and management
* 📂 Examples – Sample usage of core components in training/evaluation

***

### 🔧 Modules Covered

#### 1. `MultiModalDataGenerator`

> File: `custom_data_generator.py`

A Keras `Sequence` generator that merges image and tabular data for training multi-input models.

* Batch generation
* Augmentation support
* On-the-fly shuffling
* Feature scaling

***

#### 2. `NHANESImageMapper`

> File: `data_manager.py`

Responsible for:

* Reading tabular and image metadata
* Pairing image and tabular data
* Stratified train-test splitting
* Normalization and data formatting

***

### Getting Started

For installation and environment setup, refer to Getting Started.

***

### Examples

See the Examples folder for:

* Initializing data generators
* Mapping and pairing NHANES datasets
* Loading images and tabular features

***

### Contributing

This documentation is actively being developed. If you'd like to improve or extend the docs:

1. Fork the repository
2. Work on the `docs/` folder
3. Submit a pull request with reference to the relevant issue

***

### Related Links

* Project Repository: [GitHub Repo](https://github.com/25hency/Nutritional-Deficiency-Detection-using-Deep-Learning)
* Issue Tracker: [#12 – API Documentation](https://github.com/25hency/Nutritional-Deficiency-Detection-using-Deep-Learning/issues/12)

***

> Note: This documentation is meant for contributors and developers. If you're looking for how to **use** the model or retrain it, please check the usage guides in `getting-started.md`.
