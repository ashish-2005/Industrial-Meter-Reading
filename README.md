# Industrial Meter Reading

![image](https://user-images.githubusercontent.com/71766106/229355994-63833df4-158f-4442-a599-93bbcccf3236.png)

* First, I trained YOLOv8 exclusively for meter detection with help of PyTorch and [ultralystics](https://github.com/ultralytics/ultralytics), see [here](detector.ipynb)
* Then I also train U-NET with Resnet50 backbone for cropped image segmentation to obtain mask, [here](segmentor.ipynb). For this, I used TensorFlow’s Keras and [SegmentationModels](https://github.com/qubvel/segmentation_models) library which have some pre-defined DL architectures for segmentation tasks.
* Then with help of functions defined in the 203-meter-reader notebook, I obtained the readings from masks, see [meter-reader](meter_reader.ipynb) notebook.

![Pipeline](https://user-images.githubusercontent.com/71766106/229354739-a653e7ee-8e5c-4d51-8180-d2d05255ce34.png)

## Video inference

![vid](https://user-images.githubusercontent.com/71766106/229518897-0e01e44d-b2a0-40f1-a823-c11a6b0afb8c.gif)

*(Readings are a bit inaccurate becuase model is trained on meter with MPa unit and inerval 25/50 | 1.6/32 and i was unable to find video of working meter with these specification, this can easily be cured by introducing more diverse meters for training)*

## OpenVINO compatibility test

To test compatibilty of model with OpenVINO, I ran benchmark test on both models.

![Detector](https://user-images.githubusercontent.com/71766106/229520580-2fab5dea-8d3b-4591-91ad-93069da63c82.png)
(Detector Benchmarks)

![segmentor](https://user-images.githubusercontent.com/71766106/229517544-093b978b-bfa6-4db3-a3a2-85fd75ad9c90.png)
(Segmentor Benchmarks)

#### Optimization
* For now, segmentor is backed with Resnet50 which makes it unnecessarily powerful but slow. I am planning to try differnt backbone artitechtures like VGG16/19, Resnet18/34 to make it faster. 
* Since, we now have the openvino-IR of both models we can do some optimization like post-training int8 quantization with openvino-nncf to increase the inference speed. Hence making it a more scalable solution.

