# usage-generator.md

## Usage Example – MultiModalDataGenerator

This example shows how to use the `MultiModalDataGenerator` to create training batches from **paired tabular and image data**.

The generator is designed for multi-input Keras models that expect:

* Preprocessed tabular features
* Resized image tensors
* One-hot encoded labels (if applicable)

***

### Step-by-Step Example

```python
from custom_data_generator import MultiModalDataGenerator
from data_manager import NHANESImageMapper

# Step 1: Map and pair the dataset
mapper = NHANESImageMapper(
    tabular_path="dataset/NHANES/merged_data.csv",
    image_dir="dataset/Image data/"
)
paired_data = mapper.create_paired_dataset()

# Step 2: Initialize the generator
generator = MultiModalDataGenerator(
    dataset=paired_data["train"],
    batch_size=16,
    image_size=(224, 224),
    augment=True,
    tabular_features=["age", "bmi", "vitamin_d", "calcium"],
    num_classes=3  # One-hot encoded label output
)

# Step 3: Fetch a batch
(inputs, labels) = generator[0]
image_batch, tabular_batch = inputs

# Step 4: Inspect shapes
print("Image batch shape:", image_batch.shape)        # e.g., (16, 224, 224, 3)
print("Tabular batch shape:", tabular_batch.shape)    # e.g., (16, 4)
print("Labels shape:", labels.shape)                  # e.g., (16, 3)
```

#### Generator Output Format

Each batch returns:

```
([image_batch, tabular_batch], label_batch)
```

This is fully compatible with multi-input Keras models:

```
model.fit(generator, epochs=10)
```

#### TIPS:

* `augment=True` applies random image transformations to boost generalization.
* Ensure `tabular_features` match those used in model design and data preprocessing.
* You can also use `generator["test"]` to validate during training.

#### Next Steps

Build a multi-input model and start training using this generator.\
See your training notebook (`train_multimodal.ipynb`) for full integration.
