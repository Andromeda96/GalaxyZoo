## Galaxy image classification using boosting decision trees

![Image result for galaxy classification](https://github.com/whywww/GalaxyZoo/blob/master/Fig1.png)

_Figure 1 HUBBER'S CLASSIFICATION SYSTEM_

### Problem Description

Galaxies are made up of millions of stars like the Sun. Different initial conditions and history will result in different appearances of the Galaxies --- they may be elliptical or spiral, concentrated or discrete, red or blue, convex or disk. A better classification for the galaxies is important for the astronomers to learn the formation of galaxy. The Sloan Digital Sky Survey (SDSS) is taking photos for millions of galaxies. We plan to use the data from SDSS to design a machine learning algorithm to classify the galaxies.

#### Dataset description

Galaxy Zoo 2 dataset [1] consists of 61578 training and 79975 testing JPG images of galaxies adapted from SDSS, which is originally of FITS format. Each image is labeled by volunteers on 11 decision tree (GZ2) questions with different choice responses, see Figure 2. The response results are presented in the form of possibilities for each choice. The galaxies can then be classified by setting a certain threshold for the debiased likelihoods of the responses.  

![DecisionTreeImage](https://github.com/whywww/GalaxyZoo/blob/master/Fig2.png)

_Figure 2 Flowchart of classification tasks for GZ2, beginning at the top center. Tasks are color-coded by their relative depths in the decision tree._

### Related Works

Shamir [3] used the same dataset for classification of spiral, elliptical and edge-on galaxies achieved 90 percent of accuracy using WND-CHARM algorithm, which was generalized from cell and tissue analysis. The major downside of this algorithm is high computational complexity compared to another algorithm introduced in [4], the Gini coefficient, which achieved 55 percent accuracy on the same multi-class task but 77 percent on binary classification task.

### Feature Extraction

#### Features

1. Pixel color 

2. HoG (Histogram of oriented Gradients)

3. Eccentricity

4. Radius for 90% luminosity

#### Feature processing

The pixel and HoG features may include irrelevant features that run the risk of swamping the classifiers. Therefore, we use PCA for dimension reduction to select the most representative features. Also, we include components generated from LDA along with PCA features. And then normalize the data to give all features a standard deviation of 0.5 and a mean of 0.

### Machine Learning Algorithm

General idea: Boosting presumes users have a base or weak learning algorithm, given labeled training examples, they may produce a base or weak classifier. So, the goal is to improve the performance of the weak learning algorithm while treating it as a “black box”. However, it is not simply called repeatedly, but required to work slightly better than the random guessing on the train set and infer something new about the structure or the feature of the data each time it does classification. 

Using Adaboost: AdaBoost classifier builds a strong classifier by combining multiple poorly performing classifiers so that you will get high accuracy strong classifier. The basic concept behind Adaboost is to set the weights of classifiers and training the data sample in each iteration such that it ensures the accurate predictions of unusual observations. The classifier should be trained interactively on various weighed training examples. In each iteration, it tries to provide an excellent fit for these examples by minimizing training error.

![img](https://github.com/whywww/GalaxyZoo/blob/master/Fig3.png)

_Figure 3 Sturcture of Algorithm, individual classifier vote and final prediction label returned that performs majority voting._

### Further study:

1)To get a sense of Boosting’s performance overall, we can compare it with other methods on our datasets.

2)We can try different base learning algorithms, like decision stumps, C4.5, etc. 

3)Try different ways in which weights can be used by the base learner. 

In some case, base learner cannot easily be modified to handle the given weights directly or in 

other cases, algorithms can be modified to directly use the given example weights. 

4) We can gradually study the algorithms following the path, 1)Adaboost, 2)Gradient tree boosting 3)XGBoost.

 

_Reference:_

[1] Willett, Kyle W. et al. “Galaxy Zoo 2: Detailed Morphological Classifications for 304 122 Galaxies from the Sloan Digital Sky Survey.” Monthly Notices of the Royal Astronomical Society 435.4 (2013): 2835–2860. Crossref. Web.

[2] L. du Buisson, N. Sivanandam, Bruce A. Bassett, M. Smith, Machine learning classification of SDSS transient survey images, Monthly Notices of the Royal Astronomical Society, Volume 454, Issue 2, 01 December 2015, Pages 2026–2038, https://doi.org/10.1093/mnras/stv2041

[3] Shamir, Lior. "Automatic morphological classification of galaxy images." Monthly Notices of the Royal Astronomical Society 399.3 (2009): 1367-1372.

[4] Abraham, Roberto G., Sidney Van Den Bergh, and Preethi Nair. "A new approach to galaxy morphology. I. Analysis of the Sloan Digital Sky Survey early data release." The Astrophysical Journal 588.1 (2003): 218.

[5] [Schapire, R.](file:///insight/search%3fq=Robert E. Schapire) and [Freund, Y.](file:///insight/search%3fq=Yoav Freund) (2013), "Boosting: Foundations and Algorithms", [Kybernetes](https://www.emerald.com/insight/publication/issn/0368-492X), Vol. 42 No. 1, pp. 164-166. 

 
