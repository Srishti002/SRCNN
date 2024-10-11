# SRCNN
## Project Description
This project is about implementing SRCNN(Super Resolution Convolutional Neural Network) on low resolution images to obtain high resolution images. There are four different approaches to super resolution in general. These are:-
> 1. Patch based ( or example based):- This method work by using a database of low and high-resolution image patches to learn the mapping between them.
> 2. Edge based:- These focus on preserving and enhancing edge information in the image during the super-resolution process.
> 3. Image statistical methods:- These methods use statistical properties of images to guide the super-resolution process.
> 4. Prediction models:- This includes CNNs based methods like SRCNN.

So, in this project we are implementing **prediction models methods like SRCNN** for transforming low resolution image into high resolution image.

## SRCNN Architecture
![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-11%20194250.png)

- ### Preprocessing:-
  The only preprocessing we do here is bicubic interpolation on LR images to make it to the desired size.
  
- ### Patch extraction:-
  Here patch extraction is equivalent to convolving a image by the set of filters.
  
  F1(Y) = max (0, W1 ∗ Y + B1)
  
  W1= filter
  
  B1=bias

  '*' denotes convolution operation

  n1 filters of c * f1 * f1 

- ### Non Linear Mapping:-
  This operation non linearly maps each high dimensional vector onto another high dimensional vector.

  F2(Y) = max (0, W2 ∗ F1(Y) + B2)

  W2 contains n2 filters of size n1 × f2 × f2

- ### Reconstruction:-
  We define a convolutional layer to produce the final high-resolution image:-
    
  F(Y) = W3 ∗ F2(Y) + B3

  W3 corresponds to c filters of a size n2 × f3 × f3

## Step by Step Guide:-
- ### Dataloading:-
  We use *'BSD100'* dataset for this project. *'image_SRF_2'* as training set , *'image_SRF_3'* as validation set and *'image_SRF_4'* as testing set .

  While loading data we have to convert the LR images and their respective labels to Tensor form for further processing.

  And also resize both labels and LR images to 3 * 224 * 224 as later we are using VGG-16 model for better performance and we know that VGG-16 accepts images of spatial dimension of 224 * 224 .

  ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-12%20021610.png)


  Normalize both LR images and labels.

  ![](https://github.com/user-attachments/assets/5f7ad203-2795-4e13-ade1-27cc721918dc)

- ### SRCNN Model:-
  


  
  
  
  


