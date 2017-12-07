# 360-degree video coding and the related projection method

## 1. Brief introduction about video coding

The task of coding is to convert any information to binary form. The key point of coding is to find a way to compress the information. Because the binary data is often transmitted through network. If the size of information is compressed to a lower size, the load of our network will be reduced.

To encode some information like text, we can use Huffman encoding method or some other kind of method to covert these kind of information to binary stream.  
![](/assets/video_compression.PNG)

As shown in the figure, when encoding the image, we can consider the spacial redundancy of the image. So DCT-based coding can be used to compress the image data.

While for video which is composed by a set of image frames, between two neighbor images, they must be similar due to the continuity of our real world. There is a temporal redundancy.

![](/assets/video_compression_process.PNG)

This figure shows the next frame \(one image in video\) can be predicted by the present frame using the motion vector. There are many methods to calculate such motion vector, we are not going to expand in details. In a word, all sort of redundant information can be compressed. And for different types of information, we will come up with a rule to encode it. We will follow all of these standards to do encoding and decoding.   
The standards may be updated if there is a new method which has a better performance.

In this article, we will mainly introduce the coding of 360-degree video. Until now, there is still no commonly accepted standard for this coding. Let's first look at what is 360-degree video.

## 2. Introduction to 360-degree video

Unlike other kind of videos, the 360-degree video is taken by several cameras at the same time. For example, 'Instra360 Air' is a special designed camera for Android users.

![](/assets/Instra360AirCamera.jpg)

This camera has two camera lens, for each lens it has 210 degree viewing angle. So when we combine the information that the two lens get, we can obtain a 360-degree information around the camera.

The way to do jointing should also be concerned carefully. Because the images taken by different lens will contain some overlapped region. Here are many tricks and algorithms for doing this which we may not discuss here. Suppose the image data has constructed to a sphere. We can use spherical coordinates to describe the position of each pixels. They are not in one plane, thus we need to do projection to a plane.

## 3. Projection methods

The team JEVT\(Joint Video Exploration Team on Future Video coding, [https://jvet.hhi.fraunhofer.de/](https://jvet.hhi.fraunhofer.de/)  
\) is working on the coding methods. They has design a library called '360Lib'. Here I list a table to show the projection formats that is supported in 360Lib:

| Index | Projection format | Abbreviation form |
| --- | --- | --- |
| 0 | Equirectangular | ERP |
| 1 | Cubemap | CMP |
| 2 | Euqal-area | EAP |
| 3 | Octahedron | OHP |
| 4 | Viewport generation using rectilinear projection | - |
| 5 | Icosahedron | ISP |
| 6 | Craster Parabolic Projection for CPP-PSNR calculation | - |
| 7 | Truncated Square Pyramid | TSP |
| 8 | Segmented Sphere Projection | SSP |
| 9 | Adjusted Cubemap Projection | ACP |
| 10 | Rotated Sphere Projection | RSP |

Here we mainly introduce the first two projection methods which are Equirectangular projection and Cubemap\(Cube projection\).   
Consider there is a sphere with the spherical coordinate $$(r, \theta, \phi)$$. The radius of sphere is irrelevant of our problem. $$\theta$$ and $$\phi$$ can describe a position. For each position, there is a pixel there. The projection is to find a transform of $$(\theta, \phi)$$ to the plane coordinate $$(x, y)$$.  
![](/assets/640px-3D_Spherical.svg.png)  
\(image from wiki\)

### a. Equirectangular projection

Equirectangular projection\(ERP\) is the most simple method.

I may first show the transform equation:


$$
x=(\theta-\theta_0)cos\phi_0
$$



$$
y=\phi-\phi_0
$$


$$(\theta_0, \phi_0)$$ is the original point that we choose.

### b. Cube projection

[https://docs.unity3d.com/Manual/class-Cubemap.html](https://docs.unity3d.com/Manual/class-Cubemap.html)

## References

Polytechnique university EIE546 course website: [http://www.eie.polyu.edu.hk/~ylchan/teaching/EIE546VT/EIE546ylchan2017.htm](http://www.eie.polyu.edu.hk/~ylchan/teaching/EIE546VT/EIE546ylchan2017.htm)

