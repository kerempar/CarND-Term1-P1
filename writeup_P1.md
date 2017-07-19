# **Finding Lane Lines on the Road** 

## Kerem Par
<kerempar@gmail.com>


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report 


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg_1_original.jpg =400x225 "Original"

[image2]: ./test_images_output/solidWhiteRight.jpg_2_grayscale.jpg =400x225 "Grayscale"

[image3]: ./test_images_output/solidWhiteRight.jpg_3_blurred.jpg =400x225 "Blurred"

[image4]: ./test_images_output/solidWhiteRight.jpg_4_edges.jpg =400x225 "Edges"

[image5]: ./test_images_output/solidWhiteRight.jpg_5_roi_edges.jpg =400x225 "Regipn of Interest Edges"

[image6]: ./test_images_output/solidWhiteRight.jpg_6_lines.jpg =400x225 "Lines"

[image7]: ./test_images_output/solidWhiteRight.jpg_7_combined.jpg =400x225 "Combined"

[image8]: ./test_images_output/solidYellowCurve2.jpg_1_original.jpg =400x225 "Original"

[image9]: ./test_images_output/solidYellowCurve2.jpg_2_grayscale.jpg =400x225 "Grayscale"

[image10]: ./test_images_output/solidYellowCurve2.jpg_3_blurred.jpg =400x225 "Blurred"

[image11]: ./test_images_output/solidYellowCurve2.jpg_4_edges.jpg =400x225 "Edges"

[image12]: ./test_images_output/solidYellowCurve2.jpg_5_roi_edges.jpg =400x225 "Regipn of Interest Edges"

[image13]: ./test_images_output/solidYellowCurve2.jpg_6_lines.jpg =400x225 "Lines"

[image14]: ./test_images_output/solidYellowCurve2.jpg_7_combined.jpg =400x225 "Combined"

[image15]: ./test_images_output/challenge_frame_0.jpg_1_original.jpg =400x225 "Original"

[image16]: ./test_images_output/challenge_frame_0.jpg_2_grayscale.jpg =400x225 "Grayscale"

[image17]: ./test_images_output/challenge_frame_0.jpg_3_blurred.jpg =400x225 "Blurred"

[image18]: ./test_images_output/challenge_frame_0.jpg_4_edges.jpg =400x225 "Edges"

[image19]: ./test_images_output/challenge_frame_0.jpg_5_roi_edges.jpg =400x225 "Regipn of Interest Edges"

[image20]: ./test_images_output/challenge_frame_0.jpg_6_lines.jpg =400x225 "Lines"

[image21]: ./test_images_output/challenge_frame_0.jpg_7_combined.jpg =400x225 "Combined"



---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 7 steps. First, I converted the images to grayscale, then I blurred the image by applying Gaussian Smoothing (with Kernel Size = 5), then I performed Canny Edge Detection (with low threshold = 50 and high threshold = 150), then I applied a Region of Interest filter to filter out unrelated edges, then I used Hough Transformation to detect the line segments belonging to lane lines (with rho=2, theta=1, threashold=15, min line length=40, and max line gap=20), then I converted line segments to single lines for the left and right lanes and finally I applied the lines to the original image.  

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the slopes of each line segment, separating the line segments into two groups, left and right, then iterating over line segments in each group to find the minimum and maximum bounds for the coordinates of each group, forming a single line for each group by using these coordinates, then extending these lines by calculating the coordinates of the intersection points of these single lines with the boundaries (edges) of region of interest (i.e. top and bottom boundaries) 

The pipeline was tested on all test images and videos.
The following three sequences of images (i.e. processing of SolidWhiteRight.jpg, SolidYellowCurve2.jpg, and the first frame of challenge.mp4 video) show how the pipeline works: 

####SolidWhiteRight.jpg

0.Original image

![alt text][image1]

1.Grayscaled image 

![alt text][image2]

2.Blurred image after appyling Gaussian Smoothing 

![alt text][image3]

3.Edges after appyling Canny Edge Detection

![alt text][image4]

4.Edges after appyling Region of Interest filter

![alt text][image5]

5.Lines extrapolated to the bounds of region of interest

![alt text][image6]

6.Lines drawn onto the original image

![alt text][image7]

####SolidYellowCurve2.jpg

0.Original image 

![alt text][image8]

1.Grayscaled image 

![alt text][image9]

2.Blurred image after appyling Gaussian Smoothing 

![alt text][image10]

3.Edges after appyling Canny Edge Detection

![alt text][image11]

4.Edges after appyling Region of Interest filter

![alt text][image12]

5.Lines extrapolated to the bounds of region of interest

![alt text][image13]

6.Lines drawn onto the original image

![alt text][image14]

####Challenge.mp4

0.Original image 

![alt text][image15]

1.Grayscaled image 

![alt text][image16]

2.Blurred image after appyling Gaussian Smoothing 

![alt text][image17]

3.Edges after appyling Canny Edge Detection

![alt text][image18]

4.Edges after appyling Region of Interest filter

![alt text][image19]

5.Lines extrapolated to the bounds of region of interest

![alt text][image20]

6.Lines drawn onto the original image

![alt text][image21]


### 2. Identify potential shortcomings with your current pipeline

This pipeline assumes straigt roads and detect straight lines, a potential shortcoming would be what would happen when driving on curved roads or road segments.

Other shortcoming could be the sensitivity to several aspects such as camera position in the car, frame size, region of interest selection, parameters, thresholds, etc. selected for edge detection, hough transform, etc. might not work sufficiently good for all kinds of images/videos with different road shapes, colors, camera position, etc.

For instance, although several improvements were made in the pipeline to make it adaptable to various frame sizes, and region of interest, some issues can still be seen when it is tried with challange.mp4.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use curve fitting to the line segments (or to the points) to be able to handle also the curved roads.

Another potential improvement could be to dynamically choose parameters/thresholds of the algorithms ()e.g. edge detection) to make the pipeline more adaptive to various lighting conditions by calculating a color histogram of the image. 

