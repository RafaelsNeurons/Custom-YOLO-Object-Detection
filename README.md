#Custom-YOLO-Object-Detection
In this Project I train YOLO to detect objects of my own dataset.
For this Project the Darknet-Framework was used to train the YOLOv3-Network.

I created my own dataset with sensor images. The camera I used was the Intel Realsense D435, but I only used 2D-Images.
The images were labeled with labelImg.
I trained the model with Google Colab.

#Conclusion:
Object detection works well even with a relatively small data set of 50 images. Object detection in a video or in real time is not yet smooth. The video is analyzed frame by frame, so the stream stops between the individual frames. I still see potential for improvement in this respect. Next, however, I will use the Tensorflow framework again.


Step by Step:
1. clone the github repository
    for yolov3:
    for yolov4: git clone https://github.com/AlexeyAB/darknet.git
    
2.Make changes in the darknet/Makefile

GPU=1
CUDNN=1
OPENCV =1

2. Download Pretrained Convolutional Weights 
    for yolov3 on https://pjreddie.com/darknet/yolo/  (yolov3.weights,darknet53.conv.74)
    for yolov4 on https://github.com/AlexeyAB/darknet (yolov4.weights, yolov4.conv.137)
    
3. Change Weights Save Interval (its good to change this because google colab can shut down if you don´t have the pro version)
    for yolov3 open the detector.c file in darknet/example and change line 138. Just change the 10000 to 1000 like 
                if(i%1000==0 || (i < 1000 && i%100 == 0)){
    
    for yolov4 no change is nessesary
    
4. Copy configuration file to darknet folder
        Yolov3:
        
        Yolov4: Go to yolov4/darknet/cfg and copy the yolov4.cfg data to yolov4/darknet
        
5. Make changes in the .cfg 

  for yolov3:
  
  for yolov4:
    in line 2,3 change  batch=64
                        Subdivisions=12
                        
    in line 8,9 change  width=64
                        height=12
                       
    in line 20 change  max_batches=2000
    
    in line 22 change steps=1800
   

    in line 961,968 change filters = 18      # filters = (classes+5)*3 , so you have to change it to your amount of classes for example (1+5)*3 = 18 =filters
                           classes = 1       #if you train more than 1 object you have to change it to your amount of classes
   
   
    in line 1049,1056 change filters = 18
                             classes = 1
                             
                           
     in line 1137,1144 change filters = 18
                              classes = 1
    
    6. Save the changes and rename your .cfg for example to 
                for yolov3: sensor_yolov3.cfg
                for yolov4: sensor_yolov4.cfg
                
                
     DATA PREPARATION:
     
     1. Collect images
            - a minimum number of 500+ images for a single class (2000 to 3000 is recommended) #I used 50 for my first try and it worked also
            
     2. Inside the darknet folder create a folder called 'sensor_data' and inside it 'sensor_images'
     
     3. Save the images inside sensor_images
     
     4. Label the images 
            - I used labelImg by tzutalin. (https://github.com/tzutalin/labelImg)
            - In LabelImg you have to change the setting to YOLO ( setting in the left under corner)
            
     5. Split the Data into Train and Test
            5.1 create the file sensor_data/sensor_training.txt
            5.2 create the file sensor_data/sensor_testing.txt
            5.3 copy the paths of the images in there and split it to 80% training 20% testing 
                      -for example /sensor_data/sensor_images/image1.jpg
            
            
     6. Create a folder called 'sensor_labels' inside 'sensor_data'
     
     7. Copy all label files to 'sensor_labels' (also the classes file)
     
     8. Create the Object Label File
            8.1 create the file sensor.names inside the folder sensor_data
            8.2 write in the sensor.names file the name of your lable which you gave your pictures in labelImg
                        - in my case it was 'sensor_io'
                        
                        
      9. Create the data file
            9.1 create the file sensor.data inside the folder sensor_data
            9.2 write in the sensor.data file :
            
                classes =1
                train = sensor_data/sensor_training.txt
                valid = sensor_data/sensor_testing.txt
                names = sensor_data/sensor.names
                backup = backup
            9.3 save the file
       
       10. zip the darknet folder and load it to your google drive
       
       11. then go to colab and proceed with my jupyter-notebook sensor_custom.ipynb
                - maybe you have the change the weight and cfg. names in the notebook
                - maybe you have to change the Makefile, cause of the arches of the GPU, but I wrote a text in the Notebook about it
     
                        
                        
                        
