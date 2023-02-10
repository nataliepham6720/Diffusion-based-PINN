# Diffusion-based-Fluid-Super-resolution
<br>

PyTorch implementation of 

**A Physics-informed Diffusion Model for High-fidelity Flow Field Reconstruction** 

(<a href="https://arxiv.org/abs/2211.14680">link</a> to paper)

<div style style=”line-height: 25%” align="center">
<h3>Sample 1</h3>
<img src="https://github.com/BaratiLab/Diffusion-based-Fluid-Super-resolution/blob/main_v1/images/reconstruction_sample_01.gif">
<h3>Sample 2</h3>
<img src="https://github.com/BaratiLab/Diffusion-based-Fluid-Super-resolution/blob/main_v1/images/reconstruction_sample_02.gif">
</div>


## Datasets
Datasets used for model training and sampling can be downloaded via the following links.

- High resolution data (ground truth for the super-resolution task) (<a href="https://figshare.com/ndownloader/files/39181919">link</a>)

- Low resolution data measured from random grid locations (input data for the super-resolution task) (<b>link coming soon</b>)


## Running the Experiments
This code has been tested on the following environment:

```
PyTorch 1.7 + CUDA 10.1 + torchvision 0.8.2
TensorBoard 2.11
Numpy 1.22
tqdm 4.59
einops 0.4.1
matplotlib 3.6.2
```

Download the high res and low res data and save the data files to the subdirectory ``./data/``.

<!--
More details about how to run the experiments are coming soon.
-->

- Step 1 - Model Training

(If you prefer not to go through Step 1, we provide the following pretrained checkpoints to directly start from Step 2:
- model without physics-informed conditioning input(link)
- model with physics-informed conditioning input (link)

In the subdirectory ``./train_ddpm/``, run:

``
bash train.sh
``

or 

``
python main.py --config ./km_re1000_rs256_conditional.yml --exp ./experiments/km256/ --doc ./weights/km256/ --ni
``

The checkpoint of the trained model is by default saved at the following trajectory. You can atler the saving directory according to your need by changing the values of ``--exp`` and ``--doc``.
``.../Diffusion-based-Fluid-Super-resolution/train_ddpm/experiments/km256/logs/weights/km256/``

- Step 2 - Super-resolution

Add the file of trained model weight (e.g., ``baseline_ckpt.pth``) from Step 1 to the following directory.

``.../Diffusion-based-Fluid-Super-resolution/pretrained_weights/``



In the main directory of this repo, run:

``
python main.py --config kmflow_re1000_rs256.yml --seed 1234 --sample_step 1 --t 240 --r 30
``


## References
If you find this repository useful for your research, please cite the following work.
```
@article{shu2023physics,
  title={A Physics-informed Diffusion Model for High-fidelity Flow Field Reconstruction},
  author={Shu, Dule and Li, Zijie and Farimani, Amir Barati},
  journal={Journal of Computational Physics},
  pages={111972},
  year={2023},
  publisher={Elsevier}
}
```


This implementation is based on / inspired by:

- [https://github.com/ermongroup/SDEdit](https://github.com/ermongroup/SDEdit) (SDEdit: Guided Image Synthesis and Editing with Stochastic Differential Equations)
- [https://github.com/ermongroup/ddim](https://github.com/ermongroup/ddim) (Denoising Diffusion Implicit Models)

