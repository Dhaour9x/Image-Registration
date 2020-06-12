# Image-Regidtration
Since the SLAM resulting image for the map doesn’t always have the correct dimensions
(approximately the same as the ground truth map), we have to correct the dimensions of the generated SLAM maps approximatly to the dimension of the ground truth map using image registration using OpenCV.
 We also want to convert from .pgm  to .png that the algorithm expects. 

Image registration is a digital image processing technique which helps us align different images of the same scene. For instance, one may click the picture of a book from various angles. Below are a few instances that show the diversity of camera angle.

Now, we may want to “align” a particular image to the same angle as a reference image. In the images above, one may consider the first image to be an “ideal” cover photo, while the second and third images do not serve well for book cover photo purposes. The image registration algorithm helps us align the second and third pictures to the same plane as the first one.

How does image registration work?
 The Image registration algorithm works as follows:

    Convert both images to grayscale.
    Match features from the image to be aligned, to the reference image and store the coordinates of the corresponding keypoints. Keypoints are simply the selected few points which are used to compute the transform (generally points that stand out), and descriptors are histograms of the image gradients to characterize the appearance of a keypoint. In this post, we use ORB (Oriented FAST and Rotated BRIEF) implementation in the OpenCV library, which provides us with both keypoints as well as their associated descriptors.
    Match the keypoints between the two images. In this post, we use BFMatcher, which is a brute force matcher. BFMatcher.match() retrieves the best match, while BFMatcher.knnMatch() retrieves top K matches, where K is specified by the user.
    Pick the top matches, and remove the noisy matches.
    Find the homomorphy transform.
    Apply this transform to the original unaligned image to get the output image.
