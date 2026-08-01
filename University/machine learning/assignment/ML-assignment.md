## 1. Accuracy, Precision, Recall, and F1-Score

Accuracy means how many predictions made by the model are correct. For example, if the model gives 90 correct answers out of 100, then the accuracy is 90%.

Precision means how many of the positive predictions are actually correct. It checks the quality of positive predictions made by the model.

Recall means how many actual positive cases the model was able to find correctly. It is important when missing a positive case is a big problem.

F1-Score is a balance between Precision and Recall. It is useful when both of them are important.

## 2. Difference Between MSE and MAE

MSE gives more punishment to large errors because it focuses more on bigger mistakes. On the other hand, MAE treats all errors more equally.

MAE is preferred when the dataset has outliers or unusual values because it is less affected by very large errors. MSE is useful when large mistakes should be penalized more strongly.

## 3. ROC-AUC

An AUC score of 0.5 means the model is performing almost like random guessing and cannot separate the classes properly.

An AUC score of 0.9 means the model is performing very well and can separate the classes correctly most of the time.

Higher AUC values usually mean better model performance.

## 4. Difference Between mAP@0.5 and mAP@[0.5:0.95]

mAP@0.5 checks whether the predicted object location is at least 50% correct compared to the real object location.

mAP@[0.5:0.95] is much stricter because it checks the model at many different levels of accuracy. It gives a more detailed and realistic evaluation of the model performance.

Because of this, mAP@[0.5:0.95] is considered harder and more reliable.

## 5. Training Accuracy = 99.5%, Validation Accuracy = 72%, Test Accuracy = 70%

This situation shows overfitting.

The model performed extremely well on training data but performed poorly on validation and test data. This means the model memorized the training data instead of learning general patterns.

Possible causes can be:

- Small dataset
    
- Too much complex model
    
- Training for too long
    
- Noisy data
    
- Lack of regularization
    

Some ways to reduce overfitting are:

- Using more data
    
- Applying data augmentation
    
- Reducing model complexity
    
- Using dropout or regularization
    
- Using early stopping
    

## 6. Symptoms of Overfitting and Underfitting

### Overfitting

- Very high training accuracy
    
- Low validation and test accuracy
    
- Good performance on training data only
    
- Poor performance on new data
    

### Underfitting

- Low training accuracy
    
- Low validation accuracy
    
- Model fails to learn patterns properly
    
- Poor performance on both training and testing data
    
