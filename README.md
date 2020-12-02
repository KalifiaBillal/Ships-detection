## About
In 2020, it was estimated that 979 #migrants died while crossings the #Mediterranean Sea. In 2019, the number of deaths amounted to 1.9 thousand. However, the accurate number of deaths recorded in the Mediterranean Sea cannot ascertained. Between 2014 and 2018, for instance, about 12 thousand people who #drowned were never found.

## Setup
Python 3.5+ is required for compatability with all required modules

```bash
# Install required modules
pip install -r requirements.txt
```

## Model
A convolutional neural network (CNN) is defined within the `model.py` module using the [TFLearn](http://tflearn.org/) library. This model supports the 80x80x3 input dimensions of the ShipsNet image data.

## Training
The defined CNN can be trained with the JSON version of the ShipsNet dataset and saved to a Tensorflow .tfl file for later use. Train the model by running `train.py` and passing the path to `shipsnet.json` and the path to the output .tfl file as arguments.

```bash
# Train the model
mkdir models
python train.py "shipsnet.json" "models/model.tfl"
```

The latest version of `shipsnet.json` is available through the [ShipsNet](https://www.kaggle.com/rhammell/ships-in-satellite-imagery) Kaggle page, which has further information describing the dataset layout. 

## Detector
A trained model can be applied across entire images using the sliding window detector function `detector.py`, which takes the model file path, input image path, and optional output image path as arguments. The output image will cluster positive detections and draw a bounding box around their center point. 

Example images are contained in the `scenes` directory. 
```bash
# Run on demo image with default output path
python detector.py "models/model.tfl" "scenes/scene_9.png"

# Run on demo image with defined output path
python detector.py "models/model.tfl" "scenes/scene_1.png" "scenes/scene_1_detections.png"
```
