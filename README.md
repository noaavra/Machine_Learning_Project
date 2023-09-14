# Machine Learning for Novel X-ray Imaging
**Authors: Mor Shy & Noa Avrahamov**

Welcome to our project focusing on reconstruction of images from X-rays captured by Computational Ghost Imaging (CGI) method, using deep learning.
In this project, we used the neural network DAttNet with deep learning algorithms to try to improve the reconstruction of the images.
Our goal is to improve the resolution of the reconstructed images of the new X-ray method.

# Installation
### Datasets
We used the coco dataset, which you can download from [here](https://cocodataset.org/#download).
Please refer to the dataset's documentation for usage terms, licensing, and any specific instructions provided by the dataset creators.

The coco dataset we used - for training and testing - is already uploaded to a storage bucket in the Google Cloud Platform, called `our_train_test_data`.
This bucket holds the datasets, the loaders (generated data from previous runs) and the results (the reconstructed images) of previous runs.

We also used the Mnist dataset. In order to download it (locally in the folder of the code), change the following lines in the function load_data_mnist in the code:
```
train_data = datasets.MNIST(root='data', train=True, download=True, transform=transform)
test_data = datasets.MNIST(root='data', train=False, download=True, transform=transform)
```
### Packages Required
Install the required python packages using the command:
```
pip install matplotlib numpy opencv-python fiftyone wandb google-cloud-storage
pip install torch==1.12.1 torchvision==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu113
pip install torchaudio==0.12.1 --extra-index-url https://download.pytorch.org/whl/cu113
```
### Code Parts
Our project consists of a few distinct code parts, each contained in its respective section:
1. **DattNet:** This section sets the neural network DAttNet for this code.
2. **Data Generation:** This section contains the code for uploading the datasets, and performing the necessary calculations on the datasets before the training.
3. **Log and Support:** These sections contain various support functions such as hitogram-equalization, and logging function.
4. **Training and Testing:** These sections hold the codes for the training and testing of the model, respectively.
5. **Parameters:** In this section there is a function that gets all the parameters that can be modified for a specific run.
6. **Main:** This section holds the main function and the sweep command.

# How to Use
### Start a Run
To run the code as a single run (and not a sweep), follow these steps:
1. Open the `DattNet_code_13_09_23_version.ipynb` file located in the main folder.
2. Within the `Parameters section` section, you can experiment with various parameters directly (learning rate, number of epochs, which datasets to use and more)
3. In the penultimate code section of the code, comment the sweep command in the following way to run the main:
```
%%capture output

if __name__ == "__main__":
    main()

# wandb.agent(sweep_id="noaavra/DattNet/x2w9ltj4", function=main, count=2)
```
### Using W&B
In order to see the graphs and logged output images of the runs, you need to sign up to Weights & Biases.
Then, log in using the API of your W&B account and the commands:
```
import wandb
wandb.login()
```
In order to run a sweep instead of a single run, change back the penultimate section of the code:
```
%%capture output

# if __name__ == "__main__":
#     main()

wandb.agent(sweep_id="noaavra/DattNet/x2w9ltj4", function=main, count=2)
```
- Don't forget to update the path to match your username and the sweep ID you use, so instead of `noaavra/DattNet/x2w9ltj4` you should have `your-username/DattNet/sweep-ID`.
- You can change the `count` parameter to match the number of runs you want in the sweep.

### So What Is Left To Do
We left throught the code a few `TODO` comments, explaining the reamining bugs and problems to fix.

Other than that, you should continue running sweeps using W&B, in order to find the right parameters (such as learning rate and number of epochs) for the runs, that will get better results.

GOOD LUCK!
