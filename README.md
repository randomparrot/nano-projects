# CT Scan Disease Detector
This project aims to use a ct-scan as an input image and detect whether the person in the scan has no diseases, COVID-19, tuberculosis, or pneumonia. 


![image](https://github.com/randomparrot/nano-projects/assets/68300789/1a5b2a2c-6627-4370-9725-1e95e5081729)
![image](https://github.com/randomparrot/nano-projects/assets/68300789/fa554b81-7b85-4fba-8f02-8d0db2df52ad)



^ An example output. The top image represents the input image, while the bottom represents the output image. The percent represents the model's confidence in identifying this scan as showing signs of tuberculosis.

## The Algorithm

This program utilizes imagenet and resnet-18 and adds more possible outputs (the resulting disease detected). The existing model has been training to have a >90% accuracy. Essentially, with resnet-18 being
the base AI program, while training the program was able to classify various ct-scans as COVID19, normal, tuberculosis, and pneuomnia by identifying similarities and differences. It uses torch and torchvision
to train.
When training, I used the script python3 train.py --model-dir=models/ct-scan data/ct-scan epochs = 35, essentially training the model off of input data images and allowing it to learn and become more accurate as the epochs ran. 
Afterwards, I exported the model as an .onnx, using the script python3 onnx_export.py --model-dir=models/ct-scan
After these steps, I was successfully able to use the trained model which is about 91% accurate.

## Running this project

1. Use the jetson-inference project (git clone --recursive https://github.com/dusty-nv/jetson-inference) and change directories into it 
2. To use the existing model, download the following file named resnet18.onnx at this link : https://www.mediafire.com/file/njdth21j6gaotbx/resnet18.onnx/file
3. Download the data from this link: https://www.kaggle.com/datasets/jtiptj/chest-xray-pneumoniacovid19tuberculosis?resource=download
4. Download labels.txt and put it under jetson-inference/python/training/classification/models/
5. Create two new directories under data and models both called ct-scan
6. Unzip the contents of the kaggle file into the data directory. Once finished, you should see test, train, and val directories which contain images of the various categories
7. In the terminal, go to jetson-inference/python/training/classification using the cd command.
8. Create variables by typing NET=models/ct-scan and DATASET = data/ct-scan
9. Test it out! Use an image of your choice from the test folder in data, then type imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=models/labels.txt $DATASET/[location of test image, should be put after data/ct-scan] [name of output].jpg
   *NOTE: remove parenthesis from any test images
10. You should now be able to see an output image named as whatever you specified above

[View a video explanation here]
https://youtu.be/O3j3b4v2Igg
