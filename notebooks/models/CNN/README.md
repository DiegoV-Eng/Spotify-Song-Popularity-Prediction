## Neural Networks

### Experimental design

 The application of Neural Networks for classifying the popularity of songs in the dataset involves the following inital steps:

 1. Data Loading: Loaded the integrated dataset containing audio features and populairty labels of the songs.

 2. Image Extraction: Extracted spectrogram images for each track using the provided 'preview_url' and linked the images to the dataset.

 3. Popularity Binning: The 'popularity' column was binned into three categories: low, medium, and high.

 4. Data Sampling: Sampled 10,000 values from the dataset, ensuring each entry is associated with a sprectogram image. 

### Analyzing Spectrograms

 Spectrograms serve as a powerful tool for converting the audio features of songs into visual representations. Understanding the nuances of spectrogram images is crucial for comprehending how the neural network interprets and learns from these representations.

 1. Frequency Analysis:

      Spectrograms represent the distribution of frequencies in an audio signal. The horizontal axis represents time and the vertical axis represents frequency. The color intensity represents the magnitude of the frequencies. Darker areas indicate more intense frequencies while lighter areas indicate less intense frequencies.

 2. Patterns:

      Changes in color intensity in the spectrogram represents patterns within the audio signal. For instance, distinct patterns may represent beats, tempo, or other features in the song. The network can learn to associate these patterns with different levels of popularity.

 3. Feature Extraction:

      Spectrogram images capture essential features of the audio, such as music keys, instrumentalness, or vocal patterns. The neural network uses these features to make predictions about the popularity of songs.

 Sample Spectrogram Images:

![Untitled-3-2](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/assets/89276533/b8a082d8-2546-4d98-b906-bc320957bdd1)

 In these samples, we can clearly identify the following aspects:

 1. Distinct Patterns: This indicates the varying musical elements.
 2. Intensity Variations: This indicates the changes in the audio signal.
 3. Time-Frequency Relationship: This indicates how the frequency changes over the course of song's duration.

 The neural network processes these spectrogram images to identify intricate features such as the presence of certain instruments, the complexity of the audio, or the density of frequency content.


### Neural Network Architecture

 The Neural Network Architecture is a critical aspect of the experiment, outlining the structure and layers of the Convolutional Neural Network (CNN). It is defined using Keras Sequential Model.

 1. Input Layer:
 
      The input layer accepts the spectrogram images derived from the audio features and serves as the entry point of the neural network. 

 2. Convolutional Layer:

      This layer acts as the backbone of the neural network. In our model, convolutional layer is applied to filter the input images to extract relevant features. The choice of 32 filters of size(3,3) is common in image processing tasks. It provides the network with abilty to get 32 feature maps. The choice of using ReLU function was based on that it helps the model learn complex patterns within the images. 

 3. MaxPooling Layer:

      Following the convolutional layer, Maxpooling layer is applied to reduce the complexity of data. This layer uses a size of (2,2) which reduces the quantity of pixels in the images.

 4. Flattening Layer:

      This layer transforms the 2D array obtained from the previous layer into 1D array. This prepares the data for the subsequent dense layers.

 5. Dense Layers:

      These layers are fully-connected layers used to process the flattened data to learn high-level representations. In our model, 64 dense layers are applied with ReLU activation function. This facilitated the network to read more complex patterns in the data.

 6. Dropout Layer: 

      A Dropout Layer with a dropout rate of 0.5 is applied to prevent overfitting. Therefore, it randomly drops out 50% of the neurons during trainning. This regularization technique enhances the model's ability to generalize the unseen data.

 7. Output Layer:

      The final layer consists of three neurons, each representing a popularity category (Low, Medium, or High). The softmax activation function is applied to obtain a probaility distribution across these categories.


### Results

 Trainning Performance:

 The neural network was trainned over 10 epochs on the sampled dataset and the results are summarized below:

 1. The model quickly achieved a high trainning accuracy of approximately 96%. 
 2. Training loss had a steady decline.
 3. Validation loss maintained stability

 Testing Performance:

 The trained neural network was evaluated on the test set, and the following results were obtained:

 1. The test accuracy was 96.35%
 2. This confirmed the model's capability to classify song popularity based on spectrogram images.

![Untitled-4-2](https://github.com/dmml-heriot-watt/group-coursework-machine-learners/assets/89276533/484ceba1-8ba4-4785-9999-25269a13f5ed)

### Discussion

 Model Performance:

 The achieved test accuracy of 96.35% reflects the model's efficiency in classifying songs into their respective popularity categories. This high accuracy suggests that the neural network can effectively learn and generalize patterns from spectrogram images.

 Quick Convergence:

 The model quickly converges during the initial epochs, indicating efficient learning from the training data. This quick convergence is a positive aspect, especially considering the large dataset and complex image features.

 Stable Trainning Performance:

 The stability of the training accuracy throughout the epochs indicated the model's ability to consistently learn and adapt. This makes the neural network architecture robust.

 Generalization to Unseen Data:

 The model's ability to maintain a high level of accuracy on the test set implies successful generalization to previously unseen data. This affirms the model's potentiality for real-world applications.
