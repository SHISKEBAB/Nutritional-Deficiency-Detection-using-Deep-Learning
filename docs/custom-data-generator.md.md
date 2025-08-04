# custom-data-generator.md

The `MultiModalDataGenerator` is a custom Keras `Sequence` class that enables training with **multi-input models** using both **image** and **tabular** data.

It:

* Supports batch-wise data generation
* Scales tabular features
* Applies optional image augmentation
* Works seamlessly with Keras model training

***

### Constructor

```python
MultiModalDataGenerator(
    dataset,
    batch_size=32,
    image_size=(224, 224),
    shuffle=True,
    augment=False,
    tabular_features=None,
    num_classes=None
)
```

#### Parameters

```
|Name	| Type	| Description |
|-------|-------|-------------|
|dataset	| list[dict]	|List of samples, each with 'image_path', 'features', 'label'|
|batch_size	|int	|Batch size for training|
|image_size	|tuple	|Target image resolution (width, height)|
|shuffle	|bool	|Shuffle dataset at end of each epoch|
|augment	|bool	|Apply image augmentations if `True`|
|tabular_features	|list[str]	|List of tabular features to extract|
|num_classes	|int	|Number of output classes (for one-hot encoding); optional|
```

#### Key Methods:

`__len__()` : Returns number of batches per epoch

`__getitem__(idx)`: Returns a batch of image and tabular data with labels.&#x20;

`on_epoch_end()` :Shuffles the dataset after each epoch if `shuffle=True`.

`init_scalers()` :Initializes MinMaxScaler for tabular data and fits on the full dataset.

`__data_generation(batch_samples)`  :Internal method to:

* Load and preprocess image
* Scale tabular data
* Return formatted input-output pairs

#### Example Usage:

```
from custom_data_generator import MultiModalDataGenerator
from data_manager import NHANESImageMapper

# Prepare dataset
mapper = NHANESImageMapper("dataset/NHANES", "dataset/Image data")
paired_data = mapper.create_paired_dataset()

# Instantiate generator
generator = MultiModalDataGenerator(
    dataset=paired_data["train"],
    batch_size=16,
    augment=True,
    tabular_features=["age", "bmi", "calcium", "vitamin_d"],
    num_classes=3
)

# Fetch a batch
(images, tabular_inputs), labels = generator[0]
```

#### Output Format

Each Batch returns:

```
([image_batch, tabular_batch], label_batch)
Compatible with Keras models that use multiple inputs.

```

#### Notes

* Tabular features must be numerical and normalized (handled internally)
* Label encoding is one-hot by default (if `num_classes` is specified)
* Images are resized using PIL and normalized to `[0, 1]` float32 tensors
