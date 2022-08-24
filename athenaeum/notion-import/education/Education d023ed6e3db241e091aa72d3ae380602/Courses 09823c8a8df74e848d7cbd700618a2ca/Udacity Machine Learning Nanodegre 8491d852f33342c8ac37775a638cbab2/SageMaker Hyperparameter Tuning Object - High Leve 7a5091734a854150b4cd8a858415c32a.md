# SageMaker Hyperparameter Tuning Object - High Level

Now that we have our estimator object completely set up, it is time to create the hyperparameter tuner. To do this we need to construct a new object which contains each of the parameters we want SageMaker to tune. In this case, we wish to find the best values for the `max_depth`, `eta`, `min_child_weight`, `subsample`, and `gamma` parameters. Note that for each parameter that we want SageMaker to tune we need to specify both the *type* of the parameter and the *range* of values that parameter may take on.

In addition, we specify the *number* of models to construct (`max_jobs`) and the number of those that can be trained in parallel (`max_parallel_jobs`). In the cell below we have chosen to train `20` models, of which we ask that SageMaker train `3` at a time in parallel. Note that this results in a total of `20` training jobs being executed which can take some time, in this case almost a half hour. With more complicated models this can take even longer so be aware!

```python
from sagemaker.tuner import IntegerParameter, ContinuousParameter, HyperparameterTuner

xgb_hyperparameter_tuner = HyperparameterTuner(
	estimator = xgb, # The estimator object to use as the basis for the training jobs.
	objective_metric_name = 'validation:rmse', # The metric used to compare trained models.
	objective_type = 'Minimize', # Whether we wish to minimize or maximize the metric.
	max_jobs = 20, # The total number of models to train
	max_parallel_jobs = 3, # The number of models to train in parallel
	hyperparameter_ranges = {
	    'max_depth': IntegerParameter(3, 12),
	    'eta'      : ContinuousParameter(0.05, 0.5),
	    'min_child_weight': IntegerParameter(2, 8),
	    'subsample': ContinuousParameter(0.5, 0.9),
	    'gamma': ContinuousParameter(0, 10),
})
```

Now that we have our hyperparameter tuner object completely set up, it is time to train it. To do this we make sure that SageMaker knows our input data is in csv format and then execute the fit method.

```python
# This is a wrapper around the location of our train and validation data, to make sure that SageMaker
# knows our data is in csv format.
s3_input_train = sagemaker.s3_input(s3_data=train_location, content_type='csv')
s3_input_validation = sagemaker.s3_input(s3_data=val_location, content_type='csv')

xgb_hyperparameter_tuner.fit({'train': s3_input_train, 'validation': s3_input_validation})
```

As in many of the examples we have seen so far, the fit() method takes care of setting up and fitting a number of different models, each with different hyperparameters. If we wish to wait for this process to finish, we can call the wait() method.

```python
xgb_hyperparameter_tuner.wait()
```

Once the hyperamater tuner has finished, we can retrieve information about the best performing model.

```python
xgb_hyperparameter_tuner.best_training_job()
```

In addition, since we'd like to set up a batch transform job to test the best model, we can construct a new estimator object from the results of the best training job. The xgb_attached object below can now be used as though we constructed an estimator with the best performing hyperparameters and then fit it to our training data.

```python
xgb_attached = sagemaker.estimator.Estimator.attach(xgb_hyperparameter_tuner.best_training_job())
```