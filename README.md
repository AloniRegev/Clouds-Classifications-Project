# Defense Against Adversarial Examples in NN
Final project in a Deep Learning course at the University of Haifa. 

## Objective:
Adversarial examples are inputs to the model, for instance a deep neural network, which meant to cause the model to misclassify, hence significantly damage its accuracy. 

Standard models are oftentimes not resilient against adversarial examples, that is why in recent years there has been a lot on studies on the subject and defenses against those attacks were built. 
Such defenses are required to reverse the effects of the adversarial perturbations, and on legitimate examples not to significantly impact the classifier’s predictions `[4]`.

A common defense is adversarial training although it is efficient only against the specific attacks the model has been trained with, thus not very robust and requires a big overhead `[2]`. 

A recent method takes the most important features in the inputs and train the model on them, since feature input spaces are often unnecessarily large, which provides extensive opportunities for an adversary to construct adversarial examples. We have chosen feature squeezing since it has been proven to be relatively fast, robust and efficient `[1]`.

Therefore, we compared feature squeezing with adversarial training against two different attacks. 

## Run me
The `.ipynb` file is divided into sections according to the steps applied described below. It is possible to run the entire notebook, or each code snippet separately as long as its perquisites have been ran. Models and outputs are being saved in the main folder of the project, it’s also possible to run the pre-trained model we provided and then not run the snippet in which the model is trained. 

## Details
* **Attacks:** `Deep fool`, `Fast Gradient Sign Method attack (FGSM)`.
* **Defenses:** Adversarial training, feature squeezing in the form of median smoothing (median filter)
* **Dataset:** `Cifar10`, Collection of 60,000 32x32 color images in 10 different classes.

### Background
*	**DeepFool attack** - finds the closest separating hyperplane between classes, then projects the given image onto that hyperplane and shifts it by minimal distance such that it is misclassified. Meaning the attack misclassifies the input it with the minimal perturbation possible. 
*	**FGSM attack**– gets an input image, and uses the gradients of the loss – of the model output with respect to the input image to create an adversarial image that maximizes the loss
*	**Feature squeezing** in the form of a median filter is meant to help eliminate adversarial perturbations
*	**Adversarial training** – training the model together with adversarial inputs helps the model defend and correctly classify against the specific attack applied on it. 

### Steps
1.	**Setup:**
Create and train model on clean dataset, compute accuracy and loss as benchmark. Model architecture: Feature extractor was built from three blocks, each with 2 convolution layers, ReLu function as activation function and maxPooling was applied. The total 6 convolutions helped extract all necessary features. Kernel size used was 3, stride and padding were 1 to keep original size of image after the convolution.  Applied data augmentation to help the model robustness. Used Adam optimizer, with weight decay to help prevent vanishing gradients. Applied early stopping as well to prevent overfitting (which helped during training of pre-processed data as well). 
    * Hyper-parameters - learning rate is 0.001, batch size is 64, and maximum number of epochs is 70.
2.	**Attack model** on clean test data via FGSM, DeepFool attacks, check accuracy and loss. 
3.	**Defend model:**
    * Apply adversarial training with FGSM perturbed images on clean data, then apply attack again and compare results.
    * Pre-process training data via feature squeezing. Then train model as usual and apply each attack DeepFool and FGSM on test data, separately. Meaning, generate adversarial images on original clean model, and then test accuracy on the pre-processed model with the adversarial inputs. Comparing to performance of attacked model without feature squeezing. 

## Results and Graphs
Accuracy of the final model on the test set (in percent): 

| Defense \ Attack | DeepFool (%) | FGSM (%) | None (%) |
|---|---|---|---|
| None | 7.4 | 0.1 | 88.5 |
| Adversarial training |   | 76.9 | 81.5 |
| Feature squeezing | 77.5 | 45.3 | 80.1 |

Graphs for training of the clean model:

## Conclusions
*	We can see that both defenses of feature squeezing and adversarial training hasn’t significantly impacted the test accuracy of the model, we reached 80% accuracy and 81% vs. the original 88%.  Meaning the requirement of in adversarial examples to reverse the effects of the adversarial perturbations; and on legitimate examples, not to significantly impact a classifier’s predictions was achieved.
* It shows that feature squeezing as a defense is more effective against DeepFool rather than FGSM attack (77% accuracy vs. 45% accuracy). Perhaps because FGSM attack does not take the minimal change possible in order to mislead the classifier, as we used a non-negligible parameter of 0.1 epsilon.
Yet, significantly improves the model accuracy against both, as both attacks had caused less than 10% accuracy on the clean model. 

* Under FGSM attack adversarial training was more effective than feature squeezing, since the adversarial training is meant to prepare against a specific attack, but less robust. Reached 76% accuracy vs. 45%.  

## Resources
1. [Feature Squeezing: Detecting Adversarial Examples in Deep Neural Networks](https://arxiv.org/pdf/1704.01155.pdf)
2. [Defense Methods Against Adversarial Examples for Recurrent Neural Networks](https://arxiv.org/pdf/1901.09963.pdf)
3. [DeepFool: a simple and accurate method to fool deep neural networks](https://arxiv.org/pdf/1511.04599.pdf)
4. [Adversarial Attack and Defense on Neural Networks in PyTorch](https://towardsdatascience.com/adversarial-attack-and-defense-on-neural-networks-in-pytorch-82b5bcd9171)

### Authors: 
* [Neta Oren](https://github.com/n242)
* [Regev Aloni](https://github.com/AloniRegev)
