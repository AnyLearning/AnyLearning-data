# ZhangLabData: Chest X-Ray - Dataset Ninja

## Introduction
Released on June 2, 2018, by Daniel Kermany, Kang Zhang, and Michael Goldbaum, the **Chest X-Ray** subset of the **ZhangLabData** contains 5,856 images categorized into **PNEUMONIA_BACTERIA**, **PNEUMONIA_VIRUS**, and **NORMAL** classes. This dataset was created to enhance the diagnostic capabilities of deep learning models, particularly for identifying pediatric pneumonia, a leading cause of childhood mortality.

The dataset leverages transfer learning techniques and highlights areas identified by the neural network to improve interpretability.

[Research Paper](https://www.cell.com/cell/fulltext/S0092-8674(18)30154-5)

## Summary
### The full dataset
- **Size**: 5,856 images
- **Splits**: Train (5232), Test (624)
- **Classes**: 
  - **PNEUMONIA_BACTERIA**: 2,780
  - **PNEUMONIA_VIRUS**: 1,493
  - **NORMAL**: 1,583
    
*Note: The train.zip and test.zip file provided in this repository contain only a sample of the full dataset, consisting of 139 training images and 42 testing images. These images are already formatted for direct upload and use in the Anylearning app. For access to the full dataset, please refer to the download section.*

## License
The dataset is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0).

## Citation
If using the dataset, please cite:
```
Kermany, Daniel; Zhang, Kang; Goldbaum, Michael (2018), 
“Large Dataset of Labeled Optical Coherence Tomography (OCT) and Chest X-Ray Images”, 
Mendeley Data, V3, doi: 10.17632/rscbjbr9sj.3
```

## Download
Download the full dataset from [ZhangLabData: Chest X-ray Dataset](https://datasetninja.com/zhang-lab-data-chest-xray#introduction)

## Convert to AnyLearning format
If you download the **full dataset** from the link in the **Download** section, you will need to convert it into a specific format compatible with AnyLearning. The dataset should be organized into 3 subfolders, each corresponding to one of the 3 classes. You can use the following code to perform the conversion:
```python
import os
import shutil
import json

def create_class_folders(base_path, classes):
    for cls in classes:
        class_path = os.path.join(base_path, cls)
        if not os.path.exists(class_path):
            os.makedirs(class_path)

def move_images_to_class_folders(base_path, target_path):
    img_path = os.path.join(base_path, 'img')
    ann_path = os.path.join(base_path, 'ann')
    
    for ann_file in os.listdir(ann_path):
        if ann_file.endswith('.json'):
            with open(os.path.join(ann_path, ann_file), 'r') as f:
                data = json.load(f)
            
            class_name = data['tags'][0]['name']
            image_file = ann_file.replace('.json', '')
            image_path = os.path.join(img_path, image_file)
            class_folder = os.path.join(target_path, class_name)
            
            if not os.path.exists(class_folder):
                os.makedirs(class_folder)
            
            shutil.copy(image_path, class_folder)

def main():
    train_path = '/path/to/train' # replace with your folder path
    test_path = '/test/to/test' # replace with your folder path

    out_train_path = 'formatted_train'
    out_test_path = 'formatted_test'
    
    # Collect all classes from train and test annotation files
    classes = set()
    for base_path in [train_path, test_path]:
        ann_path = os.path.join(base_path, 'ann')
        for ann_file in os.listdir(ann_path):
            if ann_file.endswith('.json'):
                with open(os.path.join(ann_path, ann_file), 'r') as f:
                    data = json.load(f)
                classes.add(data['tags'][0]['name'])
            break
        
    
    create_class_folders(out_train_path, classes)
    create_class_folders(out_test_path, classes)
    
    move_images_to_class_folders(train_path, out_train_path)
    move_images_to_class_folders(test_path, out_test_path)

if __name__ == "__main__":
    main()
```



