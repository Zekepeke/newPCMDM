# README

## Done:

- Got AWS running and ran all the requirements
- The SMPLH_MALE.pkl, the processed AMASS data used in the TECH repo, and official BABEL annotation dataset
- Don't know if "babel_v1-0_release.zip" from BABEL paper is the babel_v2.1?


## Current:

- Doing data prep
- need to train a model on the data 
- Emailing the authors of the paper


## Data preparation
Due to licensing restrictions, we are unable to provide pre-processed data directly. However, you can refer to [TEACH](https://github.com/athn-nik/teach#data) for specific data processing methods.

Eventually, you should have a folder `data` with such a structure:
```
data
|-- babel
|   `-- babel_v2.1
|       `...
|   `-- babel-smplh-30fps-male 
|       `...
|
|-- smpl_models
|   `-- smplh
|       `--SMPLH_MALE.pkl
```

Besides, you should download the folder `deps` in [TEACH](https://github.com/athn-nik/teach/tree/main/deps) to this project.

## Pre-trained weights
We provide the pretrained models here: [pretrained models](https://drive.google.com/drive/folders/1Lrj5FEt7bFFiv_VnfoDFoQgZzfF4X6RJ?usp=sharing). The 'pretrained.zip' file contains the pretrained model and training configurations used to report metrics in our paper, while 'MotionCLIP.zip' contains the model used for evaluation. You can put the pretrained model and training configuration file under `./save/pcmdm` and put the `MotipnClip.ckpt` under `./motionclip_save`.

## Running the code
You can use the following three commands to obtain the results for the last three rows of the experimental results table in our paper:
```
# No special sampling
python eval.py --model_path ./save/pcmdm/model000600000.pt --guidance_param 2 --inpainting_frames 0

# Past inpainting sampling
python eval.py --model_path ./save/pcmdm/model000600000.pt --guidance_param 2 --inpainting_frames 2

# Compositional transition sampling
python eval.py --model_path ./save/pcmdm/model000600000.pt --guidance_param 2 --composition True --inter_frames 2
```

Besides, if you want to train a model from scratch, you can use this comman:
```
python train_diffusion.py --save_dir ./save/pcmdm --dataset babel --hist_frames 5 
```

## Acknowledgments
Our code is based on [TEACH](https://github.com/athn-nik/teach) and [MDM](https://github.com/GuyTevet/motion-diffusion-model). Thanks for their greate work!
