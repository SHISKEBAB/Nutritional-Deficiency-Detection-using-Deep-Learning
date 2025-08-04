# usage-mapper.md

## Usage Example – NHANESImageMapper

This example demonstrates how to use the `NHANESImageMapper` to pair tabular NHANES data with their corresponding image files.

The output is a dictionary containing training and testing data, each as a list of paired samples.

***

### Prerequisites

Make sure your project directory looks like this:

```
dataset/
├── NHANES/
│ └── merged_data.csv # Tabular data file
└── Image data/
├── train
├── test
└── ...
```

#### The \`merged\_data.csv\` file should contain a \`SEQN\` column whose values match the image filenames (without extension).

### Step-by-step Example

```
from data_manager import NHANESImageMapper

# Step 1: Instantiate the Mapper
mapper = NHANESImageMapper(
    tabular_path="dataset/NHANES/merged_data.csv",
    image_dir="dataset/Image data/"
)

# Step 2: Create Paired Dataset
paired_data = mapper.create_paired_dataset(test_size=0.2, random_state=42)

# Step 3: Inspect Output
print("Train size:", len(paired_data["train"]))
print("Test size:", len(paired_data["test"]))

# Sample structure of one paired entry
print(paired_data["train"][0])
# {
#   "image_path": "dataset/Image data/0012.jpg",
#   "features": {
#       "age": 25,
#       "bmi": 18.5,
#       ...
#   },
#   "label": "mild"
# }

```

### Notes

* Samples missing images or essential tabular values are automatically dropped.
* The `features` dictionary contains only the selected numerical columns.
* The `label` field should match the classification target (e.g., mild, moderate, severe).
