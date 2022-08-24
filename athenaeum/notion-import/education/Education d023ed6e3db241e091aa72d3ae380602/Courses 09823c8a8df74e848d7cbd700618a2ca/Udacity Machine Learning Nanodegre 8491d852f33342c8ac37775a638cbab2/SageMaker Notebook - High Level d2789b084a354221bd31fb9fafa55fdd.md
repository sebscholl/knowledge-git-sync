# SageMaker Notebook - High Level

**High Level Overview**

The flow includes:

1. Loading and cleaning data
2. Breaking data into training, validation, and testing sets
    1. If using SageMaker, upload that data as an artifact to s3
3. Initializing the estimator or model
4. Giving the model the data location.
5. Fitting the model
6. Testing the Model

**Training Data**

When a training job is constructed using SageMaker, a container is executed which performs the training operation. This container is given access to data that is stored in S3. This means that we need to upload the data we want to use for training to S3. In addition, when we perform a batch transform job, SageMaker expects the input data to be stored on S3. We can use the SageMaker API to do this and hide some of the details.

**Example of taking Data from Raw to Upload for SageMaker**

```python
# First we package up the input data and the target variable (the median value) as pandas dataframes. This
# will make saving the data to a file a little easier later on.
print('Features: ', boston.feature_names)

# Our data represents the values for all features while the target is the labels/predictions.
print('Data: ', len(boston.data))
print('Target: ', len(boston.target))

# Use pandas to create dataframes of the data
# Data frames structure the data with columns and rows
X_bos_pd = pd.DataFrame(boston.data, columns=boston.feature_names)
Y_bos_pd = pd.DataFrame(boston.target)

print('X:', X_bos_pd)
print('Y:', Y_bos_pd)

# We split the dataset into 2/3 training and 1/3 testing sets using the sklearn.model_selection.train_test_split method.
X_train, X_test, Y_train, Y_test = sklearn.model_selection.train_test_split(X_bos_pd, Y_bos_pd, test_size=0.33)

# Then we split the training set further into 2/3 training and 1/3 validation sets using same method.
X_train, X_val, Y_train, Y_val = sklearn.model_selection.train_test_split(X_train, Y_train, test_size=0.33)

# This is our local data directory. We need to make sure that it exists.
data_dir = '../data/boston'

# We use pandas to save our test, train and validation data to csv files. Note that we make sure not to include header
# information or an index as this is required by the built in algorithms provided by Amazon. Also, for the train and
# validation data, it is assumed that the first entry in each row is the target variable.

# We convert the X_test data to a csv and save it in the data directory WITHOUT Y_test labels.
X_test.to_csv(os.path.join(data_dir, 'test.csv'), header=False, index=False)

# We convert the validation and training data sets to a csvs and add them to the data directory.
pd.concat([Y_val, X_val], axis=1).to_csv(os.path.join(data_dir, 'validation.csv'), header=False, index=False)
pd.concat([Y_train, X_train], axis=1).to_csv(os.path.join(data_dir, 'train.csv'), header=False, index=False)

# Prefix creates a subfolder in the S3 bucket that the data artifacts are being uploaded to.
prefix = 'boston-xgboost-HL'

# Once the test, train, validation files are written it's time to upload them to S3
test_location = session.upload_data(os.path.join(data_dir, 'test.csv'), key_prefix=prefix)
val_location = session.upload_data(os.path.join(data_dir, 'validation.csv'), key_prefix=prefix)
train_location = session.upload_data(os.path.join(data_dir, 'train.csv'), key_prefix=prefix)
```

**Constructing an Estimator (Using XGBoost Model)**

To construct an estimator, the object which we wish to train, we need to provide the location of a container which contains the training code. Since we are using a built in algorithm this container is provided by Amazon. However, the full name of the container is a bit lengthy and depends on the region that we are operating in. Fortunately, SageMaker provides a useful utility method called get_image_uri that constructs the image name for us.

Find list of built in algorithms here: [https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-algo-docker-registry-paths.html](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-algo-docker-registry-paths.html)

```python
# As stated above, we use this utility method to construct the image name for the training container.
container = get_image_uri(session.boto_region_name, 'xgboost')

# Now that we know which container to use, we can construct the estimator object.
xgb = sagemaker.estimator.Estimator(
		container, # The image name of the training container
    role,      # The IAM role to use (our current role in this case)
    train_instance_count=1, # The number of instances to use for training
    train_instance_type='ml.m4.xlarge', # The type of instance to use for training
    output_path='s3://{}/{}/output'.format(session.default_bucket(), prefix), # Where to save the output (the model artifacts)
    sagemaker_session=session
) # The current SageMaker session
```

**Setting Hyperparams on a Model**

Once a model is created it is time to set any model specific hyperparameters. There are quite a few that can be set when using the XGBoost algorithm, below are just a few of them. If you would like to change the hyperparameters below or modify additional ones you can find additional information on the [XGBoost hyperparameter page](https://docs.aws.amazon.com/sagemaker/latest/dg/xgboost_hyperparameters.html).

```python
xgb.set_hyperparameters(
    max_depth=5,
    eta=0.2,
    gamma=4,
    min_child_weight=6,
    subsample=0.8,
    objective='reg:linear',
    early_stopping_rounds=10,
    num_round=200
)
```

**Kicking off Training**

Once:

- [ ]  Data is imported
- [ ]  Data is formatted
- [ ]  Data is save and uploaded to s3 bucket
- [ ]  Estimator (model) is initialized
- [ ]  Hyperparameters are set

It's time to kick off training.

```python
# This is a wrapper around the location of our train and validation data, to make sure that SageMaker
# knows our data is in csv format.
s3_input_train = sagemaker.s3_input(s3_data=train_location, content_type='csv')
s3_input_validation = sagemaker.s3_input(s3_data=val_location, content_type='csv')

xgb.fit({'train': s3_input_train, 'validation': s3_input_validation})
```

Once training is done we Test

**Testing the Model**

Batch Transform is a convenient way to perform inference on a large dataset in a way that is not realtime. That is, we don't necessarily need to use our model's results immediately and instead we can peform inference on a large number of samples. An example of this in industry might be peforming an end of month report. This method of inference can also be useful to us as it means to can perform inference on our entire test set.

To perform a Batch Transformation we need to first create a transformer objects from our trained estimator object

```python
# Using an instance count of 1 and an instance type of ml.m4.xlarge
# should be more than enough.
xgb_transformer = xgb.transformer(instance_count = 1, instance_type = 'ml.m4.xlarge')

# Start the transform job. Make sure to specify the content type and the split type of the test data.
xgb_transformer.transform(test_location, content_type = 'text/csv', split_type = 'Line')

# Currently the transform job is running but it is doing so in the background. Since we wish to wait until the transform job is done and we would like a bit of feedback we can run the wait() method.
xgb_transformer.wait()
```

**Using Model**

Now the transform job has executed and the result, the estimated sentiment of each review, has been saved on S3. Since we would rather work on this file locally we can perform a bit of notebook magic to copy the file to the data_dir.

```python
!aws s3 cp --recursive $xgb_transformer.output_path $data_dir
```

The last step is now to read in the output from our model, convert the output to something a little more usable, in this case we want the sentiment to be either 1 (positive) or 0 (negative), and then compare to the ground truth labels.

```python
predictions = pd.read_csv(os.path.join(data_dir, 'test.csv.out'), header=None)
predictions = [round(num) for num in predictions.squeeze().values]

from sklearn.metrics import accuracy_score
accuracy_score(test_y, predictions)
```