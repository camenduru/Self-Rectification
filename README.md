# Generating Non-Stationary Textures using Self-Rectification

> **Generating Non-Stationary Textures using Self-Rectification**<br>
> Yang Zhou<sup>1</sup>, Rongjun Xiao<sup>1</sup>, Dani Lischinski<sup>2</sup>, Daniel Cohen-Or<sup>3</sup>, Hui Huang<sup>1</sup><br>
>
>  <sup>1</sup>Shenzhen University, <sup>2</sup>The Hebrew University of Jerusalem, <sup>3</sup>Tel Aviv University

>**Abstract**: <br>
>This paper addresses the challenge of example-based non-stationary texture synthesis. We introduce a novel two-step approach wherein users first modify a reference texture using standard image editing tools, yielding an initial rough target for the synthesis. Subsequently, our proposed method, termed "self-rectification", automatically refines this target into a coherent, seamless texture, while faithfully preserving the distinct visual characteristics of the reference exemplar. Our method leverages a pre-trained diffusion network, and uses self-attention mechanisms, to gradually align the synthesized texture with the reference, ensuring the retention of the structures in the provided target. Through experimental validation, our approach exhibits exceptional proficiency in handling non-stationary textures, demonstrating significant advancements in texture synthesis when compared to existing state-of-the-art techniques.

## Description

This repo contains the official code and data for our paper [Self-Rectification](https://arxiv.org/abs/2401.02847). 

## Setup

We implement our method with [diffusers](https://github.com/huggingface/diffusers) code base. The code runs on Python 3.10.13 with Pytorch 2.0.1. Conda environment is highly recommended.

```shell
pip install -r requirements.txt
```

## Usage

To quickly get started, run the following command to generate the images shown in the teaser (Fig. 1) of our paper:

```shell
python main.py
```

To generate different results, you can modify the configuration section in the front of the `main.py` file:

```python
# ================================== change config here! ========================================
P1 = 20
P2 = 5
S1 = 20
S2 = 5

ref_images = torch.cat([
    load_image('./images/aug/203.jpg', 512, device),
    load_image('./images/aug/203-1.jpg', 512, device),
    load_image('./images/aug/203-2.jpg', 512, device),
    load_image('./images/aug/203-3.jpg', 512, device)
])
target_image = load_image('./images/tgts/203-2.jpg', 512, device)

out_dir = "./workdir/exp/"
# ================================== config end. ========================================
```

- `P1, P2, S1, S2`: the hyperparameters contained in our method.

- `ref_images`: the reference/example/source textures. 

- `target_image`: the target image user edited.

- `out_dir`:  the path where the results are saved.

### Data

The example textures we experimented with are provided in this repo. Some of them are collected from the work [TexExp](https://github.com/jessemelpolio/non-stationary_texture_syn), and others from the internet. Each of them was resized to 512×512 pixels as the reference/source texture. We built several different target images for each example in PhotoShop, which can be done quickly with just a few lazy edits. 

All the reference and target textures are provided in `./images/refs` and `./images/tgts`, respectively.  Some reference textures have augmentations, which are contained in `./images/augs`.

## Examples

Here we show some examples along with their para settings.

| No. | Reference | Target | Result | Setting                               |
| ---- | ----------------- | ----------------- | ----------------- | ----------------- |
| 6-1 | ![ref](./assets/6/ref.jpg) | ![target](./assets/6/target.jpg) | ![result](./assets/6/result.jpg) | P1=20, P2=15, <br />S1=20, S2=5.<br />augmentation:<br />6-1, 6-2, 6-3 |
| 203-1 | ![ref](./assets/203/ref.jpg) | ![target](./assets/203/target.jpg) | ![result](./assets/203/result.jpg) | P1=20, P2=5, <br />S1=20, S2=5.<br />augmentation:<br />203-1, 203-2, 203-3 |
| 3001-1 | ![ref](./assets/3001/ref.jpg) | ![3001-1](./assets/3001/target.jpg) | ![result](./assets/3001/result.jpg) | P1=20, P2=5, <br />S1=20, S2=5.<br />no augmentation<br /> |
| 5001-1 | ![ref](./assets/5001/ref.jpg) | ![result](./assets/5001/target.jpg) | ![result](./assets/5001/result.jpg) | P1=20, P2=5, <br />S1=20, S2=5.<br />no augmentation<br /> |



## Acknowledgements

The code is built upon [MasaCtrl](https://github.com/TencentARC/MasaCtrl). We sincerely thank for their great work.

## Cite

```
@misc{zhou2024generating,
      title={Generating Non-Stationary Textures using Self-Rectification}, 
      author={Yang Zhou and Rongjun Xiao and Dani Lischinski and Daniel Cohen-Or and Hui Huang},
      year={2024},
      eprint={2401.02847},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```

