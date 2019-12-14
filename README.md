
## ImageclassificationProject

 This project is an image classification project in Pattern recognition class. 
Our goal is getting **better score**  from the process of extracting good performance in the Kagle.  
The basic base is 101 subjects in the paper, 30 chapters in each topic.  
We wanted to improve the performance based on the actual data that we categorize in the kaggle.


## install dependencies
#### Use openCV(SIFT)
```
! yes | pip3 uninstall opencv-python
! yes | pip3 uninstall opencv-contrib-python
! yes | pip3 install opencv-python==3.4.2.16
! yes | pip3 install opencv-contrib-python==3.4.2.16
```
#### Data Load (from kaggle)
```
! kaggle competitions download -c 2019-ml-finalproject
! unzip 2019-ml-finalproject.zip
```
####  Use Kmeans using GPU
```
!pip install kmc2
```
#### Use pickle for time Saving
```
# Save
#with open('/content/drive/My Drive/2019-ml-finalproject/codebook2.pickle','wb') as f:
# pickle.dump(codebook,f,pickle.HIGHEST_PROTOCOL)
# Load
with  open('/content/drive/My Drive/2019-ml-finalproject/codebook2.pickle', 'rb') as f:
codebook = pickle.load(f)
```

## Paper
[Beyond Bags of Features: Spatial Pyramid Matching for Recognizing Natural Scene Categories](https://inc.ucsd.edu/~marni/Igert/Lazebnik_06.pdf)

## Report
### BOVW (Base : 41.2)
##### Level 0 , CodebookSize = 200, kmc2 
step:8, linearSVC(C=0.0004) -> 0.30082

step:8, histogramIntersection  -> 0.36643

step:8, histogramIntersection kmeans++ -> 0.35992

---- use 2758 images ---- I

step:8, histogramIntersection, ImageSize(reduction) -> **0.43557**

step:8, use augmentation -20~20 per 5 rotation and reversal ->  0.40248

step:8, use only reversal image -> 0.41843

step:8, PCA 100 on descriptor -> 0.13888
---- use 3030 images ---- I

### SPM (Level2, codebooksize:200)
|  <center>STEP SIZE</center> |  <center>SCALER</center> | <center>Histogram</center> |<center>Intersection</center> |<center>Imgsize</center> |<center>Result</center> |
|:--------|:--------:|--------:|--------:|--------:|--------:|
| <center>8 </center> | o </center> |<center>append </center> |<center>o </center>|<center> -16 edge </center>|<center>0.56737</center>
| <center>8 </center>| x </center> |<center>append </center> |<center>o </center>|<center>-16 edge </center>|<center>0.43498 </center>
| <center>8 </center>| o </center> |<center>sum </center> |<center>o </center>|<center>-16 edge </center>|<center>0.55555</center>
| <center>8 </center>| x </center> |<center>sum </center> |<center>o </center>|<center>-16 edge </center>|<center>0.34633</center>
| <center>4 </center>| o </center> |<center>append </center> |<center>o </center>|<center>-16 edge </center>|<center>0.56501</center>
| <center>8 </center>| o </center> |<center>append </center> |<center>o </center>|<center>256*256 </center>|<center>0.56087</center>
| <center>8 </center>| o </center> |<center>append </center> |<center>x </center>|<center>256*256 </center>|<center>0.57565</center>

### VLAD(Cut -16 edges )
200 codebook, SVC(linear, C=1) -> **0.57978**

200 codebook, SVC(linear, C=10) -> 0.56087

200 codebook, SVC(linear, C=1), PCA -> 0.02245

512 codebook, SVC(linear, C=1) -> 0.55791

Resize 256,256, 200 codebook, SVC(linear, C=1) ->0.55260


## Mistake
 I use google drives that prevent time-consuming per each time data was loaded from Kaggle.  Losses occurred during data loading into the drive. Learning data should be 101*30=3030 pics, but there was  2758 pics so a lot of time loss while carrying out.
 Also, After a certain period of time, the session error will occur and become initialized. You must always store it. In my code, you can see many pickle code.

## Reference

[VLAD](https://github.com/lixuan0023/VLAD/blob/master/VLADClass.py)

[VLAD_codebook](https://books.google.co.kr/books?id=SXzQDQAAQBAJ&pg=PA373&lpg=PA373&dq=vlad+512&source=bl&ots=yNc1cKp-Qv&sig=ACfU3U3BHKySxHTGh8MF0uiUj1mZxKtRSw&hl=ko&sa=X&ved=2ahUKEwiTnuXipbXmAhXYMN4KHfr-BawQ6AEwAHoECAcQAQ#v=onepage&q=vlad%20512&f=false)

[Intersection](https://github.com/wihoho/Image-Recognition/blob/5dc8834dd204e36172815345f0abe5640a4a37ef/recognition/classification.py#L10)

[SPM1](https://github.com/bilaer/Spatial-pyramid-matching-scene-classifier)

[SPM2](https://github.com/TrungTVo/spatial-pyramid-matching-scene-recognition/blob/master/spatial_pyramid.ipynb)
