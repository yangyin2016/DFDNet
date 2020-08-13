## [Blind Face Restoration via Deep Multi-scale Component Dictionaries](https://arxiv.org/pdf/2008.00418.pdf)

>#### __Note: This branch contains all the restoration results, including 512*512 face region and putting them to the origial input.__ 


<p>
Overview of our proposed method. It mainly contains two parts: (a) the off-line generation of multi-scale component dictionaries from large amounts of high-quality images, which have diverse poses and expressions. K-means is adopted to generate K clusters for each component (i.e., left/right eyes, nose and mouth) on different feature scales. (b) The restoration process and dictionary feature transfer (DFT) block that are utilized to provide the reference details in a progressive manner. Here, DFT-i block takes the Scale-i component dictionaries for reference in the same feature level.
</p>  
    

<img src="./Imgs/pipeline_a.png">
<p align="center">(a) Offline generation of multi-scale component dictionaries.</p>
<img src="./Imgs/pipeline_b.png">
<p align="center">(b) Architecture of our DFDNet for dictionary feature transfer.</p>


## Pre-train Models and dictionaries
Downloading from the following url and put them into ./.
- [BaiduNetDisk](https://pan.baidu.com/s/1K4fzjPiezVSMl5NjHoJCGQ) (s9ht)
- [GoogleDrive](https://drive.google.com/drive/folders/1bayYIUMCSGmoFPyd4Uu2Uwn347RW-vl5?usp=sharing)

These folder structure should be:
    
    .
    ├── checkpoints                    
    │   ├── facefh_dictionary                  
    │   │   └── latest_net_G.pth   
    ├── weights
    │   └── vgg19.pth
    ├── DictionaryCenter512
    │   ├── right_eye_256_center.npy
    │   ├── right_eye_128_center.npy
    │   ├── right_eye_64_center.npy
    │   ├── right_eye_32_center.npy
    │   └── ...
    └── ...

## Prerequisites
- Pytorch (≥1.1 is recommended)
- dlib
- [face-alignment](https://github.com/1adrianb/face-alignment)
    ```bash
    cd ./FaceLandmarkDetection
    python setup.py install
    cd ..
    ```
    

## Testing
1. Crop face from the whole image.
```bash
python test_FaceDict.py
```
#### __Four parameters in ```test_FaceDict.py``` can be changed for flexible restoration:__
- Line 149: ```opt.gpu_ids = [0] # gpu id. if use cpu, set opt.gpu_ids = []```
- Line 150: ```TestImgPath = './TestData/TestWhole' # test image path```
- Line 151: ```ResultsDir = './Results/TestWhole' #save path```
- Line 152: ```UpScaleWhole = 4  # the upsamle scale for the final results```

>Note: our model can only generate 512&times;512 face result and the background will be further enhanced in the future work.)

#### __Results path contains the following foler:__
- Step0_Input: ```# Save the input image.```
- Step1_AffineParam: ```# Save the crop and align parameters for the latter copying the face result to the original input.```
- Step1_CropImg: ```# Save the cropped face images and resize them to 512×512.```
- Step2_Landmarks: ```# Save the landmarks for RoIAlign.```
- Step3_RestoreCropFace: ```# Save the face restoration results (512×512).```
- Step4_FinalResults: ```# Save the final restoration results by putting the face result to the original input.```

## Some plausible restoration results on real low-quality images

 <table  style="float:center" width=100%>
 <tr>
  <th><B>Input</B></th><B>Crop Face</B></th><B>Restore Face</B></th><th><B>Final Results</B></th>
 </tr>
 <tr>
  <td>
  <img src='./Imgs/RealLR/n000056_0060_01.png'>
  </td>
  <td>
   <img src='./Imgs/ShowResults/n000056_0060_01.png'>
  </td>
 </tr>
 
  
 </table>

## Citation

```
@InProceedings{Li_2020_ECCV,
author = {Li, Xiaoming and Chen, Chaofeng and Zhou, Shangchen and Lin, Xianhui, Zuo, Wangmeng and Zhang, Lei},
title = {Blind Face Restoration via Deep Multi-scale Component Dictionaries},
booktitle = {ECCV},
year = {2020}
}
```

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

