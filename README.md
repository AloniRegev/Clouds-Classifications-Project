# Defense Against Adversarial Examples in NN
Final project in a Deep Learning course at the University of Haifa. 

## Objective:
Adversarial examples are inputs to the model, for instance a deep neural network, which meant to cause the model to misclassify, hence significantly damage its accuracy. 
Standard models are oftentimes not resilient against adversarial examples, that is why in recent years there has been a lot on studies on the subject and defenses against those attacks were built. 
A common defense is adversarial training although it is efficient only against the specific attacks the model has been trained with, thus not very robust and requires a big overhead [2]. 
A recent method takes the most important features in the inputs and train the model on them, since feature input spaces are often unnecessarily large, which provides extensive opportunities for an adversary to construct adversarial examples. We have chosen feature squeezing since it has been proven to be relatively fast, robust and efficient [1]. 
Therefore, we compared feature squeezing with adversarial training against two different attacks. 

## Details
Attacks: Deep fool, Fast Gradient Sign Method attack (FGSM)
Defenses: Adversarial training, feature squeezing in the form of median smoothing (median filter)
Dataset: Cifar10, Collection of 60,000 32x32 color images in 10 different classes.  

## Run me
The .ipynb file is divided into sections according to the steps applied described below. It is possible to run the entire notebook, or each code snippet separately as long as its perquisites have been ran. Models and outputs are being saved in the main folder of the project, it’s also possible to run the pre-trained model we provided and then not run the snippet in which the model is trained. 

## Steps
1.	Setup:
Create and train model on clean dataset, compute accuracy and loss as benchmark. Model architecture: Feature extractor was built from three blocks, each with 2 convolution layers, ReLu function as activation function and maxPooling was applied. The total 6 convolutions helped extract all necessary features. Kernel size used was 3, stride and padding were 1 to keep original size of image after the convolution.  Applied data augmentation to help the model robustness. Used Adam optimizer, with weight decay to help prevent vanishing gradients. Applied early stopping as well to prevent overfitting (which helped during training of pre-processed data as well). 
Hyper-parameters: learning rate is 0.001, batch size is 64, and maximum number of epochs is 70.
2.	 Attack model on clean test data via FGSM, DeepFool attacks, check accuracy and loss. 
3.	Defend model:
* Apply adversarial training with FGSM perturbed images on clean data, then apply attack again and compare results.
* Pre-process training data via feature squeezing. Then train model as usual and apply each attack DeepFool and FGSM on test data, separately. Meaning, generate adversarial images on original clean model, and then test accuracy on the pre-processed model with the adversarial inputs. Comparing to performance of attacked model without feature squeezing. 

## Results:

### Authors: 
* [Neta Oren](https://github.com/n242)
* [Regev Aloni](https://github.com/AloniRegev)
