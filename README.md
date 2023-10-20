
# DeepSpark

This repository contains both the data and code required to develop and train an algorithm for detecting Calcium Sparks in sequences of cardiomyocyte images captured using fluorescence microscopy.

It has been developed in a Python notebook using Google Colab, so a tool that can edit and execute .ipynb files is required. There are comments and clarifications throughout the notebook to facilitate and speed up the understanding of the code and the tasks carried out, as well as the explanation of what is carried out in each section. The code file is *DeepSpark.ipynb*. 

## Data Organization
The data of the biophysical model is organized in a folder called *IMAGENES*. Inside *IMAGENES* there are 10 folders with the name CELL\{i} , with i ranging from 1 to 10. These are the 10 experiments carried out and mentioned in the paper. Each CELL folder contains a file named *sparks.xlsx* which contains information about the sparks present in the 360 images of the respective experiment. In addition, inside each folder of every cell there are folders with images of the experiment carried out in different noise conditions, tagged with values 0, 1, 2, 3, 5, 10, 15, 20, with 20 being the highest level of noise. In every noise folder, the data used during the project has been the data inside the subfolder SCALE10. The levels of noise are characterized by the following SNR values: 

|     Noise     | mean SNR |  s.e.m  |
|--------------:|---------:|--------:|
|  0       | 45.1911  | 0.5108733929771045  |
|  1       | 34.5226  | 0.1429235642105408  |
|  2       | 29.2216  | 0.15282696490725592 |
|  3       | 25.7405  | 0.15860267773466136 |
|  5       | 21.4976  | 0.14976363301704765 |
|  10      | 16.3741  | 0.13930535843336148 |
|  15      | 14.0582  | 0.24276202210348174 |
|  20      | 12.3465  | 0.219346928408418   |

The folder named GFP30_RO_01_Serie2_SPARKS, contains the experimental images of cardiomyocytes.

The algorithm requires as input a sequence of images normalized to [0,1]. This normalization is carried out dividing all pixel values of the images by the maximum possible value a pixel image can take along all the sequence. The output is a list of the predicted sparks with the following information: Position x, Position y, open time (ms), close time (ms).

## Models and Results
The Models folder contains the DeepSpark encoder-decoder trained model (*DeepSpark*) and can be loaded to python with the function *keras.models.load_model()*. On the other hand, the Results folder contains the *DeepSpark.xlsx* file with the performance (TPR and F1-score), alongside other information, of the DeepSpark model in cells 1 to 5 in all levels of noise. This is unseen data during the training, and is used for the model validation and comparison with the reference model. Additionally, it also contains the *pooled_sparks.xlsx* file, that has the same information as *DeepSpark.xlsx* but from the reference model.
