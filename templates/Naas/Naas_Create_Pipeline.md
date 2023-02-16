<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Create_Pipeline.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Create+Pipeline:+Error+short+description">Bug report</a>

**Tags:** #naas #pipeline #jupyter #notebook #dataanalysis #workflow #streamline

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** This notebook is a guide that teaches you how to create a notebook pipeline using naas.

## Input

### Import libraries


```python
from naas.pipeline.pipeline import (
    Pipeline,
    DummyStep,
    DummyErrorStep,
    NotebookStep,
    End,
    ParallelStep,
)
```

### Setup NotebookStep
For demonstration purposes, we used the `DummyStep` to illustrate its functionality.

In order to create a pipeline, you should used the `NotebookStep()` which has three parameters:
- the name (string) of the step
- the notebook path (string) for execution
- the parameters (dictionary) that are injected through papermill in the first cell or after the cell labeled "parameters."

`NotebookStep("My Notebook", "my_notebook.ipynb")`


```python
collection = DummyStep(
    "Collection"
)  # In this step, data can be collected from various sources such as databases, APIs, or file systems.
cleaning = DummyStep(
    "Cleaning"
)  # Once the data is collected, it is often necessary to clean and preprocess it to remove any irrelevant or duplicate information. This step may involve tasks such as removing null values, correcting data formats, and standardizing column names.
transformation1 = DummyStep(
    "Transformation 1"
)  # In this step, the data is transformed into the desired format, such as a flat file or a specific data model. This may involve tasks such as aggregating data, joining multiple tables, or calculating new fields.
transformation2 = DummyStep(
    "Transformation 2"
)  # In this step, the data is transformed into the desired format, such as a flat file or a specific data model. This may involve tasks such as aggregating data, joining multiple tables, or calculating new fields.
distribution = DummyStep(
    "Distribution"
)  # In this step, the data is loaded into its final destination, such as a data warehouse, a data lake, or a specific application.
```

## Model

### Create Basic Pipeline
- Link your notebook using this syntax: `>>`
- Create ParallelStep using this syntax: `[step1, step2]`


```python
pipeline = Pipeline()

(
    pipeline
    >> collection
    >> cleaning
    >> [transformation1, transformation2]
    >> distribution
    >> End()
)

pipeline.run()
```

## Output

### Monitor your pipeline in "pipeline_executions"
When the pipeline is run, a "pipeline_executions" folder will be created in your file system. Inside this folder, you will be able to access each pipeline executions. If you use NotebookStep, executed notebooks will be stored in this folder. This allows you to easily review and analyze the results of the pipeline, and to troubleshoot any issues that may have occurred. The "pipeline_executions" folder is a valuable tool for understanding the performance of your pipeline and for making improvements to it over time.
