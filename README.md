# 3D Printer Failure Detection

This is a local program desined to run on the NVIDIA Jetson Nano using the jetson-inference libraries. It detects failures in 3D prints.

## The Algorithm

The code is based off of a retrained resnet18 model that I trained on roughly 1500 images of both failed and successful prints. There are two classes, fail and not_fail

## Running this project

1. Download all of the files included in this repository as a .zip.
2. Ensure the jetson-inference library has been installed on your Jetson Nano.
3. Upload and unzip the code in your Nano under the jetson-inference/python/training/classification directory
4. Run the code
        
   (a) To run the code and have the input be your webcam, type: imagenet --model=/home/nvidia/jetson-inference/python/training/classification/models/print_fail_detect/resnet18.onnx --labels=/home/nvidia/jetson-inference/python/training/classification/models/print_fail_detect/labels.txt --input-blob=input_0 --output-blob=output_0 /dev/video0
        
   (b) To run the code and have the input be your own video/image file, put that file within the jetson-inference folder on your Nano. Once that is completed, continue and run: imagenet --model=/home/nvidia/jetson-inference/python/training/classification/models/print_fail_detect/resnet18.onnx --labels=/home/nvidia/jetson-inference/python/training/classification/models/print_fail_detect/labels.txt --input-blob=input_0 --output-blob=output_0 /[path-to-your-file]

   (c) If you want to be able to see what the webcam is seeing, add an output source to the end, after you define your input source. This is explained very well by the jetson-inference documentation, found here: https://github.com/dusty-nv/jetson-inference/blob/master/docs/aux-streaming.md
   An example for this would be: imagenet --model=/home/nvidia/jetson-inference/python/training/classification/models/print_fail_detect/resnet18.onnx --labels=/home/nvidia/jetson-inference/python/training/classification/models/print_fail_detect/labels.txt --input-blob=input_0 --output-blob=output_0 /dev/video0 webrtc://@:1234/out
   This would create a WebRTC stream viewable via your browser. To access it you would just type [Your_jetsons_IP]:1234 
        
5. There will be prints in the terminal that will classify the image supplied as either "fail" or "not_fail", and on an output stream there will be a readout in the top left corner of the AI's confidence and if it believes the print has failed.

[View a video explanation here](https://www.youtube.com/watch?v=msI9ZKM9R8Q)

## Dataset Used
If you want to use my dataset, here it is!
[Kaggle](https://www.kaggle.com/datasets/padraigvalenti/3d-printing-failure-detection)
