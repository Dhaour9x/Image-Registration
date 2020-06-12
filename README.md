# Image-Regidtration

Estimating the quality of a SLAM algorithm means estimating the accuracy of its results, which can be determined by the map and the trajectory of the mobile platform created while driving. The simplest way to compare the results of several algorithms on the same data sequence is to calculate any difference between the generated map and the ground truth map (i.e. the absolute map).\cite{DBLP:journals/corr/abs-1708-02354}


The framework that evaluates the maps is also presented in this section. The object of observation is a result map, and through its visual evaluation it is possible to find out which algorithm produces the best map, i.e. to determine which map contains the least amount of noise, the most accurate walls, the least amount of artifacts, etc. Some metrics of quantitative estimation are presented in this paper.

 The maps produced with each algorithm considered are compared using several metrics, and a score is given for each run. In this way it is possible to create a ranking of SLAM algorithms.


The metrics used to evaluate the quality of the maps produced by different SLAM algorithms are Hausdorff distance and SSMI index (eng. Structural Similarity Index). These metrics allow to measure the map quality based on a ground truth map and provide different criteria for map evaluation.



Since the SLAM resulting image for the map does not always have the correct dimensions
(approximately the same as the Ground Truth Map), the dimensions of the generated SLAM maps must be corrected approximately to the dimensions of the Ground Truth Map by image registration with OpenCV.
We also want to convert from automatically saved .pgm to .png, which the algorithm expects. 

Image registration is a digital image processing technique that helps us to align different images of the same scene.
Now we want to align a certain image to the same angle as a ground truth image. In the images above, the first image can be considered a "reference image", while images (d) and (e) are not well suited for comparison. The image registration algorithm helps us to align images (d) and (e) in the same plane as the ground truth image.


 ## The image registration algorithm works as follows:
* Both images are converted to grayscale.
* Adjust features from the image to be aligned to the reference image and save the coordinates of the corresponding keypoints. Keypoints are simply the selected few points used to calculate the transformation (generally points that stand out), and descriptors are histograms of image gradients to characterize the appearance of a keypoint. In this algorithm we use the ORB (Oriented FAST and Rotated BRIEF) implementation in the OpenCV library, which provides us with both the keypoints and the associated descriptors
* Wählen Sie die besten Übereinstimmungen aus, und entfernen Sie die verrauschten Übereinstimmungen.
* Finden Sie die Homomorphie-Transformation.
* Wenden Sie diese Transformation auf das ursprüngliche, nicht ausgerichtete Bild an, um das Ausgabebild zu erhalten.

