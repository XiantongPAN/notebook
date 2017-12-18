# 360-degree video coding and the related projection method

## 1. Brief introduction about video coding

The task of coding is to convert any kind of information to a binary form. The key point of coding is to find a way to compress the information. Because the binary data is often transmitted through network. If the size of information is compressed to a lower size, the load of network transmission will be reduced.

The image shows some common coding methods for Text, Image and Video compression: 

![](/assets/video_compression.PNG)

To encode some information like text, we can use Huffman encoding method or some other kinds of method to covert information to binary stream.

For image compression, there is a spatial redundancy of the image. It means our world is composed of continues matters, so that it will looks like very similar in two nearing area. A DCT-based coding can be used to compress the image data.

While for video which is composed by a set of image frames, between two neighbor images, they must be similar due to the time continuity of our real world. There is a temporal redundancy.


![](/assets/video_compression_process.PNG)

This figure shows the next frame (one image in video) can be predicted by the present frame using the motion vector. There are many methods to calculate such motion vector, we are not going to expand in detail. In a word, all sort of redundant information can be compressed. And for different types of information, we will come up with a rule to encode it. We will follow these standards to do encoding and decoding.   
The standards may be updated if there is a new method which has a better performance.


In this article, we will mainly introduce the coding methods of 360-degree video. Until now, there is still no commonly accepted standard for this kind of coding. Let's first look at what is 360-degree video.

## 2. Introduction to 360-degree video

Unlike other kind of videos, the 360-degree video is taken by several cameras at the same time. For example, 'Instra360 Air' is a special designed camera for Android users.

![](/assets/Instra360AirCamera.jpg)

This camera has two camera lenses, for each lens it has 210 degree viewing angle. When we combine the information that the two lenses get, we can obtain a 360-degree information around the camera.

The way to do jointing should also be concerned carefully. Because the images taken by different lenses will contain some overlapped region. Here are many tricks and algorithms for doing this which we may not discuss here. Suppose the image data has constructed to a sphere. We can use spherical coordinates to describe the position of each pixels. They are not in one plane. Thus, we need to do projection.


## 3. Projection methods

The team JEVT (Joint Video Exploration Team on Future Video coding, https://jvet.hhi.fraunhofer.de) has been working on the coding methods. They had design a library called '360Lib'. Here I list a table to show the projection formats that is supported in 360Lib:

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


Here we mainly introduce the first two projection methods which are Equirectangular projection and Cubemap (Cube projection).
  
  Consider there is a sphere with the spherical coordinate (r,θ,φ). The radius of sphere is irrelevant of our problem. θ and φ can describe a position. For each position, there is a pixel there. The projection is to find a transform of (θ,φ) to the plane coordinate (x,y).
  
  
![](/assets/640px-3D_Spherical.svg.png)  
\(image from wiki\)

### a. Equirectangular projection

Equirectangular projection(ERP) is the simplest method.

I may first show the transform equation:

{  x=φ  y=θ

This really shows nothing. Consider the range:

(0≤φ< 2π, 0≤θ≤π)

Hence x and y are also in this range, which means a 2π×π rectangle image is created. This is the so called ‘equal’ and ‘rectangular’ projection.

In another point of view, when you are familiar with the tellurion, and the longitude and latitude on it. We can regard this projection is worked on these lines. When projected the longitude and latitude onto a rectangular, the distance between two lines is not changed. This is what Wikipedia’s point of view (https://en.wikipedia.org/wiki/Equirectangular_projection). The formula in it is a little different of what I have shown as I had supposed that my original point is (0, 0).

In math, the Equirectangular projection is neither conformal mapping nor Equal-area projection. Lots of distortion will be caused.



### b. Cube projection

Some people familiar with the Unity3D may saw the word cubemap again and again. When there is a spherical object in the scene, and you want to draw some textures on it, which means you should apply an image to the sphere. However, the image is always rectangular. You should do a projection from plane to sphere. The most common method is cubemap (https://docs.unity3d.com/Manual/class-Cubemap.html). 
![](/assets/CubeLayout6Faces.png)

The texture is composed of 6 squares. It is an expand of cube. Each of the square is applied to one side of the sphere. Intuitively, this will perform better than the equirectangular method, the distortion will be less.

## References

The Hong Kong Polytechnic University EIE546 course website: (http://www.eie.polyu.edu.hk/~ylchan/teaching/EIE546VT/EIE546ylchan2017.htm)

