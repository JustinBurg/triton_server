# Deploying an object detection model with Nvidia Triton Inference Server

**Download a pretrained model and create an object detection service**
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

