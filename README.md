# CNN_AircraftDetection
Convolution Neural Network model for aircraft detection in satellite images using keras

### Explanation

<img width="1220" alt="Screenshot 2021-04-28 at 12 10 01 AM" src="https://user-images.githubusercontent.com/36126610/116295576-ddae3480-a7b6-11eb-906b-0a846820c8b9.png">

The dimension of each image is 20*20*3 and a total of 32000 images were used. First, we input each image and store the output (aircraft present or not) which in this case is 0(not present) or 1(aircraft present). The naming convention of each image was first character being 0/1 followed by name where 0/1 represented the output of the image. In this the number of filters was increased after each layer. In the first step, 4 successive convolution & ReLU activation layer was computed with depth of layers being (20,44,68,92) and kernel size being fixed as 3*3. The dimension of next layer is computed for each X, Y direction where N-dimension size, F-kernel size, P-padding size, S-stride. In this case stride value was kept 1 and no padding was done. The dimension only changes after each convolution layer due to kernel filter applied, activation function just computes value of given input and output remains of same dimension. Activation function is applied to avoid overfitting and, in this case, ReLU computes max (0,𝑥). Then 𝑚𝑎𝑥𝑝𝑜𝑜𝑙𝑖𝑛𝑔 of dimension 2*2 filter layer is applied to downsample the data along row, column dimension. Then we flatten the layer (converting it to Fully connected layerSigmoid functionFlatten Dense ReLU ActivationMax PoolingConvolution 2DReLU Activation(4 layers)Input ImageFinal ClassificationLoss function minimisationBackward PropagationForward PropagationFully connected layer
a column vector) and then apply dense function (which connects all the convolution weights directly to given number of classes) to a 120 layered output, apply ReLU and finally apply dense to 1 class output and apply sigmoid activation function. If the value is >0.5 we classify the image as containing aircraft (value is set to 1) else a non-aircraft image is found. 

#### Mathematical Computation from Fully Connected Layer to Final Output Layer:

It has majorly 3 components: Forward computation, Backward computation and defining loss function and minimizing it. These steps are exactly same as done in neural networks just that the input layer in this is the convolved fully connected output layer. 

<img width="968" alt="Screenshot 2021-04-28 at 12 26 25 AM" src="https://user-images.githubusercontent.com/36126610/116296945-6da0ae00-a7b8-11eb-8ea2-903529cf44ae.png">

The Loss function J is a generally taken as Euclidean distance function and accordingly the weight parameters are updated. There are various ways to minimise the loss function. In case of CNN the normal gradient based approach doesn’t seem to work because the loss function may get stuck in local minima, so to avoid this we generally used Stochastic Gradient Descent with Momentum term optimisation algorithm or some higher end algorithm such as Adagrad, RMS Prop or Adams. In this Adams was used because rest other optimisation algorithm contains a hyperparameter (similar to learning rate) and finding the optimised value of that hyperparameter again either becomes another optimisation problem or using hit and trial method becomes computationally expensive.

<img width="997" alt="Screenshot 2021-04-28 at 12 28 52 AM" src="https://user-images.githubusercontent.com/36126610/116297317-c6704680-a7b8-11eb-8fdd-b6ead28331c6.png">

<img width="973" alt="Screenshot 2021-04-28 at 12 41 22 AM" src="https://user-images.githubusercontent.com/36126610/116298782-84e09b00-a7ba-11eb-93e0-77a0bd07fbb7.png">

<img width="945" alt="Screenshot 2021-04-28 at 12 42 36 AM" src="https://user-images.githubusercontent.com/36126610/116298912-accffe80-a7ba-11eb-92a0-b33bdb2b8d97.png">

Training the network:

For training the entire dataset is split into 70:30 where 70% of dataset is used for training and rest for validating. 70% of dataset is selected using random permutation. Epoch (maximum iteration) of 150 was selected and Batch size of 200. To avoid overfitting termination condition was set using ‘patience’ function. For no change in delta for 10 iteration would lead to termination of loop. The training ended after 53 iterations and for each iteration it took about 1 minute. The training dataset went up to a maximum of 99.82% while the validation accuracy achieved was about 75%. The training was performed on only CPU computation mode as GPU computational supported device was not available.

Result:

The overall accuracy on the validation data set obtained was around 98.5% while the accuracy on training data set was around 75.32%. The plots of accuracy and loss versus epochs for both training data and validation data set was plotted to visualise the sections where the model may require improvements to increase accuracy.

<img width="935" alt="Screenshot 2021-04-28 at 12 50 38 AM" src="https://user-images.githubusercontent.com/36126610/116299904-dfc6c200-a7bb-11eb-9b6b-d11c63ffed52.png">

<img width="752" alt="Screenshot 2021-04-28 at 12 46 51 AM" src="https://user-images.githubusercontent.com/36126610/116299383-43042480-a7bb-11eb-9f79-c2a2b22aea22.png">

<img width="1211" alt="Screenshot 2021-04-28 at 12 48 30 AM" src="https://user-images.githubusercontent.com/36126610/116299592-82cb0c00-a7bb-11eb-9834-bd23bf270a22.png">
