## Semantic Segmentation
Semantic Segmentation laid down the fundamental path to advanced Computer Vision tasks such as object detection, shape recognition, autonomous driving, robotics, and virtual reality. Semantic segmentation can be defined as the process of pixel-level image classification into two or more Object classes. It differs from image classification entirely, as the latter performs image-level classification. For instance, consider an image that consists mainly of a zebra, surrounded by grass fields, a tree and a flying bird. Image classification tells us that the image belongs to the ‘zebra’ class. It can not tell where the zebra is or what its size or pose is. But, semantic segmentation of that image may tell that there is a zebra, grass field, a bird and a tree in the given image (classifies parts of an image into separate classes). And it tells us which pixels in the image belong to which class. Here we will discuss semantic segmentation using TensorFlow Keras.

We have to build a computer vision model that can convert an input image into a segmented image (also called masked image or label image).

By understanding how semantic segmentation works, we can easily come up with an idea of how to choose our pre-trained model. One of the popular architectural approaches is FCNN (Fully Convolutional Neural Networks). In contrast to CNNs in image classification, where the decision head is made up of dense layers, an FCNN is made up of layers related to convolutional operations only. Because the final output is an image of a shape identical to the input image. 

An FCNN contains two parts: an encoder and a decoder. An encoder is a downstack of convolutional neural layers that extract features from the input image. A decoder is an upstack of transpose convolutional neural layers that builds the segmented image from the extracted features. The sizes of feature maps go down while downsampling (e.g. 128, 64, 32, 16, 8, 4 – in order), and they go up while upsampling (e.g. 4, 8, 16, 32, 64, 128 – in order).

Among FCNNs, U-Net is one of the successful architectures acclaimed for its performance in Medical Image Segmentation. It encourages skip connections between a few specific-sized layers of downstack and upstack. Skip-connections yield better performance because of the truth that upstack struggles to build finer details of the image on its own during upsampling. Skip-connections bye-pass a large stack of layers to feed finer details from a downstack layer to its corresponding upstack layer.

### U-Net model

Here, we wish to use the functional approach of U-Net architecture, but we will have our own architecture suitable to our task. The downstack can be a pre-trained CNN, trained for image classification (e.g. MobileNetV2, ResNet, NASNet, Inception, DenseNet, or EfficientNet). It can effectively extract the features. But, we have to build our upstack to match our classes (here, 59), build skip-connections, and train it with our data. 

We prefer a pre-trained DenseNet121 to be the downstack that can be obtained through transfer learning and build the upstack with pix2pix, a publicly available generative upstack template. We build the downstack with the above layers. We use the pre-trained model as such, without any fine-tuning and build a U-Net model by merging downstack and upstack with skip-connections.

We select the final ReLU activation layer for each feature map size, i.e. 4, 8, 16, 32, and 64, required for skip-connections.

The amount of training data plays a vital role in performance in a deep learning model. Limited data, in our case, maybe one reason for relatively poor performance. By tuning hyperparameters carefully, improving or changing model architectures, and increasing training data, we could achieve performance improvements.

We observe closeness to a certain level. By training for more epochs, we can obtain improvement in the results.
