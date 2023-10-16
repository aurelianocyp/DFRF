# DFRF #
The pytorch implementation for our ECCV2022 paper "Learning Dynamic Facial Radiance Fields for Few-Shot Talking Head Synthesis".

[[Project]](https://sstzal.github.io/DFRF/) [[Paper]](https://arxiv.org/abs/2207.11770) [[Video Demo]](https://www.youtube.com/watch?v=F6fkVNk9bBw)

## Requirements
RTX3090，不要在A5000跑
- Python 3.7
- Pytorch3d 0.5.0(安装完requirements后自行安装，还需安装ffmpeg=4.0=hcdf2ecd_0,还需更改torch版本，pip install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
)
- process data阶段的TensorFlow要求pip install tensorflow-gpu==2.6.0.如果TensorFlow变成2.6.0后还是报错，多半是安装TensorFlow时把torch版本替换了，再次用上面的pip install一下就好了
- run阶段用tensorflow-gpu==2.6.0貌似好像也能行,错了，虽然2.6在run时能成功，但是tensorboard启动不了，所以还是乖乖在run时用tensorflow-gpu==1.15.2吧
- 处理256*256的视频时，最好把process的01 2 63457分开跑，否则跑第二步时可能会报cuda out of memory

For more details, please refer to the `requirements.txt`. We conduct the experiments with a 24G RTX3090.

- Download `79999_iter.pth` from [here](https://github.com/sstzal/DFRF/releases/tag/file) to `data_util/face_parsing`
- Download `exp_info.npy` from [here](https://github.com/sstzal/DFRF/releases/tag/file) to `data_util/face_tracking/3DMM`
- Download 3DMM model from [Basel Face Model 2009](https://faces.dmi.unibas.ch/bfm/main.php?nav=1-1-0&id=details):

    ```
    cp 01_MorphableModel.mat data_util/face_tracking/3DMM/
    cd data_util/face_tracking
    python convert_BFM.py
    ```
## Dataset
Put the video `${id}.mp4` to `dataset/vids/`, then run the following command for data preprocess.  
```
sh process_data.sh ${id}
```
The data for training the base model is [[here]](https://github.com/sstzal/DFRF/releases/tag/Base_Videos).

## Training
```
sh run.sh ${id}
```
Some pre-trained models are [[here]](https://github.com/sstzal/DFRF/releases/tag/Pretrained_Models).

## Test
Change the configurations in the `rendering.sh`, including the `iters, names, datasets, near and far`.
```
sh rendering.sh
```

## Acknowledgement 
This code is built upon the publicly available code [AD-NeRF](https://github.com/YudongGuo/AD-NeRF) and [GRF](https://github.com/alextrevithick/GRF). Thanks the authors of AD-NeRF and GRF for making their excellent work and codes publicly available. 

## Citation ##
Please cite the following paper if you use this repository in your reseach.

```
@inproceedings{shen2022dfrf,
   author={Shen, Shuai and Li, Wanhua and Zhu, Zheng and Duan, Yueqi and Zhou, Jie and Lu, Jiwen},
   title={Learning Dynamic Facial Radiance Fields for Few-Shot Talking Head Synthesis},
   booktitle={European conference on computer vision},
   year={2022}
}
```
