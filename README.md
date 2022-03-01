# JetsonNano_ObjectDetection

installation
https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md

Traing dataset
https://teachablemachine.withgoogle.com/train/image

cv2.rectangle(img, (x1, y1), (x2, y2), (255,0,0), 2)


x1,y1 ------
|          |
|          |
|          |
--------x2,y2
Record dataset
:~/jetson-inference/python/training/detection/ssd$ camera-capture /dev/video0 
Training
:~/jetson-inference/python/training/detection/ssd$ python3 train_ssd.py --dataset-type=voc --data=data/electronics --model-dir=models/electronics --batch-size=2 --workers=1 --epochs=30
Export model
:~/jetson-inference/python/training/detection/ssd$ python3 onnx_export.py --model-dir=models/electronics
Run AI
~/jetson-inference/python/training/detection/ssd$ detectnet --model=models/electronics/ssd-mobilenet.onnx --labels=models/electronics/labels.txt  --input-blob=input_0 --output-cvg=scores --output-bbox=boxes /dev/video0
