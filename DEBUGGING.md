Troubleshooting
===============

Watson Studio
--------------

* Make sure you follow the instructions as per the documentation to create the AutoAI service.
* Ingest the dataset as specified.
* Do not stop the AutoAI process abruptly after it has started.
* Create a new experiment if you want to make changes to the settings.

Jupyter Notebooks
-----------------

* Make sure the pip install ran correctly. You might need to restart the kernel and run the cells from the top after the pip install runs the first time.
* Many of the cells rely on variables that are set in earlier cells. Some of these are cleared in later cells. Start over at the top when troubleshooting.
* Many of the cells rely on service credentials from Bluemix that are set in earlier cells. Make sure to add your service credentials correctly. Run the cells from top down and evaluate the outcome.