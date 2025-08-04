# getting-started.md

## Getting Started

Welcome! This guide will help you set up and run the **Nutritional Deficiency Detection using Deep Learning** project on your local machine.

***

### Prerequisites

* Python ≥ 3.8
* Git
* Virtual environment tool (optional but recommended)

***

### Installation Steps

#### 1. Clone the Repository

```bash
git clone https://github.com/25hency/Nutritional-Deficiency-Detection-using-Deep-Learning.git
cd Nutritional-Deficiency-Detection-using-Deep-Learning
```

2. (Optional) Create a Virtual Environment

```
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

#### 3. Install Dependencies

```
pip install -r requirements.txt
```

### Project Structure

```
├── custom_data_generator.py      # Multi-modal Keras data generator
├── data_manager.py               # NHANES data pairing and management
├── train_multimodal.ipynb        # Training logic
├── evaluate_multimodal_model.ipynb # Model evaluation
├── dataset/                      # Folder for images and tabular CSVs
└── docs/                         # Documentation (you're here)
```

### Dataset Setup

You need the NHANES dataset with the following structure:

```
dataset/
├── NHANES/                # Tabular data (.csv)
│   └── merged_data.csv
└── Image data/            # Image data
    ├── test
    ├── train
    └── ...
```

Make sure:

* The tabular CSV contains a `SEQN` column
* Image filenames match the corresponding `SEQN` (e.g., `0001.jpg` ↔ `SEQN=0001`)

### Running Training

```
jupyter notebook train_multimodal.ipynb
```

Inside, you'll see:

* Preprocessing steps using `NHANESImageMapper`
* Data loading with `MultiModalDataGenerator`
* Training using a multi-input Keras model

### Running Evaluation

Likewise, open and run:

```
jupyter notebook evaluate_multimodal_model.ipynb
```

### Troubleshooting

* If images fail to load, check that filenames match the `SEQN` values.
* If you see missing features, check your CSV headers for typos.
* For memory errors, reduce batch size or image resolution.

### Contributing

For contribution guidelines and documentation help, check the [README.md](./)
