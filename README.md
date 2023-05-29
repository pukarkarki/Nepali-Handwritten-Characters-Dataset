# About dataset
<div style="text-align: justify">
The dataset comprises of grayscale images of 11,600 handwritten nepali characters. The characters are consonants, numerals and vowels.
</div>

* consonants = "क ख ग घ ङ च छ ज झ ञ ट ठ ड ढ ण त थ द ध न प फ ब भ म य र ल व श ष स ह क्ष त्र ज्ञ"
* numerals = "० १ २ ३ ४ ५ ६ ७ ८ ९"
* vowels = "अ आ इ ई उ ऊ ए ऐ ओ औ अं अः"

<div style="text-align: justify">
The dataset comprises of 58 classes( 36 consonants + 10 numerals + 12 vowels). Each class consists of 200 images splitted into training set comprising of 160 images and test set comprising of 40 images.
</div>

## About data collection
The dataset was created by modifying the amazing [Devanagari Character Dataset](https://www.kaggle.com/datasets/ashokpant/devanagari-character-dataset). The purpose of the modification was to structure the dataset in a standard computer vision dataset. This also resulted in the dataset being easy to load using [PyTorch's torchvision.datasets.ImageFolder](https://pytorch.org/vision/stable/generated/torchvision.datasets.ImageFolder.html).

## Description of dataset
The dataset is structured as shown below
```
data/ <- overall dataset folder
    train/ <- training images
        ०/ <- class name as folder name
            0.jpg
            5.jpg
            ...
        १/
            1.jpg
            2.jpg
            ...
    test/ <- testing images
        ०/ <- class name as folder name
            1.jpg
            2.jpg
            ...
        १/
            0.jpg
            3.jpg
            ...
```
The images are grayscale with the resolution of 28x28 and are in JPG format.

## Using the dataset
#### Walk through the dataset
You can use the following function to walk through the dataset.
```
import os
def walk_through_dir(dir_path):
  """
  Walks through dir_path returning its contents.
  Args:
    dir_path (str or pathlib.Path): target directory
  
  Returns:
    A print out of:
      number of subdiretories in dir_path
      number of images (files) in each subdirectory
      name of each subdirectory
  """
  for dirpath, dirnames, filenames in os.walk(dir_path):
    print(f"There are {len(dirnames)} directories and {len(filenames)} images in '{dirpath}'.")
```
#### Load the dataset
```
from pathlib import Path
image_path = Path("data/")
# Setup train and testing paths
train_dir = image_path / "train"
test_dir = image_path / "test"

# Use ImageFolder to create dataset(s)
from torchvision import datasets
train_data = datasets.ImageFolder(root=train_dir, # target folder of images
                                  transform=None, # transforms to perform on data (images)
                                  target_transform=None) # transforms to perform on labels (if necessary)
test_data = datasets.ImageFolder(root=test_dir, 
                                 transform=test_transforms)
```
### Get class names
```
# Get class names as a list
class_names = train_data.classes

# Can also get class names as a dict
class_dict = train_data.class_to_idx
```

## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/pukarkarki/Nepali-Handwritten-Characters/blob/main/LICENSE) file for details.

