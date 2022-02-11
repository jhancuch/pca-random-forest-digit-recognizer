# EDA of MNIST Digit Data and Building Random Forest and K-Means Models Utilizing PCA

The research question of interest is the predict the hand written digit correctly. This has applications in automatic mail sorting or identifying forms based upon the form number such as tax forms and U.S. government standard form series. 

The code can be run interactively through a [Google Colab Notebook]().

## Research design and modeling methods
I utilize an 80/20 train/validate split to ensure the models I build are not overfitting prior to generating predictions using the test set. I first generate a random forest classifier model, then a random forest classifier model using principal component analysis in the preprocessing stage, and then finally a K-Means classifier. I then fit the model using cross validation (k=5) before testing the final model on a validation set to ensure the model did not overfit to the training set.

Through EDA, I discover that it is a ver clean dataset with no nulls and the dependent variable classes are relatively balanced (ranging from 9% of the total to 11% of the total).

It will be interesting to see how the PCA processed classifier performs versus the non-PCA processed classifier. While the PCA does reduce dimensionality and thus increases the speed of the training, it does has some information loss. We set our information loss at 5% and it will be interesting to see how this transfers over to the test set. For the K-Means clustering, it will be interesting to see how many clusters there are. While there could be just 10, potential there could be more since people have different handwriting styles.

## Results and evaluation
| Metric | Random Forest | PCA Random Forest | K-Means |
|---     | ---           | ---               | ---     |
| CV Accuracy Mean | 0.96 | 0.93 | NA |
| Validation Accuracy | 0.97 | 0.93 | 0.85 |
| Test Accuracy | 0.97 | 0.93 | 0.85 |

Random Forest without and principal component analysis is by far the best model with a test accuracy of 97 percent compared to 93 percent for the PCA random forest and 85 percent for the K-means. The 5% reduction in information through PCA resulted in a 4% drop in test accuracy. While this should have sped up the model, instead it took 54 seconds compared to just the 16 seconds for the stand alone random forest model. This could be due to another program on my machine running at the same time and should be investigated. But at face value, just the random forest model has a better accuracy and lower computation time. We find through the K-means validation that k=390 is the optimal k. This shows there are a lot of different ways for individuals to write a single digit. However, k-means appeared to struggle to successfully cluster edge cases such as 4 and 9 and 3 and 8.

## Discusion
If i were to deploy one of these three models, it would be the random forest due to its high accuracy. However, prior to deployment, I would need to test the actual computation time again for both the random forest model and the pca random forest model. I originally used %%time which just computes the time for a single run. However, by using timeit%% instead, it conducts 1000 iterations and computes the mean and standard deviation which would give us a much better sense of what the actual population stastitic is.
