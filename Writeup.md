*Finding Lane Lines on the Road*

Goals of this project are the following:
	Make a pipeline that finds the lane lines of the road
	Reflect on my work

My pipeline had several stages. First, it grayscaled the current image or frame. Then, it smoothed the image  using a gaussian blur function. This allowed it to avoid picking up every single edge with the edge detector. Then, I used the canny function to detect edges. 

Once  I had the edges, I observed the edges found within a pre-determined window of my image. In this case, that window was the lower bottom triangle of the image composed of the bottom two corners and the center of the image. Within this region, I ran my hough_lines function to find lines greater than 30 pixels long and with some gaps. To clean my output, I only labeled one line per lane side. I did so by picking the highest and lowest pixels corresponding with each side of the lane. I distinguished each side by the sign of the slope of the lines that traced out the lane sides. 

Finally, after choosing my two lines, I overlaid them onto the original image. I then ran this over every frame of the videos.

There are a few potential shortcomings of the algorithm. One, the algorithm has a constant region of searching for lane lines. This means that it can only be used in center placed cameras, which is an obvious failure  in design. One solution could be to detect the road with a black color filter and then focus on the given region. Another could be do manually program a separate region for every camera on the car. A second shortcoming of the algorithm is that it can only detect one lane on each side of the image (one with a positive slope, one with a negative slope). A solution could be to differentiate lines by a minimum difference in slope rather than the sign of the slope. A third shortcoming of the algorithm is that it does not use any memory from one frame to the next. I would recommend creating a bias in which the algorithm assumes that the lanes will be found close to the position of the lanes from the previous frame.


