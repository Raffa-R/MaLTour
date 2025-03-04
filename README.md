# EducaTour Model (Transfer Learning from EfficientNetV2B0, DenseNet121, Xception)
In creating machine learning models for EducaTour, we created 3 different models, all three using the transfer learning method. Where the three pre-trained model architectures are EfficientNetV2B0, Dense121, and Xception. The aim of making these three models is to compare which model is the best of the three models. The elements reviewed are model accuracy and model size. A good model is a model that has the highest accuracy and the smallest size.

## Table of Contents
[1. EfficentNetV2B0](#efficientnetv2b0)<br>
[2. Xception](#xception)<br>
[3. DenseNet121](#densenet121)<br>
[4. Model Report Comparison](#model-report-comparison)
  - [Training and Validation Accuracy and Loss](#training-and-validation-accuracy--loss)<br>
  - [Confusion Matrix](#confusion-matrix-comparison)<br>
  - [Prediction Preview](#prediction-preview-comparison)<br>
  - [Test on Undefined Data](#undefined-data-test-comparison)<br>
  
[5. Model Inference Strategy](#model-inference-strategy)<br>
[6. Access to Models](#access-to-models)<br>
[7. Summary](#summary)<br>

## EfficientNetV2B0
EfficientNet was created by Mingxing Tan and Quoc V. Le from Google in 2019. EfficientNet uses compound coefficients to uniformly scale the depth (number of layers), breadth (number of channels), and resolution of input images on a CNN network. This is different from other architectural approaches which carry out this scaling irregularly. From the research results, EfficientNet's accuracy on ImageNet data significantly outperforms other CNN architectures. Therefore, the EfficientNet model architecture was chosen to create a model using the transfer learning methods.

For the EfficientNet model, there was a particular strategy, Which is to train several layers in the network, namely the layers at the back and the fully connected/DNN layer. In this case, the number of back layers to be trained with the prepared training set must be determined first. In this strategy, 125 back layers in the EfficientNet architecture are retrained and the rest are retained (frozen).
![alt text][efficient-arch]
Source: [Complete Architectural Details of all EfficientNet Models](https://towardsdatascience.com/complete-architectural-details-of-all-efficientnet-models-5fd5b736142)

## Xception
Xception model stands for "Extreme Inception." The Inception architecture is used as a foundation, but depthwise separable convolutions are used instead of the regular Inception modules. A more effective model with enhanced performance is the end outcome of this.

For the Xception model, the strategy was use depthwise separable convolutions are used instead of the regular Inception modules. So a more effective model with enhanced performance is the end outcome of this. Depthwise Separable Convolutions factorize a standard convolution into a depthwise convolution (which applies a single filter to each input channel) followed by a pointwise convolution (which applies a 1x1 convolution to combine the outputs from the depthwise convolution). 
![alt text][xception-arch]
Source: [Review: Xception — With Depthwise Separable Convolution, Better Than Inception-v3 (Image Classification)](https://towardsdatascience.com/review-xception-with-depthwise-separable-convolution-better-than-inception-v3-image-dc967dd42568)

## DenseNet121
DenseNet121 (Dense Convolutional Network) is an architecture that focuses on making the deep learning networks go even deeper, but at the same time making them more efficient to train, by using shorter connections between the layers. DenseNet is a convolutional neural network where each layer is connected to all other layers that are deeper in the network, that is, the first layer is connected to the 2nd, 3rd, 4th and so on, the second layer is connected to the 3rd, 4th, 5th and so on. This is done to enable maximum information flow between the layers of the network. To preserve the feed-forward nature, each layer obtains inputs from all the previous layers and passes on its own feature maps to all the layers that will come after it. Source: [Creating DenseNet 121 with TensorFlow](https://towardsdatascience.com/creating-densenet-121-with-tensorflow-edbc08a956d8)

## Model Report Comparison
### Training and Validation Accuracy & Loss
#### EfficientNetV2B0
![alt text][efficient-acc-n-loss]
#### Xception
![alt text][acc-n-loss]
#### DenseNet121
![alt text][dn-acc]
![alt text][dn-loss]

### Confusion Matrix Comparison
#### EfficientNetV2B0
![alt text][cm-efficient-net]
#### Xception
##### Before Fine Tuned
![alt text][cm-1]
##### After Fine Tuned
![alt text][cm-2]
#### DenseNet121
![alt text][cm-dense-net]

### Prediction Preview Comparison
#### EfficientNetV2B0
![alt text][pre-3]
#### Xception
##### Before Fine Tuned
![alt text][pre-1]
##### After Fine Tuned
![alt text][pre-2]
#### DenseNet121
![alt text][pre-4]

### Undefined Data Test Comparison
#### EfficientNetV2B0
![alt text][undefined-efficient]
#### Xception
![alt text][undefined-xception]
#### DenseNet121
![alt text][undefined-dense]

## Access to Models
You can access all the three models [here](https://drive.google.com/drive/folders/10V5Z3o4rDMZQO_G7K_Dt6571nVGkCzN4?usp=sharing)

## Model Inference Strategy
We put the model in the server so the user will send the picture they have taken. We choose this method because:
1. **Computational Power**: Servers typically have more computational resources (CPU, GPU) than edge devices, allowing for faster and more complex model inference.
2. **Ease of Update**: Updating models on a server is simpler and more centralized, without the need to push updates to numerous edge devices.
3. **Data Aggregation**: Centralized predictions allow for easier aggregation and analysis of data, facilitating better monitoring, logging, and refinement of the model.
4. **Security**: Servers can provide better security measures to protect the model and data, reducing the risk of unauthorized access and data breaches.
5. **Consistent Environment**: Running the model on a server ensures a consistent and controlled environment, avoiding the variability in hardware and software across different edge devices.
6. **Scalability**: Server infrastructure can be scaled up to handle more requests by adding more computational resources, while edge devices have limited scalability.
7. **Maintenance and Management**: Centralized management of the model is easier for maintenance, debugging, and troubleshooting compared to distributed edge deployments.

## Summary
To sum up, Educatour ML team did comparison between three architecture models. From the evaluation we can infer that every architecture
share similar accuracy. However, in the end we chose the EfficientNetV2B0 as it has the smallest size among them all. Also, we put the
model in the server and let the server to execute the model inference for some reason such as Computational Power, Ease of Update, and
Consistent Environment.

[efficient-arch]: https://miro.medium.com/v2/resize:fit:2000/format:webp/1*rnhgFRXetwD8PvxhZIpwIA.png
[xception-arch]: https://miro.medium.com/v2/resize:fit:863/1*VvBTMkVRus6bWOqrK1SlLQ.png "Xception Architecture"
[acc-n-loss]: ./assets/__results___56_0.png "Xception Training and Validation Accuracy & Loss"
[dn-acc]: ./assets/densenet_acc.png "DenseNet121 Training and Validation Accuracy"
[dn-loss]: ./assets/densenet_loss.png "DenseNet121 Training and Validation Loss"
[efficient-acc-n-loss]: ./assets/efficientnet_trainval_plot.png "EfficientNetV2b0 Training and Validation Accuracy & Loss"
[cm-1]: ./assets/__results___46_0.png "Confusion Matrix Xception Before Fine Tuned"
[cm-2]: ./assets/__results___65_0.png "Confusion Matrix Xception After Fine Tuned"
[cm-dense-net]: ./assets/densenet_cm.png "Confusion Matrix DenseNet121"
[cm-efficient-net]: ./assets/efficientnet_cm.png "Confusion Matrix EfficientNetV2b0"
[pre-1]: ./assets/__results___42_0.png "Xception Prediction Preview Before Fine Tuned"
[pre-2]: ./assets/__results___62_0.png "Xception Prediction Preview After Fine Tuned"
[pre-3]: ./assets/model_2_classification_result.png "EfficientNetV2b0 Prediction Preview After Fine Tuned"
[pre-4]: ./assets/densenet121_test.png "DenseNet121 Prediction Preview"
[undefined-efficient]: ./assets/efficientnet_undef_test.png "EfficientNetV2b0 test on undefined data"
[undefined-xception]: ./assets/xception_undef_test.png "Xception test on undefined data"
[undefined-dense]: ./assets/dense_net_undef_test.png "DenseNet121 test on undefined data"
