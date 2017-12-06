# 360-degree video coding and the related projection method

## 1. Brief introduction about video coding

The task of coding is to convert any information to binary form. The key point of coding is to find a way to compress the information. Because the binary data is often transmitted through network. If the size of information is compressed to a lower size, the load of our network will be reduced.

To encode some information like text, we can use Huffman encoding method or some other kind of method to covert these kind of information to binary stream.
![](/assets/video_compression.PNG)

As shown in the figure, when encoding the image, we can consider the spacial redundancy of the image. So DCT-based coding can be used to compress the image data. 

While for video which is composed by a set of image frames, between two neighbor images, they must be similar due to the continuity of our real world. There is a temporal redundancy. 

![](/assets/video_compression_process.PNG)

This figure shows the next frame (one image in video) can be predicted by the present frame using the motion vector. There are many methods to calculate such motion vector, we are not going to expand in details. In a word, all sort of redundant information can be compressed. And for different types of information, we will come up with a rule to encode it. We will follow all of these standards to do encoding and decoding. 
The standards may be updated if there is a new method which has a better performance. 

In this article, we will mainly introduce the coding of 360-degree video. Until now, there is still no commonly accepted standard for this coding. Let's first look at what is 360-degree video.




## 2. Introduction to 360-degree video

Unlike other kind of videos, the 360-degree video is taken by several cameras at the same time. For example, 'Instra360 Air' is a special designed camera for Android users. 

![](/assets/Instra360AirCamera.jpg)

This camera has two camera lens, for each lens it has 210 degree viewing angle. So when we combine the information that the two lens get, we can obtain a 360-degree information around the camera.

The way to do jointing should also be concerned carefully. 
## 3. Projection methods

### a. Equirectangular projection


### b. Cube projection


### c. other projection methods