# YOLOv7-Instance-Segmentation-and-Tracking


## Steps to run Code

- Clone the repository
```
git clone https://github.com/MrFahad/YOLOv7_Segmentation_and_Tracking.git
```
- Goto the cloned folder.
```
cd YOLOv7-Segmentation
```
- Create a virtual envirnoment (Recommended, If you dont want to disturb python packages)
```
## For Linux Users
python3 -m venv YOLOv7_Segmentation
source YOLOv7_Segmentation/bin/activate

## For Windows Users
python3 -m venv YOLOv7_Segmentation
cd YOLOv7_Segmentation
cd Scripts
activate
cd ..
cd ..
```
- Upgrade pip with mentioned command below.
```
pip install --upgrade pip
```
- Install requirements with mentioned command below.
```
pip install -r requirements.txt
```
- Download weights from [link](https://github.com/MrFahad/YOLOv7_Segmentation_and_Tracking/releases/tag/YOLOv7_Seg_Track) and store in "YOLOv7-Segmentation" directory.

- Run the code with mentioned command below.
```
#for segmentation with detection + Tracking
python3 segment/predict.py --weights yolov7-seg.pt --source "fb1.mp4" --trk
```

- Output file will be created in the working directory with name <b>YOLOv7_Segmentation/runs/predict-seg/exp/"original-video-name.mp4"</b>

### RESULTS
<table>
  <tr><td>Football Players Segmentation + Tracking</td></tr>
  <tr>
    <td><img src="https://github.com/MrFahad/YOLOv7_Segmentation_and_Tracking/blob/main/fb.png" width=400 height=200></td>
  </tr>
  </tr>
 </table>

## Custom Data Labelling

- I have used [roboflow](https://roboflow.com/) for data labelling. <b>The data labelling for Segmentation will be a Polygon box,While data labelling for object detection will be a bounding box</b>

- Go to the [link](https://app.roboflow.com/my-personal-workspace/createSample) and create a new workspace. Make sure to login with roboflow account.


![1](https://user-images.githubusercontent.com/62513924/190390384-db8f71fa-e963-4ee6-aaca-c49e993c64ae.png)


- Once you will click on <b>create workspace</b>, You will see the popup as shown below to upload the dataset.

![2](https://user-images.githubusercontent.com/62513924/190390882-fe08559d-ef47-450e-8613-2de899fffa4c.png)


- Click on upload dataset and roboflow will ask for workspace name as shown below. Fill that form and then click on <b>Create Private Project</b>
- Note: Make sure to select <b>Instance Segmentation</b> Option in below image.
 ![dataset](https://user-images.githubusercontent.com/62513924/190853038-612791d0-9b33-4222-b28a-63ac4c13ed83.png)


-You can upload your dataset now.

![Screenshot 2022-09-17 155330](https://user-images.githubusercontent.com/62513924/190853135-887b389c-2356-4435-a946-867bb05ac4f2.png)

- Once files will upload, you can click on <b>Finish Uploading</b>.

- Roboflow will ask you to assign Images to someone, click on <b>Assign Images</b>.

- After that, you will see the tab shown below.

![6](https://user-images.githubusercontent.com/62513924/190392948-90010cd0-ef88-437a-b94f-44ee93d8bc31.png)


- Click on any Image in <b>Unannotated</b> tab, and then you can start labelling.

- <b>Note:</b> Press p and then draw polygon points for <B>segmentation</b>

![10](https://user-images.githubusercontent.com/62513924/190394353-d7dd7b7f-7a07-4738-99b6-1d5ae66b5bca.png)


- Once you will complete labelling, you can then export the data and follow mentioned steps below to start training.

## Custom Training

- Move your (segmentation custom labelled data) inside "YOLOv7-Segmentation\data" folder by following mentioned structure.



![ss](https://user-images.githubusercontent.com/62513924/190388927-62a3ee84-bad8-4f59-806f-1185acdc8acb.png)



- Go to the <b>data</b> folder, create a file with name <b>custom.yaml</b> and paste the mentioned code below inside that.

```
train: "path to train folder"
val: "path to validation folder"
# number of classes
nc: 1
# class names
names: [ 'car']
```

- Go to the terminal, and run mentioned command below to start training.
```
python3 segment/train.py --data data/custom.yaml --batch 4 --weights '' --cfg yolov7-seg.yaml --epochs 10 --name yolov7-seg --img 640 --hyp hyp.scratch-high.yaml
```

## Custom Model Detection Command
```
python3 segment/predict.py --weights "runs/yolov7-seg/exp/weights/best.pt" --source "fb1.mp4"
```
### RESULTS
<table>
  <tr><td>Football Players Segmentation + Tracking</td></tr>
  <tr>
    <td><img src="https://github.com/MrFahad/YOLOv7_Segmentation_and_Tracking/blob/main/fb.png" width=400 height=200></td>
  </tr>
  </tr>
 </table>

## References
- https://github.com/WongKinYiu/yolov7/tree/u7/seg
- https://github.com/ultralytics/yolov5
