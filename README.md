






NOTE FOR PADRAIG BEFEORE RELEASE: CHECK TO SEE IF OUTPUT TO RTSP OR WHATEVER IS POSSIBLE IDK










# 3D Printer Failure Detection

This is a local program desined to run on the NVIDIA Jetson Nano using the jetson-inference libraries. It detects failures in 3D prints and will notify you.

![An example of a failed print that this program will detect for you.](direct image link here)

## The Algorithm

The code is based off of a retrained resnet18 model that I trained on roughly 1500 images of both failed and successful prints. There are two classes, fail and not_fail. The Python script that you run uses an 'if' statement that when the class is fail and the model's confidence is over 60%, it prints a message into the terminal.

## Running this project

1. Download all of the files included in this repository as a .zip.
2. Ensure the jetson-inference library has been installed on your Jetson Nano.
3. Upload and unzip the code in your Nano under the jetson-inference/python/training/classification directory
4. cd back to jetson-inference
5. Run the docker using docker/run.sh
6. cd into python/training/classification
7. Run the code
        
        (a) To run the code and have the input be your webcam, type: imagenet --model=models/print_fail_detect/resnet18.onnx --labels=data/print_fail_detect/labels.txt --input-blob=input_0 --output-blob=output_0 /dev/video0
        
        (b) To run the code and have the input be your own video/image file, put that file within the jetson-inference folder on your Nano. Once that is completed, continue and run imagenet --model=models/print_fail_detect/resnet18.onnx --labels=data/print_fail_detect/labels.txt --input-blob=input_0 --output-blob=output_0 /[path-to-your-file]
        
There will be prints in the terminal that will classify the image supplied as either "fail" or "not_fail".

[View a video explanation here](video link)