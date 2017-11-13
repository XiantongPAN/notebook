# 360-degree video coding and the related projection method

## brief introduction about video coding


To encode some information like text, we can use Huffman encoding method or some other kind of method to covert these kind of information to binary stream.
![](/assets/video_compression.PNG)

As shown in the figure, when encoding the image, we can consider the spacial redundancy of the image. So DCT-based coding can be used to compress the image data. 

While for video which is composed by a set of image frames, there is a temporal redundancy. 

![](/assets/video_compression_process.PNG)