---
layout: posts
title: "CS231n summary: Week1 ~ Week7"
excerpt: "summary of the cs231n lectures from week1 to week7"
comments: true
categories: 
- pytorch
- cs231n

tags: 
- pytorch
- euron
---

*This post still needs some updates!*

## Week 1
- Week1 summary
### **1. Lecture's Agenda 🍐**

* **A brief history of computer vision**

* **CS231n overview**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

* **A brief history of computer vision**
  -  **Block world(Larry Roberts, 1963)**: early 1960' was the start of computer vision.
  -  **The summer vision project of MIT(Saymour Papert, 1966)**: it's an attempt to construct a significant part of a visual system(pattern recognition).
  -  **VISON(David Marr, 1970')**: input image → primal sketch →  2.5D sketch →  3D model
  -  **Similar ideas in 1970'**: (every obj → simple geometric primitives), (complex structure → collection of simpler shapes & geometric configuration)
      -  Generalized cylinder(Brooks & Binford, 1979)
      -  Pictorial structure(Fischelr and Elschlager, 1973)
  - **Face detection(Viola & Johnes, 2001)**: real-time face detector
  - **Histogram of gradients(Dala & Triggs, 2005)**
  - **PASCAL Visual Object Challenge(2006~2012)**: 20 obj categories
  - **ImageNet**: solve a harder question, to recognize every objects.
    - most of ML algorithms such as graphical machine, SVM, AdaBoost was very easy to overfit due to the complexity of visual data.
    - an attempt to overcome dual reasons.
    - 1. images are too complex, so models have to have high dimension of input and a lot of parameters to fit.
    - 2. if training data is not enough , overfitting happens so fast.
    - Error rate of models using ImageNet is steadily decreasing. Especially, 2012 was the breakthrough moment.

* **CS231n overview**
  - CS231n focuses on one of the most important problems of visual recognition - image classification.
  - There is a number of visual recognition problems that are related to image classification, such as obj detection, img captioning.
  - CNN(Convoutional Neural Networks) have become an important tool for obj recognition.
    - large scale visual recognition challenge: deeper networks / NEC-UIUC → SuperVision → GoogLeNet, VGG → MSRA
  - CNNs were not invented overnight.
    - CNN for recognizing digits(LeCun, 1998): transistors 
    - AlexNet(Krizhevsky, 2012): transistors, GPUs / increased computer availability, labeled datasets was comparatively enough 
  - The quest for visual intelligence goes far beyond obj recognition.
    - computer vision models that see(understand) a scene like human visual system.
    - it's far to develop network models to understand complex images. 

### **3. Summary(알게 된 내용 요약) 🧠**

- HW availablity(computational ability from GPUs, etc) and labeled data in computer vision are super-important in computer vision.
- It's still hard to understand complex images using computer vision.


## Week 2
- Week2 summary
### **0. Before the Class**
- Numpy: efficient vectorize operation

### **1. Lecture's Agenda 🍐**
- **Introduction to Image Classification methods**
  - **K-Nearest Neighbor(K-NN)**
  - **Linear classifiers: SVM, Softmax**
  - **Two-layer neural network**
  - **Image features**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

- **Image Classification**
    - a core task in computer vision
    - **Problem**: semantic gap
      - there is a gap btw semantic idea and pixel values of an image.
     
    - **Challenges**
      - 1. viewpoint variation
      - 2. illumination
      - 3. deformation
      - 4. occlusion
      - 5. background clutter
      - 6. intraclass variation
      
    - **Structure of image classifier**
      - there is no obvious way.
      - there is an attemp to extract features of images with finding edges, corners and boundaries.
    
    - **Data-driven approach**
      1. Collect a dataset of images and labels
      2. Use ML to train a classifier
      - there are basically two functions in a classifer: **train function** and **predict function**
      3. Evaluate the classifier on new images
      
    - 1st classifier: **Nearest Neighbor**
      - **distance metric** to compare images: **L1 distance**
      - memorize training data
      - for each test image, find closest train image and predict label of **nearest image**
      - with N examples, how fst are training and prediction?: Train O(1), Predict O(N)
      
        : classifiers should be **fast** at prediction; **slow** for training is ok
        
        : when a model is deployed, it should be fast, however, nearest-neighbor is slow at prediction.
       
     - 2nd classifier: **K-Nearest Neighbors**
        - instead of copying label from nearest neighbor, take majority vote from K closet points
        - **distance metric**: L1, L2
        - 1. **L1**: Manhattan distance; more dependent on corrdinate system
        - 2. **L2**: Euclidean distance
        - different distance ⇒ different assumption
        - **never used on image**
        - 1. very slow at test time
        - 2. distance metrics on pixel are not informative(not very good measure for img classification
        - ex. {original, boxed, shifted, tinted} imgs usually have the same L2 distances
        - 3. curse of dimensionality

    - **Hyperparameters**
      - **choices about the algorithm that we set** rather than learn
      - such as k and distance metric in K-NN
      - these are very **problem-dependent**: must try them all out and see what works best
      - when setting hyperparameters
      - 1. split data into **three groups**(**train, val, and test**); choose hyperparameters on val and evaluate on test
      - 2. **cross-validaiton**: split data into **folds**: useful for small datasets, but not used too frequently in DL
      - choose hyperparmeters using the **validation set**, **NOT test set**

- **Linear Classification**: superimportant
  - linear classifers ⇒ neural network
  - linear classifer: f(x,W) = Wx + b
    - **x**: input image
    - **W**: parameters ir weights
    - **b**: bias(considering unbalance of dataset)
    - **f(x,W)**: score function of classifier
    

- **Coming up!**
  - **Loss function**: quantifying what it means to have a "good" W
  - **Optimization**: start with random W and find a W that minimizes the loss
  - **ConvNets**: tweak the functional form of f

### **3. Summary(알게 된 내용 요약) 🧠**

- K-NN methods are not very good for image classification.
- It's important to try classification models all out for choosing the best hyperparameters.

## Week 3
- Week3 summary
### **0. Before the Class**

- **Recall from last time**
    - Challenges of recognition: viewpoint, illumination, deformation, occlusion, clutter, intraclass variation
    - data-drive approach: kNN
    - linear classifier: parametric model → loss function & optimization

### **1. Lecture's Agenda 🍐**

- **Introduction to Image Classification methods**
    - **K-Nearest Neighbor(K-NN)**
    - ***Linear classifiers: SVM, Softmax***
    - **Two-layer neural network**
    - **Image features**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

- **Loss function**: quantifying what it means to have a "good" W

    - **use "-log" instead of "log**: actually loss function quantifying badness of model, so in order to make the output of loss function become 1 when   
    - **Multiclass SVM Loss (=Hinge Loss)**: Multiclass Support Vector Machine loss
        - Δ(margin): hyper-parameter
        - using Max

    - **Softmax Classifier:** multinomial logistic regression
      - logistic regression: sigmoid
      - calculate probability using exp
      - sentive to data

    - **Data loss** and **Regularization loss**
        - **Regularization**: L1 normalization, L2 normalization
        - λ: hyper-parameter, control the normalization; if λ increases, the model becomes simple since regularization loss increases 

- **Optimization**: start with random W and find a W that minimizes the loss
  - **slope → gradient(vector)** 
  - **numerical gradient**
  - **3 step to caculate numerical gradient**
    - (1) W
    - (2) increment 1st element of W by a small value h
    - (3) recompute the loss

  - **analytic gradient**
  - **gradient check**
  - **gradient descent(GD)**
  - **stochastic gradient descent(SGD)**: random mini batch
  - **RMSprop**: step size
  - **Adam**: momentum
  
- **Image Features**: color histogram(color spectrum), HoG(edge orientation), bag of words(benchmarked from NLP)
- **ConvNets**: tweak the functional form of f
 

### **3. Summary(알게 된 내용 요약) 🧠**

- We should decide normalization method according to how the complexity of a data needs to be reflected to a model.
- Differences between various optimizers(SGD, RMSprop, Adam)


## Week 4
- Week4 summary
### **0. Before the Class**

- we define
    - score function: s = f(x;W) = Wx
    - SVM loss: L_i = Σ j≠y_i max(0, s_j - s_y_i + 1)
    - data loss + regularization:  L = 1/N Σ i=1~N (L_i) + Σk ((W_k)^2)

    → still want to minimize loss function : gradient of L with respect to W = ∇wL → optimization

    - optimization
        - gradient descent: numerical gradient, analytic gradient

### **1. Lecture's Agenda 🍐**

- **Backpropagation**
- **Gradients for vectorized code**
- **Neural Network**
- **Neuron and Neural Network**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

- **Backpropagation:** computation graph ← chain rule
    - we want: ∂f/∂x, ∂f/∂y, ∂f/∂xz
        - ∂f/∂x = ∂f/∂q * ∂q/∂x
        - local gradient: ∂z/∂x, ∂z/∂y
        - gradient: ∂L/∂z
        - gradient = local gradient × upstream gradient

- **Gradients for vectorized code:** Jacobian matrix ∂f/∂x
  - Jacobian matrix: expression of derivatives in multivariable function
  - size of Jacobian matrix = (input size)×(input size)
  - size of gradient = size of variable : they should have the same shape with each other

- **Neural Network**
  - linear score function: f = Wx 
  - 2-layer neural network: f = W2(max(0,W1x))
  - 3-layer neural network: f = W3(max(0,W2(max(0,W1x))))

- **Neuron and Neural Network**
  - axon form a neuron: x0
  - synapse: × w0
  - dendrite: w0x0
  - cell body: Σ wixi + b
  - activation function: f
  - output axon: f(Σ wixi + b)
  - but acutally, biological neuron and nerual network are different 
  
### **3. Summary(알게 된 내용 요약) 🧠**
- backprop uses chain rule
- brain ananlogy of neural network is just conceptual one, and neural net is actually different from biological brain network.

## Week 5
- Week5 summary
### **0. Before the Class**

- History of CNN
  - 1957, perceptron: weight W update rule → w<sub>i</sub>(t+1) = w<sub>i</sub>(t) + α(d<sub>j</sub> - y<sub>j</sub>(t))x<sub>j,i
  - 1960, multilayer perceptron network
  - 1986, backpropagation: ∂E<sub>p</sub>/∂w<sub>ji</sub> = ∂E<sub>p</sub>/∂o<sub>pj</sub> * ∂o<sub>pj</sub>/∂w<sub>ji</sub>
  - 2006, deep learning
  - 2012, AlexNet → CNN, batch normalization
  
### **1. Lecture's Agenda 🍐**

- **Architecture of CNN**
- **Layers of CNN**
- **Structure of CNN**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

- **Architecture of CNN:** computation graph ← chain rule
    - fully connected layer(FC layer/Dense Layer/Flatten Layer): 32×32×3 → 3072×1(input) ⇒ Wx ⇒ activation layer: 1×10
    - convolutional layer: 32×32×3(input)⇒ 5×5×3 filter: spatially dot product
      - filter slides over the input image(convolve) several times: w<sup>T</sup>x + b
      - activation map
      - the number of filters, the size of filters, stride
    
- **Layers of CNN:** 
  - convolutional layer
    - local connectivity
    - spatial arrangement
    - parameter sharing
  - pooling layer: commonly use maxpooling
    - to reduce the number of parameters(computation)
  - fully-connected layer
  
- **Structure of CNN**
  - INPUT ->  ((CONV -> RELU) x N -> POOL?)x M -> (FC -> RELU) x K -> FC
    - POOL?: optional
    - K activations
    - commonly 0<=N<3, M>=0, 0<=K<3

### **3. Summary(알게 된 내용 요약) 🧠**
- ConvNets stack CONV, POOL, FC layers
- Trend: smaller filers, deeper architectures, getting rid of POOL/FC
- ResNet, GoogLeNet

## Week 6
- Week6 summary
### **0. Before the Class**

- computational graphs: f = Wx + regularization
- neural net: hidden layers
- CNN: separate activation maps
- mini-batch SGD

  
### **1. Lecture's Agenda 🍐**: training neural nets

- **Activation Functions**
- **Data Preprocessing**
- **Weight Initialization**
- **Batch Normalization**
- **Babysitting the Learning Process**
- **Hyperparameter Optimization**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

- **Activation Functions:** 
   - sigmoid function
      - gradient vaninshing satured neurons kill the gradients → problematic during backpropagation
      - outputs are not zero-centered
      - exp() is a bit compute expensive
  - tanh
  - ReLU
    - people like to initialize ReLU neurons with slightly positive biases
  - Leaky ReLU & PReLU
  - ELU
  - Maxout
    
- **Data Preprocessing**
  - zero-centered & normalized data
    - np.mean, np.std
  - PCA & whitening
    - PCA: decorrelated data, data has diagonal covariance matrix
    - whitened data: covariance matrix is the identity matrix
   - image data preprocessing
      - commonly preprocess until zero-centered
  
  
- **Weight Initialization**
  - small random numbers
  - large random numbers
  - Xavier initialization

- **Batch Normalization**
  - prevent gradient vanshing
  - prevent covarience shift
  - do not have to be used when dropout is applied
  
- **Babysitting the Learning Process**
  - 1) preprocess the data
  - 2) chose the architecture
  - 3) double check that the loss is reasonable

- **Hyperparameter Optimization**
  - cross-validation strategy
    - random search vs grid search
  - network architeture, learning rate, its decay schedule, update type, regularization

### **3. Summary(알게 된 내용 요약) 🧠**
- **Activation Functions**: use ReLU
- **Data Preprocessing**: images; subtract mean
- **Weight Initialization**: use Xavier init
- **Batch Normalization**: use
- **Babysitting the Learning Process**
- **Hyperparameter Optimization**: random samples

## Week 7
- Week7 summary
### **0. Before the Class**

  
### **1. Lecture's Agenda 🍐**

- **Fancier Optimization**
- **Regularization**
- **Transfer Learning**

### **2. Several Note-takings about the Lecture(내용 정리) 🧙**

- **Fancier Optimization:** 
  - problems with SGD
    - loss function has high condition number
    - local minima
    - saddle point: common in high dimension
    - gradients com from minibatches: noisy
  - SGD + momentum term
  ```python
  vx = 0
  while True:
    dx = compute_gradient(x)
    vx = rho * vx + dx // vx: velocity, rho: friction coefficient
    x += learning_rate * vx
  ```
  - Nesterov momentum
    - functioning well in convex optimization
    - functioning badly in nonconvex optimization like NN
  - Adagrad
    - grad squared term 
     ```python
    grad_squared = 0
    while True:
      dx = compute_gradient(x)
      grad_squared += dx * dx
      x -= learning_rate * dx / (np.sqrt(grad_squared) + 1e-7)
    ```
  - RMSProp
  - Adam(almost)
  - Adam(full form)
  
- **Regularization**
  - L1 regularization, L2 regularization 
  - dropout
  - data augmentation
  - batch normalization also can bring regularization effect
  
- **Transfer Learning**
  - have some dataset of interest but it has <~1M images
  - can use pretrainined with similar data 


### **3. Summary(알게 된 내용 요약) 🧠**
- optimization
  - momentum, RMSProp, Adam 
- regularization
  - dropout 
- transfer learning   
