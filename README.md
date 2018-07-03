# Leaf-Recognition-using-Tensorflow
Detection of Leaves in a Plant using TensorFlow and SSD Mobilenet Model.

# Prerequistes:
->Install Python2.7/Python3.
->Create a virtual environment.
->Inside the virtual env, Install Tensorflow, Google Protobuf Library and so on.
->Clone the models repo from: https://github.com/tensorflow/models.git

# Training the model:
  The necessary images , their xml files and their csv files are provided. The tfrecords are also generated.
  I've used ssd_mobilenet_v2_coco model  https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
  Download and extract the model. The config file should be edited accordingly if any changes are made.
  
  To train the model, get into the environment and run this command at all directories:
    ```export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim```

  From the models/research/object_detection :
  python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/ssd_mobilenet_v2_coco.config

  The number of steps to be run, is dependent on the user and the amount of error.

  This generates a numbered ckpt file in training directory; based on the latest checkpoint select the apt number and run the     following command:
  
  python export_inference_graph.py \
    --input_type image_tensor \
    --pipeline_config_path training/ssd_mobilenet_v2_coco.config \
    --trained_checkpoint_prefix training/model.ckpt-1090 \
    --output_directory leaf_graph
    
   A frozen_inference_graph.pb generated inside the leaf_graph directory is to be used in the Detection.ipynb file
   The test_images folder should contain the neccessary images on which image processing is to be done.

  NOTE: I've provided the leaf_graph folder based on my training and my images; if you are unable to create your own model; use         this
