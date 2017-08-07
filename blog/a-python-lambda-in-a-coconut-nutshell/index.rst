.. title: A Python lambda in a Coconut (nutshell)
.. slug: a-python-lambda-in-a-coconut-nutshell
.. date: 2017-08-06 13:39:09 UTC-04:00
.. tags: coconut
.. category: python fp
.. link: 
.. description: Python Coconut Lambdas
.. type: text

I recently Googled for ways to destructure a Python dict. I found this code on stackoverflow:

.. code-block:: python

   pluck = lambda dict, *args: (dict[arg] for arg in args)

.. note:: https://stackoverflow.com/questions/2955412/python-destructuring-bind-dictionary-contents

From perusing the Coconut documentation, I remembered that Coconut has a special syntax for lambda. So I converted the pluck function to use the Coconut syntax. This is what it looks like now:

.. code-block:: python

   pluck = (dict, *args) -> (dict[arg] for arg in args)

.. note:: http://coconut-lang.org/

.. note:: http://coconut.readthedocs.io/en/master/DOCS.html#lambdas

You will notice that the lambda is removed in favor of arrow (->). The placement also changed with the positioning of the arrow coming after the parameters dict and star args. The way I think about the operation of this function is that I am going to give the function a dict and any number of arguments. The expression inside the function loops through the args and yield each value associated with the arg from the dict. Each yielded value is assigned to the respective variable on the left. 

You might be wondering what the python code looks like after compilation. To compile the file_name.coco file you would run the following command:

.. code-block:: shell

   $ coconut file_name.coco --target 36 --mypy

I pass the file to the Coconut compiler. In my case, I am targeting the Python 3.6.1 interpreter. Although MyPy isn't particularly useful for this code, I also ask Coconut to run the code against the MyPy type checker. The Python that Coconut outputs unsurprisingly looks like this:

.. code-block:: python

   pluck = lambda dict, *args: (dict[arg] for arg in args)

.. note:: http://mypy-lang.org/

Now we have come full circle to our original code snippet.

This is the usage of the function:

.. code-block:: python

   upload_data = {}
   upload_data["name"] = "example"
   upload_data["description"] = "this is a demo"
   upload_data["file_name"] = "demo.png"
   name, description, file_name = pluck(upload_data, 'name', 'description', 'file_name')

I find this syntax more elegant. Often times with syntax small things add up to make something nicer. This is one way that Coconut makes it pleasant for me to use Python.

