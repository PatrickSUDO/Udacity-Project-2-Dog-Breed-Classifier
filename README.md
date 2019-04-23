[//]: # (Image References)

[image1]: ./images/sample_dog_output.png "Sample Output"
[image2]: ./images/vgg16_model.png "VGG-16 Model Layers"
[image3]: ./images/vgg16_model_draw.png "VGG16 Model Figure"


## Project Overview

In this project, I learn how to build a pipeline that can be used within a web or mobile app to process real-world, user-supplied images. Given an image of a dog, this algorithm will identify an estimate of the canine’s breed. If supplied an image of a human, the code will identify the resembling dog breed.

![Sample Output][image1]

## Observation and Discussion

At first I searched the paper of AlexNext, VGG, and GoogLeNet. I discarded the 11x11 convolutional kernel in AlexNet since it will slow down the calculation a lot, and I changed to 5x5 only. After that, I applied 1x1 convolutional kernel which is the concept from GoogLeNet to blend the information in different channels and increase the dimension. Then, I did the 3x3 convolution and pooling to decrease image size for many times, and I ended my feature extractor with global average pooling layer. I removed most of the MLP layers since it would slow down the calculation and sometimes lead to overfit, also, the Global Average Pooling layer can have the same function as MLP here. Therefore, only one MLP as final layer was used. Dropout layers were put before dense layer to prevent overfit.

However, it ended up classifying all the input image as human because transfered VGG-16 model didn't modifyor retrain for this task, it's parameter configuration is still 1000 outputs (ImageNet label). In the future, we can apply transfer learning ,and retrain with both human and dog images. Also, its final layer should be 2 neuron only (human and dog). Thus, we can increase the accuracy of classifying human and dog in the beginning.

## Lesson Learned for Future Improvements

1. F1 score and confusion matrix can be used to evaule the performance of the dog and human detector.
2. For my home-made CNN model, we can train more epochs to further decrease the loss. (as my observation, the validation still has some room the drop)
3. Batch normalization can be added between layers in my home-made model to avoid overfitting and make it more gerneral.
4. 2 Step gradient descent may be a good choice to speed up training. We can use Adam first and then SGD for further accuracy improvement.
5. For the transfer, we can lower the learning with more epochs to further improve its accuracy.

