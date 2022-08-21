# Conda [Anaconda] Environment Mangement CLI

Last Edited: December 19, 2019 11:43 PM

## **Saving and loading environments**

A really useful feature is sharing environments so others can install all the packages used in your code, with the correct versions. You can save the packages to a [YAML](http://www.yaml.org/) file with conda env export > environment.yaml. The first part conda env export writes out all the packages in the environment, including the Python version.

Above you can see the name of the environment and all the dependencies (along with versions) are listed. The second part of the export command, > environment.yaml writes the exported text to a YAML file environment.yaml. This file can now be shared and others will be able to create the same environment you used for the project.

To create an environment from an environment file use conda env create -f environment.yaml. This will create a new environment with the same name listed in environment.yaml.

## **Listing environments**

If you forget what your environments are named (happens to me sometimes), use conda env list to list out all the environments you've created. You should see a list of environments, there will be an asterisk next to the environment you're currently in. The default environment, the environment used when you aren't in one, is called root.

## **Removing environments**

If there are environments you don't use anymore, conda env remove -n env_name will remove the specified environment (here, named env_name).

## **Sharing environments**

When sharing your code on GitHub, it's good practice to make an environment file and include it in the repository. This will make it easier for people to install all the dependencies for your code. I also usually include a pip requirements.txt file using pip freeze ([learn more here](https://pip.pypa.io/en/stable/reference/pip_freeze/)) for people not using conda.