# Triton FIL backend with XGBoost
This is an abbreviated notebook for deploying an XGBoost model on Triton with the FIL backend. 

The full notebook explains how one can deploy XGBoost model in Triton, check deployment status and send inference requests, set concurrent model execution and dynamic batching and find the best deployment configuration using Model Analyzer.
https://github.com/triton-inference-server/fil_backend/blob/main/notebooks/simple-xgboost/simple_xgboost_example.ipynb

On the GPU EC2 instance, created a folder calledd `model_repository`.  This will be the directory structure that contains your models:\
`ubuntu@ip-10-0-1-122:~$ cd model_repository/\
`ubuntu@ip-10-0-1-122:~/model_repository$ ls\
`densenet_onnx  fil`

