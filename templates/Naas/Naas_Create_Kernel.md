<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Create_Kernel.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/Open_in_Naas_Lab.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=Naas+-+Create+Kernel:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #naas #ipython #conda #kernel

**Author:** [Maxime Jublou](https://www.linkedin.com/in/maximejublou)

**Description:** This Jupyter Notebook will enable you to establish a new IPython Kernel that you can customize, allowing you to install any desired tools. This kernel, once created, can be selected to run your notebooks and can be used even in a production environment.

## Input

### Parameters


```python
KERNEL_NAME = "my-new-kernel"  # This is the name of the Kernel you want to create.

# specify your requirements here.
REQUIREMENTS = """

"""
```

## Model

### Create script to create the kernel.


```python
script = f"""#!/usr/bin/env bash

# Make the script exit on error.
set -e

echo "🛠️ Removing kernel and conda env if it already exists"

# Remove kernel and conda env if it already exists
jupyter kernelspec remove -f {KERNEL_NAME} || true
rm -rf /home/ftp/__naas_custom_kernels__/{KERNEL_NAME} || true

echo "✅ Cleaning done"

# Create directory that will store our kernels
mkdir -p /home/ftp/__naas_custom_kernels__

echo "✅ '/home/ftp/__naas_custom_kernels__' directory created"

echo "🛠️ Creating conda env"

# Create conda env
conda create -p /home/ftp/__naas_custom_kernels__/{KERNEL_NAME} --yes

echo "✅ Conda env created"

# Init conda env with bash and load it
conda init bash
source /home/ftp/.bashrc
conda activate /home/ftp/__naas_custom_kernels__/{KERNEL_NAME}

echo "✅ Conda env loaded"

echo "🛠️ Installing ipykernel to the new conda env"

# Install ipykernel to be able to create a new kernel.
conda install --yes -c anaconda ipykernel

echo "✅ ipykernel installed"

echo "🛠️ Creating new kernel from conda env"

# Create the new kernel.
python -m ipykernel install --name {KERNEL_NAME} --sys-prefix

echo "✅ Kernel created"

echo "🛠️ Installing kernel into JupyterLab" 

# Install newly created kernel.
jupyter kernelspec install --user /home/ftp/__naas_custom_kernels__/{KERNEL_NAME}/share/jupyter/kernels/{KERNEL_NAME}

echo "✅ Kernel installed"

"""

# Write script to filesystem.
with open("kernel_create.sh", "w") as f:
    f.write(script)
```

### Execute kernel_create.sh script


```python
%%time

!bash ./kernel_create.sh
```

<p style="background-color:coral;padding:10px;text-align:center;font-size:16px;" >💡 This script usually takes around 10 minutes to complete, be patient.</p>

### Create script to install requirements into the new kernel


```python
install_requirements_script = f"""#!/usr/bin/env bash

# Make the script exit on error.
set -e

source /home/ftp/.bashrc
conda activate /home/ftp/__naas_custom_kernels__/{KERNEL_NAME}

echo "✅ Conda env activated"

pip install -r kernel_requirements.txt

echo "✅ Requirements installed in the kernel"
"""

# Write script to filesystem.
with open("install_requirements.sh", "w") as f:
    f.write(install_requirements_script)
```

### Write requirements to filesystem


```python
with open("kernel_requirements.txt", "w") as f:
    f.write(REQUIREMENTS)
```

### Install requirements


```python
%%time

!bash ./install_requirements.sh
```

<p style="background-color:coral;padding:10px;text-align:center;font-size:16px;" >💡 This script can take a long time based on your requirements.</p>

## Output

### Listing installed kernel


```python
kernels = !jupyter kernelspec list | awk '{ print $1 }'
assert KERNEL_NAME in kernels
print(f'✅ Kernel {KERNEL_NAME} created')
```

<p style="background-color:MediumSeaGreen;padding:10px;text-align:center;font-size:16px;"> 🎉 Your new kernel is all set 👏</p>
