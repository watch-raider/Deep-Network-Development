# Object Detection - Cigars

## Summary

### Data Collection

Images were collected from web search where I tried to collate a diverse dataset of cigar images including close-up pictures, pictures with different number of cigars and even photos I had taken with my own phone which I included in the validation. 
I was more interested in testing the performance of the model my own photos as these were not professionally taken and were in a real life setting.

### Metrics

The main metrics I used to evaluate the models performance was Mean Average Precision (mAP), Precision, Recall and the loss function. 
I also used visualistion on the validation set to assess performance.

### Methodology

After collecting my dataset, I trained the trained the pre-trained YoloV8n model on it. I was originally training on 30 epochs and experimented with different parameters. 
I would the validate the model against the validation set after training. After initial training using the default parameters, the loss function was performing as expected with the error reducing as the model iterated through training but the model was acheiving suboptimal mAP of < 0.30, which indicated model required general refinments. Therefore I performed hyperparameter tuning to in order to optimise the the model's performance metrics. 
However, first I had to decide on which optimiser to use for tuning and after a few training iterations I was acheiving the best results with Stochastic gradient descent (SGD). 
The tuning performed 30 epochs on 50 iterations and created a 'best_hyperparameters.yaml' file which I could pass to my model. 
This file included slightly increasing the learning rate and augmenting the dataset by flipping random images top avoid overfitting. 
After I experimented training with different batch sizes starting with 5 and increasing it by 5 after each iteration and found the best performance with a batch size of 25. I also introduced early stopping at 20 epochs, when training on 30 epochs to avoid overfitting.

### Results

After tuning, I was able to improve mAP to > 0.50, precision > 0.80, loss reducing as expected with training and reaching < 1. The model acheived low recall results that did not improve with the number of epochs. 
When visualising, mixed results were acheived and matched the mAP results with the model making accurate predictions for only around half the validation images. 
When performing predictions on the two images taken with my personal phone, the model accurately predicted on only one of the images.

### Conclusion & Discussion

The model didn't achieve accuracy results I was hoping for which gives the indication that cigars is a difficult object for YoloV8n to perform accurate predictions on. 
One reason for this probably due to the fact is difficult to accurately annotate cigars due to their shape. When annotating the images, 
the bounding boxes would often include a lot of background and noise. The high precision shows that the model did well in not making false postive predictions. 
The suboptimal Recall results indicates the model could be missing real objects and resulted in many false negatives when making predictions. 
One way to help solve this issue would be to use more data which will be a consideration to taken in future object dection projects.
