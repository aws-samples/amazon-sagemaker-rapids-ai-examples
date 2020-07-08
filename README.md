# amazon-sagemaker-rapidsai

This repository contains examples of running SageMaker notebook with the rapidsai kernel for data science at scale and rapid prototyping. It also contains example of using SageMaker processing with a rapids.ai custom docker image.

You can find more examples of rapids.ai notebook here:
https://github.com/rapidsai/notebooks-contrib

## Setup instructions for creating a rapidsai kernel for your SageMaker notebook.


#### In Amazon SageMaker console, create a lifecycle configuration named `rapidsai`
For `Create notebook` script, enter the following

```
#!/bin/bash
set -e
echo "Updating conda"
conda update -n base -c defaults conda -y
conda update --all -y
echo "Starting conda create command for rapidsai env"
conda create -mqyp /home/ec2-user/SageMaker/.env/rapidsai -c rapidsai -c nvidia -c conda-forge -c defaults rapids=0.13 python=3.6 s3fs ipykernel matplotlib=3.1.3 statsmodels=0.11.0
source activate /home/ec2-user/SageMaker/.env/rapidsai
echo "Installing Jupyter kernel for rapidsai"
python -m ipykernel install --name 'rapidsai' --user
echo "Finished installing rapidsai conda env"
rm /home/ec2-user/SageMaker/.create-notebook
echo "Exiting install script"
```


For `Start notebook` script, enter the following

```
#!/bin/bash
set -e

echo "Starting on Start script"

sudo -i -u ec2-user bash << EOF
if [[ -f /home/ec2-user/SageMaker/.create-notebook ]]; then
    echo "Skipping as currently installing conda env"
else
    echo "Installing Jupyter kernel"
    source activate /home/ec2-user/SageMaker/.env/rapidsai
    python -m ipykernel install --name 'rapidsai' --user
    echo "Finished setting up Jupyter kernel"
fi
EOF

echo "Finishing on Start script"
```

#### Create notebook instance with Lifecycle Configuration `rapidsai`
"Readme.md" 49L, 1639C
