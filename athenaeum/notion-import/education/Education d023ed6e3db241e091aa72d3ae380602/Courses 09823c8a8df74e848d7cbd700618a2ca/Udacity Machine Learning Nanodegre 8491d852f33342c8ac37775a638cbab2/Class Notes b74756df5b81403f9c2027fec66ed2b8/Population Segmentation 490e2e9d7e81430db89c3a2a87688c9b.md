# Population Segmentation

Class: Machine Learning Nanodegree
Created: September 8, 2021 11:41 AM
Reviewed: No
Type: Online Course
URL: https://classroom.udacity.com/nanodegrees/nd009t/parts/670d5990-4694-47a7-887d-c84710e15a45/modules/b242580a-f3b5-4f56-8959-56a2a95e64c3/lessons/53bc0d8c-18d7-4ba4-8ea8-dc661bd7fe0a/concepts/e94f2703-3a5b-47a6-b7c2-b28fa6c7f875
tags: K-means clustering, Population segmentation, Supervised learning, Unsupervised learning

### Supervised Learning

Supervised learning means that the training data is made of existing data (image, video, audio, text, numbers) with corresponding class labels (ground truth).

The algorithm is then supplied a list of possible labels to select from, and the goal of the model is to as accurately as possible predict the appropriate label for the given data.

The models quality is judged by its level of accuracy in predicting true labels given data it hasn't seen before.

### Unsupervised Learning

Unsupervised learning relies on data clustering using the perceived patterns it finds in the data.

### Model Design

Models must consider the level of detail required to complete their given task. For example, an image classifier that recognizes vehicles doesn't need to know the car model. Whereas a car model classifier would. 

This comes down to data labeling, which is extremely human intensive. Data labeling can be augmented by Active Learning Models, which rely on a smaller input of human set labels to then infer their own labeling.

# K-Means Clustering

In k-means clustering you're using an unsupervised model to perform group clustering on a given data set. Each data-point is expected to provide n-dimensions and then the `k` represents the number of clusters that you wish to segment the data into (also known as *Centroids*).

The algorithm finds the center-point of each cluster by calculating the mean of all the points within the defined space. This process then repeats to the point of convergence, until 1) a predetermined number of iterations have occurred, or 2) the change in distance between a new and old center point mean value is less than a predetermined threshold.

### **Data Dimensionality**

One thing to note is that it’s often easiest to form clusters when you have low-dimensional data. For example, it can be difficult, and often noisy, to get good clusters from data that has over 100 features. In high-dimensional cases, there is often a dimensionality reduction step that takes place *before* data is analyzed by a clustering algorithm. We’ll discuss PCA as a dimensionality reduction technique in the practical code example, later.

> P**rincipal Component Analysis (PCA)** reduces the dimensionality of the original data.
> 

### **Machine Learning Workflow for Population Segmentation**

To implement population segmentation, you'll go through a number of steps:

- Data loading and exploration
- Data cleaning and pre-processing
- Dimensionality reduction with PCA
- Feature engineering and data transformation
- Clustering transformed data with k-means
- Extracting trained model attributes and visualizing k clusters

The population segmentation Jupyter Notebook is in this Sagemaker Instance [https://ml-case-studies-wzra.notebook.us-east-1.sagemaker.aws/notebooks/ML_SageMaker_Studies/Population_Segmentation/Pop_Segmentation_Exercise.ipynb#](https://ml-case-studies-wzra.notebook.us-east-1.sagemaker.aws/notebooks/ML_SageMaker_Studies/Population_Segmentation/Pop_Segmentation_Exercise.ipynb#) **MAKE SURE SAGEMAKER IS RUNNING IF THE LINK IS DEAD.**

P**rincipal Component Analysis (PCA)** reduces the dimensionality of the original data. Sagemaker provides its own model for helping with this. 

To create a PCA model, use the built-in SageMaker resource. A SageMaker estimator requires a number of parameters to be specified; these define the type of training instance to use and the model hyperparameters. A PCA model requires the following constructor arguments:

- role: The IAM role, which was specified, above.
- train_instance_count: The number of training instances (typically, 1).
- train_instance_type: The type of SageMaker instance for training.
- num_components: An integer that defines the number of PCA components to produce.
- sagemaker_session: The session used to train on SageMaker.

Documentation on the PCA model can be found [here](http://sagemaker.readthedocs.io/en/latest/pca.html).

Below, I first specify where to save the model training data, the `output_path`.

```python
from sagemaker import get_execution_role

session = sagemaker.Session() # store the current SageMaker session

# get IAM role
role = get_execution_role()
print(role)

# get default bucket
bucket_name = session.default_bucket()
print(bucket_name)
print()

# define location to store model artifacts
prefix = 'counties'

output_path='s3://{}/{}/'.format(bucket_name, prefix)

print('Training artifacts will be uploaded to: {}'.format(output_path))

# define a PCA model
from sagemaker import PCA

# this is current features - 1
# you'll select only a portion of these to use, later
N_COMPONENTS=33

pca_SM = PCA(role=role,
             train_instance_count=1,
             train_instance_type='ml.c4.xlarge',
             output_path=output_path, # specified, above
             num_components=N_COMPONENTS, 
             sagemaker_session=session)
```