# EG3D latent code regressor

Given a single-view face image, our regressor model predicts the intermediate latent code w of the EG3D generator model. The predicted latent code - w with shape (14, 512), is then fed to the EG3D pipeline, to generate/reproduce the initial input face image. The aim of our regressor model, is to reproduce exactly the real input face image, by predicting the correct intermediate latent code - w. By directly regressing, the EG3D latent code, our method, offers a faster alternative to EG3D GAN inversion methods such as [PTI-inversion](https://github.com/danielroich/PTI). This way, by leveraging our regressor, any face image, can be directly reproduced by EG3D, by generating at the same time the corresponding depthmap and 3D mesh, with an impressive time speedup. Furthermore, the regressor, predicts latent code, which allows for further latent code interpolation, leading to novel pose, expression synthesis for any input face image. An example method for disentagling semantic features from latent code and moving along specific semantic directions in a high dimensional latent space (e.g smile direction), can be found [here](https://arxiv.org/pdf/2005.09635.pdf). 

<img src="https://github.com/cantonioupao/eg3d-code-regressor/blob/main/assets/latent_regressor.png" alt="drawing" />

In the overview of the pipeline, our latent code regressor is depicted. In essence, our model, inputs a face image and predicts the EG3D intermediate latent code - w. If the prediction is correct, when the code - w is fed in the EG3D pipeline, the exact same image is reproduced/generated. In our work, we trained mainly 2 model architectures, a Vision Transformer - [ViT]() and a unified version of the classical [UNET]() model, termed as UNET-modified. A visualization of both model arcitectures can be found [here]() and [here]() respectively. Both model architectures are trained on a synthetic training dataset of 50000 samples, by optimiying an l1-loss between the predicted and ground truth latent codes - w. The distribution of our training set, can be seen below. More details about the training dataset and the method for generating the face images can be found [here](https://github.com/cantonioupao/generate-synthetic-face-data)
![eg3d_training_dataset](https://github.com/cantonioupao/generate-synthetic-face-data/blob/main/assets/eg3d_synthetic_training.png). Both models, achieve a similar latent code reconstruction performance. All the relevant code, instructions and general interactive guide for training, testing and evaluating our models, can be found in the respective google colab notebooks.

Below you can find the relavant notebooks:
| Description      | Link |
| ----------- | ----------- |
| :point_right: $\color{red} ViT$ latent regressor training | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cantonioupao/eg3d-code-regressor/blob/main/colab_notebooks/vit_latent_code_training.ipynb)|
| :point_right: $\color{blue} UNET-modified$ latent regressor training | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cantonioupao/eg3d-code-regressor/blob/main/colab_notebooks/unet_latent_code_training.ipynb)|
|  :star: **Evalution**: Test custom input on both models (regressor + EG3D + 3D mesh) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cantonioupao/eg3d-code-regressor/blob/main/colab_notebookslatent_code_regression.ipynb)|
|  :smile: EG3D latent code interpolation | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cantonioupao/eg3d-code-regressor/blob/main/colab_notebooks/latent_code_interpolation.ipynb)|



This repository is inspired by the EG3D [paper](https://nvlabs.github.io/eg3d/media/eg3d.pdf) and uses the codebase from [EG3D](https://github.com/NVlabs/eg3d). Please refer to the [project's webpage](https://arxiv.org/pdf/2112.07945.pdf) for more information.

Some of the results on synthetic and real data can be shown below. Both models perform comparably, resulting to some robust predictions. Neverthless, for real face images, there is some deviation from the original images, as shown below. The following [repository](https://github.com/cantonioupao/generate-synthetic-face-data), is being leveraged, to invert a large number of real images, and further fine-tune our regressor models, with real data, by obtaining the respective latent codes, for real face images. 

![results](https://github.com/cantonioupao/eg3d-code-regressor/blob/main/assets/regression_results.png)

More results, soon... :soon:





