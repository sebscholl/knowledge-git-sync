# Jupyter Notebooks

Last Edited: December 19, 2019 11:43 PM

# Install

# Conda install Jupiter notebook

# Launching the notebook server

To start a notebook server, enter jupyter notebook in your terminal or console. This will start the server in the directory you ran the command in. That means any notebook files will be saved in that directory. Typically you'd want to start the server in the directory where your notebooks live. However, you can navigate through your file system to where the notebooks are.

When you run the command (try it yourself!), the server home should open in your browser. By default, the notebook server runs at [http://localhost:8888](http://localhost:8888/). If you aren't familiar with this, localhost means your computer and 8888 is the port the server is communicating on. As long as the server is still running, you can always come back to it by going to [http://localhost:8888](http://localhost:8888/) in your browser.

If you start another server, it'll try to use port 8888, but since it is occupied, the new server will run on port 8889. Then, you'd connect to it at [http://localhost:8889](http://localhost:8889/). Every additional notebook server will increment the port number like this.

If you tried starting your own server, it should look something like this:

You might see some files and folders in the list here, it depends on where you started the server from.

Over on the right, you can click on "New" to create a new notebook, text file, folder, or terminal. The list under "Notebooks" shows the kernels you have installed. Here I'm running the server in a Python 3 environment, so I have a Python 3 kernel available. You might see Python 2 here. I've also installed kernels for Scala 2.10 and 2.11 which you see in the list.

The tabs at the top show *Files*, *Running*, and *Cluster*. *Files* shows all the files and folders in the current directory. Clicking on the *Running* tab will list all the currently running notebooks. From there you can manage them.

*Clusters* previously was where you'd create multiple kernels for use in parallel computing. Now that's been taken over by [ipyparallel](https://ipyparallel.readthedocs.io/en/latest/intro.html) so there isn't much to do there.

You should consider installing Notebook Conda to help manage your environments. Run the following command:

conda install nb_conda

Then if you run the notebook server from a conda environment, you'll also have access to the "Conda" tab shown below. Here you can manage your environments from within Jupyter. You can create new environments, install packages, update packages, export environments and more.

conda tab in Jupyter

Additionally, with nb_conda installed you will be able to access any of your conda environments when choosing a kernel. For example, the image below shows an example of creating a new notebook on a machine with several different conda environments:

conda environments in Jupyter

### **Shutting down Jupyter**

You can shutdown individual notebooks by marking the checkbox next to the notebook on the server home and clicking "Shutdown." Make sure you've saved your work before you do this though! Any changes since the last time you saved will be lost. You'll also need to rerun the code the next time you run the notebook.

You can shutdown the entire server by pressing control + C twice in the terminal. Again, this will immediately shutdown all the running notebooks, so make sure your work is saved!

## **Debugging in the Notebook**

With the Python kernel, you can turn on the interactive debugger using the magic command %pdb. When you cause an error, you'll be able to inspect the variables in the current namespace.

[Jupyter%20Notebooks%20248c293b937e45a69f01e8bb7aef37de/untitled](athenaeum/notion-import/education/Education%20d023ed6e3db241e091aa72d3ae380602/Coding%2045e119ddd66942a9be9c04cec752795c/Jupyter%20Notebooks%20248c293b937e45a69f01e8bb7aef37de/untitled)

Debugging in a notebook

Above you can see I tried to sum up a string which gives an error. The debugger raises the error and provides a prompt for inspecting your code.

Read more about pdb in [the documentation](https://docs.python.org/3/library/pdb.html). To quit the debugger, simply enter qin the prompt.