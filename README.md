# Computer-Vision


## [Harris Corner Detector](https://github.com/Venchi99/Computer-Vision/blob/main/Harris.ipynb)

Implemented Harris Corner Detector and tested this function on four test images. 
Compare the results with built-in function cv2.cornerHarris(), 
there are some factors that might affect the performance of Harris corner detection: 

1. My implementation use Prewitt filter to compute x and y derivatives of image, while the 
built-in function cv.cornerHarris() use Sobel filter to compute x and y derivatives of image. 
Prewitt filter is more crude compare to Sobel filter since it didn’t accentuate pixels that are 
closer to the center of the mask. However, accentuate pixels that are closer to the center also 
smoothing the image. The overall Measure of corner response (R) in my implementation are 
larger than built-in function (larger mean and standard deviation value), hence after 
performing non-maximum suppression and thresholding, my implementation finds less 
corners compare to built-in function.

2. The window function might be different, hence affect the performance. My implementation 
uses a gaussian filter with size 13 by 13 and sigma = 2 as the window function. For built-in 
function, I only find “The window function is either a rectangular window or a Gaussian 
window” on the OpenCV document page. Hence, the window function very likely to be 
different that affect the performance.

## [Deep Learning Classification](https://github.com/Venchi99/Computer-Vision/blob/main/DLClassificaition.ipynb)
Train a CNN with the Kuzushiji-MNIST dataset using the PyTorch deep
learning framework. 


Base model:

• 5×5 Convolutional Layer with 32 filters, stride 1 and padding 2. <br>
• ReLU Activation Layer. <br>
• 2×2 Max Pooling Layer with a stride of 2. <br>
• 3×3 Convolutional Layer with 64 filters, stride 1 and padding 1. <br>
• ReLU Activation Layer. <br>
• 2×2 Max Pooling Layer with a stride of 2. <br>
• Fully-connected layer with 1024 output units. <br>
• ReLU Activation Layer. <br>
• Fully-connected layer with 10 output units. <br>


Modified model: 

• 5×5 Convolutional Layer with 32 filters, stride 1 and padding 2. <br>
• 3×3 Convolutional Layer with 64 filters, stride 1 and padding 1. <br>
13 
• Batch Normalization 2d Layer. <br>
• ReLU Activation Layer. <br>
• 2×2 Max Pooling Layer with a stride of 2. <br>
• 3×3 Convolutional Layer with 128 filters, stride 1 and padding 1. <br>
• 3×3 Convolutional Layer with 128 filters, stride 1 and padding 1. <br>
• Batch Normalization 2d Layer. <br>
• ReLU Activation Layer. <br>
• 2×2 Max Pooling Layer with a stride of 2. <br>
• Fully-connected layer with 1024 output units. <br>
• ReLU Activation Layer. <br>
• Fully-connected layer with 10 output units. <br>

Expect the architecture is different to the base model and I have increased the epoch size from 10 
to 14, everything including batch size (= 64) etc. are the same to base model. The modified 
model has 95.48% accuracy on test set, comparing to 95.05% from the base model. 

• The batch normalizationn2d layer will normalize the distribution for each mini-batch, it 
will reduce data dependence and stable the learning process. I added 2 batch 
normalizationn2d layers, each one after Convolutional Layers. <br>
• For each Convolutional Layer, I added one more Convolutional Layer after them. So, I 
get deeper network that able to learn more complex patterns. <br>
• Since wider filters can learn richer features, therefore I change some filters to double 
size in convolutional layers.<br>

## [Two-View DLT based homography estimation](https://github.com/Venchi99/Computer-Vision/blob/main/DLT_homography.ipynb)

Warp the left image according to the calculated homography. The nosie generated when select uv points might
affect the recitified results. Besides, choose different uv points might product different
H matrix, therefore affect the recitified results.