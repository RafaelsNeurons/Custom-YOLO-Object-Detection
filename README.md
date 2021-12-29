#Custom-YOLO-Object-Detection
In this Project I train YOLO to detect objects of my own dataset.
For this Project the Darknet-Framework was used to train the YOLOv3-Network.

I created my own dataset with sensor images. The camera I used was the Intel Realsense D435, but I only used 2D-Images.
The images were labeled with labelImg.
I trained the model with Google Colab.

#Conclusion:
Object detection works well even with a relatively small data set of 50 images. Object detection in a video or in real time is not yet smooth. The video is analyzed frame by frame, so the stream stops between the individual frames. I still see potential for improvement in this respect. Next, however, I will use the Tensorflow framework again.
