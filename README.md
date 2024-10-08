# Denoising Diffusion Pytorch
Implementation of DDPM (https://arxiv.org/abs/2006.11239) in Pytorch with class conditioning.

Model architecture:
- Class conditioned on label.
- UNet with 4 downsample, 4 upsample blocks. Self-attention at the 16x16 resolution and bottleneck layer.
- Pre-activation for all resnet blocks.

<img src="examples/dropout_0.1_classes_10_lr_0.0002_timesteps_4000_warmup_5000_label_True_attn_True_act_relu_preact_True_zero_20240826_59_1200000_128_4000.png" width="800">

## Training
```
accelerate launch train.py
```

## Sample Image Grid
Generate samples and render a grid of images into one image.

### No Labels
```
python sample_grid.py --checkpoint_path=<path> --rows=8 --cols=8
```
![](examples/20240819_8x8.png)

### Labels
```
python sample_grid.py --checkpoint_path=<path> --cols=8 --num_classes=10 --labels_list="airplane,automobile,bird,cat,deer,dog,frog,horse,ship,truck"
```


## Save Images to Folder
Save a large number of images to a destination folder for running eval metrics.
```
python sample_images.py --checkpoint_path=<path> --output_dir=<dir> --num_images=50000 --batch_size=2500
```
