# Machine Learning Project - Image Classification
This project is mostly focus on applying my deep learning - Neural Networks. For the purpose of this project my teammates and myself work on an image classification issue to detect the different stages of Diabetic Retinopathy

## Introduction & Problem statement 
•	Diabetics is one of the most common eye diseases among adults. Business case: the purpose of this project is to detect 5 stages of the Diabetic Retinopathy. The 5 stages are: normal, mild, moderate, severe and proliferative. 
## Data
•	It was collected from Kaggle and we only used the train data set for this project. We have about 3662 images.
•	Exploratory analysis: data is unbalanced. There is more data with not DR (normal – no disease), less images with mild and proliferative and severe. When we look at DR and not DR, the data is pretty balanced. 
•	 Feature engineering: We remove the color of the pictures: resize the pictures into 225x225 and then we add weights GaussianBlur to have a better visualization with the bold vessels. Finally, we applied T-SNE and PCA to see the distribution of the data and how data groups together/ cluster without labels. We can see that there is a distinct difference between images with DR and NO DR. However, within different stages of DR, it gets more convoluted and more difficult to distinguish the clusters. We expect our machine learning and neural networks to have a better prediction with NO DR.
## Modeling – MACHINE LEANRING
•	Before applying machine learning models, we flatten the data and standardize it and apply PCA to dimension reduction of the data. We keep 750 components out of 2563 with more than 90% of variance. 
•	We split the train and test data into 70/30 and we smote the data to balance each group (all of them).
•	We use 3 machine learning models: logistic regression classification, random forest classification and ADA Boost classifier – random search. The best results we got were from Random forest with 0.55 accuracy for train and 0.59 accuracy for test. The is underfit in this model which is the opositive to logistic regression and Ada Boost, booth overfitting the data, especially logistic regression. For the confusion matrix (Random Forest) – the model perform better with No DR class and we expected earlier. 
## Modeling – CNN
•	We used convolution neural network because it is known to be one of the best models for image classification – it is not a fully connected model meaning we have less parameters that fully connected allowing faster computation. Basically, CNN takes an input image, assign importance (weights and biases) to various objects in the image and differentiating them. In our example, we take each image of the eyeball, build a CNN with layers such as dense (number of filters we reduce of the input image to), maxpooling (down sample the data) – extract the dominant values, padding to augment the data, dropout to help prevent overfitting, with ReLU activation function and we finished by flattening the data (converting matrices into a single vector) before applying softmax to help us classifying the images. 
•	In total, we used 15 layers for this model, and we perform a split of 80/20 for the train leaving a 20% holdout for the test data set. We achieve accuracy for train and test (72.3% and 73.7%). With these numbers we can see there is a bit of underfitting. We set the batch size of 40 with epochs = 10. The train accuracy starts very low and it increases drastically by epoch 2 which is similar to loss value (around 3). 
•	Then we used the same model with images augmentation. Some of the changes on the images are flips, width, height and zoom. In the model we also add early stopping, meaning that if the validation loss does not improve (let’s say, after 3 epochs), the model can just store the best result.  In this example, we set batch size 50 and 5 more epochs getting accuracy of (63,3% for train, 62,7% for test). These results show a bit of underfitting.
•	We tried one last model for CNN with the same parameters, same data augmentation and early stopping adding test data augmentation. This technique is used to mitigate errors like poor contracts in pictures. Where we predict the classes. Using TTA, we are able to transform each image of the test data set several times, let’s say (4 images) then take the average of the predictions (probability of an image belonging to a class) to determine the final label (highest one wins). For this one, accuracy for test and train is and 
## Transfer Learning 
•	We decided to use transfer learning because we have a pretrained model and build architecture. We can just add other layers on the top of it and it helps to speed up the model training process and accelerate the results. We do not need to build a total model from scratch! 
•	For this project we used ResNet50 and EfficiNetB0. These models have different architecture, one has bottleneck (efficinet) and the other one is residual blocks (RESENET). These two models are trained in more than 1 million from image net database. ResNet has 50 layers and classify images into 1000 object categories while efficient contains less parameters than other models with fewer channels and depth separable convolution.
•	Using Reset50, we added five layers on the top of the model, we freeze the model using weights and only training the top five layers. Then, we unfreeze the layers in the base network and we jointly trained layers and the part we added. During the training process we use early stopping to regularize epochs and reduce learning rate with reduce plateu function.  
•	For the results, the loss is much lower than CNN model (starting 1.6 and final one is 0.4) and we are able to improve accuracy from 62% to 84%. As we can see in the confusion matrix, we are able to classify very well No DR and Moderate. Severe and proliferate are still not very well classified, even though it improved compared to the CNN and ML models. 
•	We perform the same for efficient and the only different is the base model. The results for this one are better and faster than RESENET50 because it has less parameters.
## Findings
•	We used machine learning algorithms, CNN and Transfer learning. Overall using machine learning we got to 50% accuracy, CNN about 73% and transfer learning about 84%. We are able to predict very well with no DR and moderate classes. There is more misclassification in severe and proliferate. 
## Future work 
•	We can use additional dataset from earlier computations, and we can try to tune other parameters such as dropout and try to use different activation functions and loss functions. 
•	In regards to image prepossessing, we can try to remove the black area in order to better classify images.
•	Finally, we can also try different things for the data augmentation process.

