# Image-Regidtration

Image registration is a digital image processing technique that helps us to align different images of the same scene.





### Generated SLAM Maps
Estimating the quality of a SLAM algorithm means estimating the accuracy of its results, which can be determined by the map of the mobile platform created while driving. 

![Gmapping SLAM Map](https://github.com/Dhaour9x/Image-Regidtration/blob/master/images/GroundTruth.jpg)
![Gmapping SLAM Map](https://github.com/Dhaour9x/Image-Regidtration/blob/master/images/gmappingSLAM.jpg)
![Hector SLAM Map](https://github.com/Dhaour9x/Image-Regidtration/blob/master/images/hectorSLAM.jpg)

Since the SLAM resulting image for the map does not always have the correct dimensions
(approximately the same as the Ground Truth Map), the dimensions of the generated SLAM maps must be corrected approximately to the dimensions of the Ground Truth Map by image registration with OpenCV.
We also have to convert from  .pgm to .png or .jpg. 


Now we want to align a certain image to the same angle as a ground truth image. In the images above, the first image can be considered a "reference image", while Gmapping and Hector SLAM images are not well suited for comparison. The image registration algorithm helps us to align images of Gmapping and Hector SLAM in the same plane as the ground truth image.

### The Results after Registration
![GmappingSLAMMap](https://github.com/Dhaour9x/Image-Regidtration/blob/master/images/gmapping_registred.png)| ![GmappingSLAMMap](https://github.com/Dhaour9x/Image-Regidtration/blob/master/images/hector_registred.png)

 ## The image registration algorithm works as follows:
* Both images are converted to grayscale.
* Adjust features from the image to be aligned to the reference image and save the coordinates of the corresponding keypoints. Keypoints are simply the selected few points used to calculate the transformation (generally points that stand out), and descriptors are histograms of image gradients to characterize the appearance of a keypoint. In this algorithm we use the ORB (Oriented FAST and Rotated BRIEF) implementation in the OpenCV library, which provides us with both the keypoints and the associated descriptors
* Wählen Sie die besten Übereinstimmungen aus, und entfernen Sie die verrauschten Übereinstimmungen.
* Finden Sie die Homomorphie-Transformation.
* Wenden Sie diese Transformation auf das ursprüngliche, nicht ausgerichtete Bild an, um das Ausgabebild zu erhalten.

### Installation:
```
git clone https://github.com/Dhaour9x/Image-Regidtration.git
cd Image-Registration
python imRegistration.py
```

### Usage:
```
python imRegister.py --first images/original_01.png --second images/modified_01.png
```
@author Riadh Dhaoui
