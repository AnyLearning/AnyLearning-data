# American Sign Language Letters Recognition

- **Dataset**: [American Sign Language Letters Recognition dataset](https://public.roboflow.com/object-detection/american-sign-language-letters/1).
- **Dataset License**: Public Domain.
- **Task**: Handpose Classification.

## Data Processing 
If you download the full dataset from the link in the Download section, you will need to convert it into a specific format compatible with AnyLearning. You can use the following code to perform the conversion:
```python
def convert(source_dir, target_dir):
   subsets = ["train", "valid", "test"]

   for subset in subsets:
      subset_dir = source_dir / subset
      labels = pd.read_csv(subset_dir / "_classes.csv")
      for _, row in labels.iterrows():
         image_name = row.iloc[0]
         class_name = row.iloc[1:].idxmax()

         src_dir = source_dir / subset / image_name
         dst_dir = target_dir / subset/ class_name 

         dst_dir.mkdir(parents=True, exist_ok=True)
         shutil.copy2(src_dir, dst_dir)
```