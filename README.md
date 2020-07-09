# Rapids.ai examples on SageMaker

This repository contains examples of running SageMaker notebook with the rapidsai kernel for data science at scale and rapid prototyping. It also contains example of using SageMaker processing with a rapids.ai custom docker image.


## Setup instructions for creating a rapidsai kernel for your SageMaker notebook.

- Use a P instance for your SageMaker Notebook.
- Once the SageMaker notebook instance is running, start a shell from the launcher and enter the following commands.


```
source /home/ec2-user/anaconda3/etc/profile.d/conda.sh
echo "Starting conda create command for rapidsai env"
conda create --name rapidsai python=3.6
conda activate rapidsai
conda install -c rapidsai -c nvidia -c conda-forge -c blazingsql/label/cuda10.2 -c blazingsql -c defaults -c pyviz rapids=0.14 python=3.6 cudatoolkit=10.2 blazingsql bokeh holoviews -y
pip install sagemaker
echo "Installing Jupyter kernel for rapidsai"
python -m ipykernel install --name 'rapidsai' --user
```

Create a new notebook and pick the conda_rapidsai kernel.

"Readme.md" 49L, 1639C
