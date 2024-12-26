# Electron Microscopy Particle Segmentation

- **Dataset**: [Electron Microscopy Particle Segmentation]().
- **Dataset License**: CC BY 4.0
- **Task**: Semantic Segmentation
- **Metrics**: IOU

## Data Processing

- Download and extract the dataset from [datasetninja.com](datasetninja.com)
- Convert to AnyLabeling format. Each valid train/val/test folder should contain images with coresponding json annotations. An image and its corresponding json annotation file share the same name. See the below example for the structure of the a json annotation file.
```json
{
  "version": "4.2.10",
  "flags": {},
  "shapes": [
    {
      "label": "cat",
      "points": [
        [100, 100],
        [150, 100],
        [150, 150],
        [100, 150]
      ],
      "group_id": null,
      "shape_type": "polygon",
      "flags": {}
    },
    {
      "label": "dog",
      "points": [
        [200, 200],
        [300, 200],
        [300, 300],
        [200, 300]
      ],
      "group_id": null,
      "shape_type": "polygon",
      "flags": {}
    }
  ],
  "imagePath": "example.jpg",
  "imageData": null,
  "imageHeight": 400,
  "imageWidth": 400
}
``` 


