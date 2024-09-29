# Image Classification Project

## Project Description
This project aims to classify images of animals into 10 different categories using a Convolutional Neural Network (CNN) model. The dataset consists of 26,179 images with categories such as dog, cat, horse, spider, butterfly, chicken, sheep, cow, squirrel, and elephant.

The model used is **ResNet152V2** as the base model, followed by several additional layers, including a custom **SelfAttention** layer, to enhance classification performance.

## Dataset
This dataset contains approximately 26,179 images of animals divided into 10 categories:
- **dog**
- **cat**
- **horse**
- **spider**
- **butterfly**
- **chicken**
- **sheep**
- **cow**
- **squirrel**
- **elephant**

The dataset is taken from [Kaggle - Animals10](https://www.kaggle.com/datasets/alessiocorrado99/animals10).

## Model Architecture
The built CNN model has the following architecture:
- **Base Model**: ResNet152V2 (pre-trained, frozen)
- **Additional Layers**:
  - Conv2D (128 filters, kernel size 3x3, activation 'relu')
  - BatchNormalization
  - MaxPooling2D (pool size 2x2)
  - Dropout (rate 0.5)
  - SelfAttention (num_channels=128)
  - GlobalAveragePooling2D
  - Dense (256 units, activation 'relu')
  - Dropout (rate 0.5)
  - Dense (10 units, activation 'softmax')

The model is trained with the **Adam optimizer** and **categorical_crossentropy** as the loss function.

## Training Process
The model is trained using a dataset split into a training set and a validation set with a ratio of 80:20. The following callbacks are used during training:
- **ReduceLROnPlateau**: Reduces the learning rate if val_loss does not improve.
- **EarlyStopping**: Stops training if val_loss does not improve for 2 epochs.
- **ModelCheckpoint**: Saves the best model based on val_accuracy.

### Saved Model Formats
The model is saved in three different formats:
- **SavedModel**: Standard TensorFlow format.
- **TF-Lite**: Optimized for mobile devices.
- **TFJS**: For running in the browser.
