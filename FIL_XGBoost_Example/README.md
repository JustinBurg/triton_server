# Triton FIL backend with XGBoost
This is an abbreviated notebook for deploying an XGBoost model on Triton with the FIL backend. 

The full notebook explains how one can deploy XGBoost model in Triton, check deployment status and send inference requests, set concurrent model execution and dynamic batching and find the best deployment configuration using Model Analyzer.
https://github.com/triton-inference-server/fil_backend/blob/main/notebooks/simple-xgboost/simple_xgboost_example.ipynb

Copy the `xgboost_model_triton_example.ipynb` onto your ec2 instance.  You will need to have jupyter lab installed.  The easiest way is to start jupyter lab and then use the upload capability in jupyter lab.  For example, I started jupyter lab and uploaded my notebook to my projects folder under:\
`/home/ubuntu/projects`\

On the GPU EC2 instance, created a folder called `model_repository`.  This will be the directory structure that contains your models:\
`ubuntu@ip-10-0-1-122:~$ cd model_repository/`\
`ubuntu@ip-10-0-1-122:~/model_repository$ ls`\
`densenet_onnx  fil`

