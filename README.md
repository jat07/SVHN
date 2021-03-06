# SVHN

Street View House Numbers (SVHN) is a real-world dataset containing images of house numbers taken from Google's street view. This repository contains the source code needed to built machine learning algorithms that can recognize and predict house numbers on scenery images.

The dataset comes in 2 different formats, full numbers which includes numbers with up to 6 digits in length and cropped images, which is used for single digit prediction, similar to MNIST. In this repository we provide all the necessary code to address both problems.

To achieve our goal, a deep neural network was developed, and especially a Convolutional Neural Network (CNN). The implementation is based on TensorFlow.



Necessary Libraries
For the code to run, the following libraries are needed which can be installed via pip:

Numpy: pip install numpy
Scipy: pip install scipy
Matplotlib: pip install matplotlib
H5py: pip install h5py
Pillow: pip install Pillow
scikit-learn: pip install scikit-learn
Tensorflow: pip install tensorflow For CPU only, or pip install tensorflow-gpu for TensorFlow with GPU support (also needs CUDA and cuDNN installation)
Project Structure
Data directory
Before running the code, we need to download SVHN datasets from here. For running the algorithm for the single digit problem, only the 3 .mat files are needed. For full format numbers, the .tar.gz files are required. The data should be stored in a directory with name res with the following structure:

res
cropped
original
extra
train
test
processed
Cropped directory should contain the 3 .mat files. Every folder under the original directory should contain the contents of the corresponding .tar.gz archieve, after it has been decompressed. Finally, processed directory will keep the images of full format, after they have been pre-processed (we will talk about this in a while)

Source directory
src directory contains the source code and it includes 2 folders containing the files explained below:

single_digit: Contains all the files needed to run a CNN for the cropped digits format

digit_statistics.py An independent script for creating a plot regarding the distribution of the images across all different images in each subset (train, test, extra)
display_image.py An independent script responsible for loading a given house number image and visualize it in 4 different formats (raw, gray-scale, normalized and gray-scale normalized)
mlp.py A Multi Layer Perceptron baseline approach for predicting the digit on the image. Not big emphasis was given in this approach.
cnn.py An implementation of Convolutional Neural Networks for predicting the number on an image. Note that the current parameters used have been selected after running a lot of different experiments. This scripts just loads the data, trains the model on-the-fly and evaluates it with the test set.
svhn.py A class that contains all the necessary functionality for loading the data from the .mat files, load them into numpy arrays and then feed them to the neural network.
multi_digit: Contains all the files needed to run a CNN for the full numbers format

digit_statistics.py An independent script for creating a plot regarding the distribution of digit lengths across all different images in each subset (train, test, extra)
display_image.py An independent script responsible for loading a given house number image and visualize it in 4 different formats (raw, gray-scale, normalized and gray-scale normalized)
svhn.py An independent script for reading raw images, processes them, crops them around the bounding boxes of every digit and resize them to 64x64 pixels.
cnn.py CNN implementation for recognizing and predicting numbers in multi-digit images.
Note: While the script svhn.py is called from cnn.py to load the images in cropped digits problem, for the case of multi-digit is different. There, the svhn.py is an independent script which must be run before running the CNN, so that it processes the raw, variable resolution images. Its constructor accepts a series a parameters to determine things like maximum acceptable digit length, grayscaling, normalization, etc. It also accepts the output directory path, which must be placed under res/processed. For instance res/processed/gray_4, for a processing that keeps only images with up to 4 digits, converted to grayscale.

Logs Directory
When cnn.py scripts runs for either case, it creates a directory named logs, which stores execution logs needed for TensorBoard. TensorBoard can be started by issuing the command tensorboard --log-dir=logs/single for logs regarding single digits problem, or tensorboard --log-dir=logs/multi for multi digit. TensorBoard can be accessed from localhost:6006.

Results
For the cropped digits format we were able to achieve an accuracy of 95.74%.

For the full numbers format we used to different accuracies. The accuracy of predicting correctly any digits on an image(single accuracy), and an accuracy of predicting all numbers correctly at the same time(multi accuracy). For the single accuracy we scored a high of 96.87% and for the multi accuracy a 87.68%. Most approaches and implementation use the single accuracy as a metric. We just provided the multi accuracy as another useful indicator. An interesting comparison of results of our achievement against other published papers, can be found here
