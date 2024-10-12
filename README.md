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

  ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-12%20022432.png)

  In general, the performance would improve if we increase the network width that is adding more filters and larger filter size could grasp richer structural information, which in turn lead to better results. Deeper 
  networks do not always result in better performance.

  Our first layer consists of 64 filters of size 9 * 9 * 3 as we are dealing with RGB image.

  Second layer consists of 32 filters of size 1 * 1 * 64.

  Third layer consists of 3 filters of size 5 * 5 * 32.

- ### Loss Calculation:-
  Here we are using both *'MSE Loss'* and *'Perceptual Loss'*.

  For super resolution , model trained with a peceptual loss is able to better reconstruct fine details compared to methods trained with per pixel loss.

  Perceptual loss is a type of loss function that aims to capture the perceptual differences between images , rather than just pixel wise differences. Perceptual differences refer to how humans visually perceive distinctions between images rather than just mathematical difference in pixel values. Twoo images can mathematically different but look very similar to humans or vice versa.

  So, perceptual loss function aims to capture these differences by using features from pre trained network. Here we are using *'VGG-16 pre trained network'*.
  
  > - The target HR image and generated HR image are passed through pre trained network.
  > - The network processes both images , producing feature maps at various layers.
  > - For each selected layer , the feature maps of generated image and target image are compared. The compariosn is usually done by MSE between feature maps.
  > - The losses from multiple layers are often combined. Earlier layer captures low level features and deeper layers capture high level semantic information.
  > - The perceptual loss is often combined with pixel wise MSE loss for final optimization objective.

  ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-12%20030818.png)
  
  ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-12%20031822.png)

- ### Training:-
  - Epochs = 20
  - Batch size = 1
  - Optimizer = Adam
  - Learning rate = 0.001
    
    ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-13%20021455.png)
  
    ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-13%20021521.png)

- ### Results:-
  - Training Set Result:-
    
    ![](https://github.com/Srishti002/SRCNN/blob/main/train_0_label.png)
    ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-12%20230358.png)

    ![](https://github.com/Srishti002/SRCNN/blob/main/train_1_label.png)
    ![](https://github.com/Srishti002/SRCNN/blob/main/Screenshot%202024-10-13%20002905.png)
   

  

  
  


  
  
  
  


