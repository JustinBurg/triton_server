# Triton Server

### Install the Triton Server Container:
`docker pull nvcr.io/nvidia/tritonserver:22.01-py3`

### Install the Triton Server Client
`pip3 install tritonclient`\
  or\
`pip3 install tritonclient[http]`\
  or\
`docker pull nvcr.io/nvidia/tritonserver:22.01-py3-sdk`\

## Using Triton
Before Triton can be used, it requires that the model be saved in specific directory structure:\
![file_structure](triton_model_repository_layout.png)

Once the model has been saved in the model respository, you can start the Triton Server container:\
`docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v $PWD/model_repository:/models nvcr.io/nvidia/tritonserver:22.01-py3 tritonserver --model-repository=/models`
