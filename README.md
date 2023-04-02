# Industrial Meter Reading

![image](https://user-images.githubusercontent.com/71766106/229355994-63833df4-158f-4442-a599-93bbcccf3236.png)

* First, I trained YOLOv8 exclusively for meter detection with help of PyTorch and [ultralystics](https://github.com/ultralytics/ultralytics), see [here](detector.ipynb)
* Then I also train U-NET with Resnet50 backbone for cropped image segmentation to obtain mask, [here](segmentor.ipynb). For this, I used TensorFlow’s Keras and [SegmentationModels](https://github.com/qubvel/segmentation_models) library which have some pre-defined DL architectures for segmentation tasks.
* Then with help of functions defined in the 203-meter-reader notebook, I obtained the readings from masks, see [meter-reader](meter_reader.ipynb) notebook.

![Pipeline](https://user-images.githubusercontent.com/71766106/229354739-a653e7ee-8e5c-4d51-8180-d2d05255ce34.png)
