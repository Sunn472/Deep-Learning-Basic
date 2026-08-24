# Deep-Learning-Basic
Deep Learning teaches a computer to learn useful patterns from large amounts of data using multiple layers of neural networks Important Deep Learning concepts
- Neuron – basic computational unit
- Weights & Bias – learned parameters
- Activation Function – introduces non-linearity, e.g. ReLU, Sigmoid, Tanh
- Loss Function – measures prediction error
- Backpropagation – calculates how weights should be changed
- Optimizer – updates weights, e.g. SGD, Adam
- Epoch – one complete pass through the training dataset
- Batch – small group of training samples
- Learning Rate – controls how much weights change during training
1. How the Network "Sees" the Image
  - A digital image is just a grid of numbers representing pixel intensities. A standard dense neural network cannot process a 2D or 3D grid directly; it requires a 1D array (a single long list) of numbers as its input.
  Grayscale: A small 28x28 pixel image contains 784 individual pixels.
  Color (RGB): A small 100x100 pixel image has three color channels (Red, Green,   Blue). This means it contains 100*100*3 = 30,000 individual pixel values.
2. The Flattening Process
  - To feed this into a basic neural network, the image must be flattened. We take the rows of the image grid and stack them end-to-end to create a single vector.
  - If you are used to working with tabular data for classification algorithms, imagine treating every single pixel as a distinct "feature" or column in a dataset. Our 100x100 RGB image becomes a single row with 30,000 features.
3.The Architecture
- Once flattened, the data moves through a standard network architecture:
<img width="783" height="391" alt="image" src="https://github.com/user-attachments/assets/f79cb0b8-5d42-42e3-89e8-ac8fda49e657" />
Input Layer: Contains one neuron for every pixel in the flattened array (e.g., 30,000 neurons).

Hidden Layers (Dense/Fully Connected): These layers process the data. In a fully connected layer, every neuron receives an input from every neuron in the previous layer. Each of these connections has an adjustable weight.

Output Layer: If you are building a classifier to identify if an image is a cat or a dog, this layer will typically have two neurons outputting probabilities.

4. The Learning Process
The network learns through standard backpropagation, just as it would with any other numeric dataset:

Forward Pass: The pixel values are multiplied by the learned weights, biases are added, and the result passes through a non-linear activation function (like ReLU or Sigmoid).

Calculate Loss: The network's final prediction is compared to the actual label using a loss function to determine how far off it was.

Backpropagation: The algorithm calculates the gradient of the loss with respect to each weight, and an optimizer adjusts the weights to minimize the error on the next pass

The Massive Limitations of This Approach
- While this basic setup can theoretically learn to classify very simple, low-resolution images, it introduces severe structural problems that make it highly inefficient for real-world computer vision tasks:

- Destruction of Spatial Information: When you flatten an image, you destroy its 2D geometry. The network no longer inherently understands that a pixel at index 10 is physically right next to a pixel at index 110. The spatial relationships that define shapes, edges, and textures are completely lost.

- Parameter Explosion: Because the hidden layers are fully connected, the number of weights grows uncontrollably. If our input layer has 30,000 neurons, and the first hidden layer has just 1,000 neurons, that single layer connection requires 30 million weights to train. This makes the model massive, computationally expensive, and highly prone to overfitting.

- No Translation Invariance: If you train the model on pictures of a cat centered in the frame, it learns specific weights for specific pixel locations. If you show it a new image where the exact same cat is shifted 10 pixels to the right, the flattened vector looks completely different to the network. It will likely fail to classify the image because it hasn't learned what a cat looks like, only where the cat's pixels were located in the training data.
