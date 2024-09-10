# Image-Cartoonifying-Road-Lane-Detection

## 1. Part I: Applying Image Processing Filters For Image Cartoonifying

In this part of the assignment we want to make the real-world images look like they are genuinely from a cartoon. The basic idea is to ll the at parts with some color and then draw thick lines on the strong edges. In other words, the at areas should become much more at and the edges should become much more distinct. We will detect edges and smooth the at areas, then draw enhanced edges back on top to produce a cartoon or comic book effect.
###  1.1 Generating a black-and-white sketch
  ● Applied CV2.cvtcolor to get a greyscale image since Laplacian filters use grayscale images.
  ● Smoothing image using median filter cv2.median blur of kernel size 9 for noise reduction because it is good at removing  noise while keeping edges sharp.
  ● After noise reduction, a Laplacian filter is used for edge detection using cv2.laplacian with kernel size 5.
  ● Applied cv2.threshold to get the binary threshold of image to make the edges either white or black.
![image](https://github.com/user-attachments/assets/a7a29ac3-0b4d-46be-8c94-0e5d6be17a34)

###  1.2 Generating a color painting and a cartoon
A strong bilateral filter smoothes at regions while keeping edges sharp, and is therefore great as an automatic cartoonifier or painting filter, except that it is extremely slow (that is, measured in seconds or even minutes rather than milliseconds!). 
Rather than applying a large bilateral filter, we apply many small bilateral filters to produce a strong cartoon effect in less time.
 ● Image is resized and then 160 repetitions were made with kernel size 9, sigma color 9, sigma space 9 then applied bilateral filter, then original size is restored.
 ● Applied cv2.bitwise_and to resized image to mask the edges from threshold image onto the cartoonized image.
 ![image](https://github.com/user-attachments/assets/634f0674-3041-479d-b9d5-ec3131b62f42)

## 2. PartII: Road Lane Detection Using Hough Transform
Detection of road lanes in an image using Hough Transform.
 ● Applied CV2.cvtcolor to get a grayscale image.
 ● Smoothing image using median filter cv2.median blur of kernel size 7.
 ● Edge detection using cv2.canny with threshold 1 = 80 and threshold 2 = 200.
 ● Defined square polygon was used to obtain the region of interest.
 ● Implemented Hough transform function .
   ○ Np.nonzero to get indices of edges.
   ○ Theta set at (0,angle sent).
   ○ Initiated an empty dictionary to store accumulator results.
   ○ Loop on each angle and check all edges.
   ○ For each edge loop to calculate ρ and check if the key exists in accumulator. Increment if exists or else create new key of value 1.
   ○ Check for items of dictionary greater than threshold
   ○ Return list of keys of items greater than threshold.
 ● Apply Hough and calculate position of points for each ρ & θ and draw the lines.
 ● Applied square polygon to cut lines in the region of interest and mask the lines on the original image using cv2.addWeighted.
 ![image](https://github.com/user-attachments/assets/cebc6828-b95e-4cba-bd43-70995e476076)
![image](https://github.com/user-attachments/assets/64e2d1a6-80a0-4315-b830-e9cb90907352)
