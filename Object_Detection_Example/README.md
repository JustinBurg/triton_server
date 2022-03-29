# Deploying an object detection model with Nvidia Triton Inference Server

**Download a pretrained model and create an object detection service**\
To create the object detection inference service, you need a pretrained model for object detection.\
Download the Dense Convolutional Network (DenseNet) model, based on an ONNX Runtime backend.\
ONNX Runtime has the capability to train existing models through its optimized backend.

To set up your object detection service, do the following:\
A. Create a repository structure compatible with the Triton container you subscribed to in Step 1. To do this, in the EC2 instance’s terminal window, run the following command:\
`mkdir -p model_repository/densenet_onnx/1`\

B. To download the DenseNet model, run the following command:\
`wget -O model_repository/densenet_onnx/1/model.onnx https://contentmamluswest001.blob.core.windows.net/content/14b2744cf8d6418c87ffddc3f3127242/9502630827244d60a1214f250e3bbca7/08aed7327d694b8dbaee2c97b8d0fcba/densenet121-1.2.onnx`\
If successful, it returns a message similar to this one:\
`2020-12-18 20:25:46 (14.1 MB/s) - ‘model_repository/densenet_onnx/1/model.onnx’ saved [32719461/32719461]`\

C. To download the associated Triton configuration files for this particular model, run the following command:\
`wget -O model_repository/densenet_onnx/config.pbtxt https://raw.githubusercontent.com/triton-inference-server/server/master/docs/examples/model_repository/densenet_onnx/config.pbtxt`\
If successful, it returns a message similar to this one:\
`2020-12-18 20:30:49 (35.5 MB/s) - ‘model_repository/densenet_onnx/config.pbtxt’ saved [387/387]`\

D. To download a list of over 1,000 labels that the DenseNet model is trained to classify objects with, run the following command:\
`wget -O model_repository/densenet_onnx/densenet_labels.txt https://raw.githubusercontent.com/triton-inference-server/server/master/docs/examples/model_repository/densenet_onnx/densenet_labels.txt`\
If successful, it returns a message similar to this one:\
`2020-12-18 20:33:10 (78.0 MB/s) - ‘model_repository/densenet_onnx/densenet_labels.txt’ saved [10311/10311]`\

Start the Triton Inference Server that is pointing to the model_repository that contains your densenet model and config file:\
`docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v $PWD/model_repository:/models nvcr.io/nvidia/tritonserver:22.01-py3 tritonserver --model-repository=/models`

On your local machine or on the same instance as your Triton Server, open another terminal and pull the client container:\
`docker pull nvcr.io/nvidia/tritonserver:22.01-py3-sdk`

The client container contains an example image that we can use for inference. 

To start the client container:\
`docker run -it --rm --net=host nvcr.io/nvidia/tritonserver:22.01-py3-sdk`

In the container, you can run inference using the Python binding with the following:\
`/workspace/install/bin/image_client -u 54.147.254.227:8000 -m densenet_onnx -c 3 -s INCEPTION /workspace/images/mug.jpg`\
Where:
`/workspace/install/bin/image_client` is the Python version of the image classification client that came with the client image\
`54.147.254.227:8000` is the location of the Triton Inference Server accepting HTTP requests\
`-m densenet_onnx` is the model in the model_repository that the Triton Inference Server is mapped to\
`-c 3` is the number of classifications we want inferred, ie:\
    `0.754130 (505) = COFFEE MUG`\
    `0.157077 (969) = CUP`\
    `0.002880 (968) = ESPRESSO`\
`/workspace/images/mug.jpg` is the location of the image being inferenced upon


