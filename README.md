# Triton Server

### Install the Triton Server Container:
`docker pull nvcr.io/nvidia/tritonserver:22.01-py3`

### Install the Triton Server Client
`pip3 install tritonclient`\
  or\
`pip3 install tritonclient[http]`\
  or\
`docker pull nvcr.io/nvidia/tritonserver:22.01-py3-sdk`

## Using Triton
Before Triton can be used, it requires that the model be saved in specific directory structure:\
<img src="https://github.com/JustinBurg/triton_server/blob/main/triton_model_repository_layout.png" width="300">

Once the model has been saved in the model respository, you can start the Triton Server container:\
`docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v $PWD/model_repository:/models nvcr.io/nvidia/tritonserver:22.01-py3 tritonserver --model-repository=/models`

Check the status of the server connection by running the following curl command:\
`curl -v <IP of machine>:8000/v2/health/ready`\
which should return `HTTP/1.1 200 OK`

## Using Triton Client
You can run the Triton Server client either as a container or embeded in your code located in a script or jupyter notebook./ 

To run in your code, install the client via pip:\
`pip3 install tritonclient[http]`\
and import the library:
`import tritonclient.http as triton_http`
