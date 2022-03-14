# co-training_for_autonomous-driving
This code is for paper Robust Object Detection for Autonomous Driving based on Semi-supervised Learning.
## Install
Install detectron2. Refer to [detection](https://github.com/facebookresearch/moco/tree/main/detection)
## Use MoCo
```
git clone https://github.com/facebookresearch/moco.git
```
Convert a pre-trained MoCo model to detectron2's format:
```
python3 convert-pretrain-to-detectron2.py input.pth.tar output.pkl
```
To implement original MoCo, refter to [MoCo](https://github.com/facebookresearch/moco)
## Prepare Dateset
Use KITTI 2D object detection dataset and Nuscene. Refer to [KITTI](http://www.cvlibs.net/datasets/kitti/eval_object.php?obj_benchmark=2d) and [nuScenes](https://www.nuscenes.org/nuscenes).
<br>Convert from KITTI to PASCAL VOC file format:<br>
```
python generate_xml.py
```
## Generate Pseudo-labels
Replace the original detectron2 with the modified version:
```
sudo cp -r ./detectron2 /usr/local/lib/python3.7/dist-packages/detectron2
```
```
python train_net.py --config-file configs/pascal_voc_R_50_C4_24k_moco.yaml \
 --num-gpus 8 MODEL.WEIGHTS ./output.pkl
```
