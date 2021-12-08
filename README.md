# ECG_Classification
Machine Learning project to classify patients using ECG-data.

This project was done in the course Advanced Machine Learning at ETH. The task was to classify patients into 4 classes. The data provided was ecg-signals of different lengths sampled at 300hz. Two datasets was received, one set with labels and then one set without labels. The task was to produce labels for the unlabeled set which was then to be handed. 

Major challenges with the project:
* Feature extraction
* Model selection

Feature extraction
As the raw ECG-signals were of different lengths and had different offsets regarding the heartbeats they were unfit to push through a ML-model as is and thus some feature extraction was needed. Three approaches was used to find in total approximately 100 features about the signals. 

First, features to describe the heartbeat was used, a regular heartbeat has five distinct peaks (called p,q,r,s,t). By separating the ecg-signals into heartbeats and finding these five peaks for each heartbeat different features like the median, mean, variance for each peak was used as features. Furthermore, the distance between peaks was thought to give information about irregularities in the heartbeat, why statistical measures of these distances also were used as features. These measures were found with not too much complexity and was also quite easy to understand, furthermore, the theory investigated told us that these kind of measures is usually studied when it comes to finding heart disease. Downside: Took hours to compute, upside: only had to compute it once.

Second, the heart rate was studied and it was considered that measures about it could give much information to the classification task. With the use of a smart library different measures about the heart rate was extracted and use as features. A challenge here was that the information about heart rate was very domain technical and it was hard to understand many of the measurements, decreasing the transparency of the model.

Third, general measures to describe time-series signals, like autocorrelation and the spectral density was used. The upside here is that these methods produced comparable measures for each hearbeat which was easy to understand. The challenge however was that the methods produced very many datapoints (potential features) and it would be computationally very inefficient to use them all. This in combination with ambiguity on what information was provided by different points (e.g. different lags in the autocorr) made the feature choice here rather arbitrary. 

Lastly, a set of ML-models were trained and tuned by using cross-validation and it was found that the GBM-classifier implemented by the catboost library did a good job of classifying the data.
