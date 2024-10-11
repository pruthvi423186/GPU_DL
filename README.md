**Setting Up Your GPU for Deep Learning on Linux**
This guide helps you configure your NVIDIA GPU for deep learning on a Linux-based OS. Follow the steps carefully to avoid compatibility issues.

Before installing all the drivers cross verify with tensorflow installation
https://www.tensorflow.org/install/source  

Swipe down and you will find the comaptiblity chart
![image](https://github.com/user-attachments/assets/f2789e45-fd4d-4ef0-b404-eec1ad0fba29)


**Step 1: Verify That You Have a Dedicated GPU**
To check if your system recognizes your GPU, open the terminal and run:

$ nvidia-smi

****Example output:****
![image](https://github.com/user-attachments/assets/034c9340-7ea8-4867-93d0-bc136b0125dc)


If you have GPU and you have't isntalled the Driver yet here is the link   
https://www.nvidia.com/en-us/drivers/ 

Select GPU and Operating system 
Example:
![image](https://github.com/user-attachments/assets/8fb9d52e-7d9a-445c-8e1d-edd8ff80b1df)
![image](https://github.com/user-attachments/assets/1b1d0a16-2508-4d7b-804f-ea9a410051fe)

Again verify with **nvidia-smi** in terminal

**Step 2: Install CUDA**

Open terminal again type **nvidia-smi**

![Screenshot from 2024-10-11 14-09-40](https://github.com/user-attachments/assets/dee881db-d161-4395-b035-2a66147d19fa)

As you can see in the image you can find the compatible version of for my gpu and the driver version

**Link for CUDA:** https://developer.nvidia.com/cuda-toolkit-archive 

**Link for CUDA compatibility** : https://docs.nvidia.com/deploy/cuda-compatibility/ 

**Example** : ![image](https://github.com/user-attachments/assets/9224ac27-de16-43cf-b522-b93cb38fb45b)


Check tensorflow installation link to find which version you need and install required CUDA

**Example:** I am using Tensorflow 2.17 latest version and it is compatible with CUDA 12.3 
**Note: ** Don't go further than 12.3 because CUDA's latest version doesn't support Tensorflow. So, be precise about versions   

![image](https://github.com/user-attachments/assets/f2789e45-fd4d-4ef0-b404-eec1ad0fba29)

Now select required version from CUDA archives 

After redirecting to required version you will be asked for select to operating system 
1. Windows
2. Linux

As of we are working on Linux based OS 
![image](https://github.com/user-attachments/assets/7675b72b-2781-436d-80e9-480dace6b50a)

Select appropriate OS then you can find repositories below


**Example commands to install CUDA12.6** : 

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin

sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600

wget https://developer.download.nvidia.com/compute/cuda/12.3.0/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb

sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb

sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/

sudo apt-get update

sudo apt-get -y install cuda-toolkit-12-3


**Note**: wget https://developer.download.nvidia.com/compute/cuda/12.3.0/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb 

In above command line you can find **cuda-repo-ubuntu2204-12-3-local_12.3.0-545.23.06-1_amd64.deb** 

**Cuda repository ubuntu 22.04** (OS and it's version)

**local_12.3.0** (CUDA version)

**-545.23.06-1_amd64.deb** (Your driver compatibility) which means you can isntall this CUDA even though if you have a higher version of GPU driver 

**CUDA 12.x >=525.60.13**

**Note**: Be specifi about your GPU driver and CUDA version at the same time otherwise there will compatible issues


**Step 3: Downloading cuDNN** 

Again verify with the tensorflow installation link 

**Example**: If I have CUDA version of **12.3.0** I have to choose cuDNN version of **8.9**

Here is the link cuDNN files

https://developer.nvidia.com/rdp/cudnn-archive

Select the appropriate version and download the archive files  and extract them 

Now, you will have the cuDNN file. Inside the file you will find files name with **lib**, **bin** etc... 

Copy every file inside lib and bin etc.. paste them in CUDA directories lib and bin 

If everything installed well enough, open terminal and type this command 

**nvcc --version**

**Output**

pruthvi@Pruthvi:~$ **nvcc --version**

nvcc: NVIDIA (R) Cuda compiler driver

Copyright (c) 2005-2023 NVIDIA Corporation

Built on Fri_Sep__8_19:17:24_PDT_2023

Cuda compilation tools, release 12.3, V12.3.52

Build cuda_12.3.r12.3/compiler.33281558_0


**Note**: If you want to use CUDA you have choice that you can use it for global environment. 

**Install tensorflow**

**Step 1**: First create python virtual environment 

 ![image](https://github.com/user-attachments/assets/f2789e45-fd4d-4ef0-b404-eec1ad0fba29)
 
 check out the python versions with tensorflow before you create a python VE

 Go to terminal and enter this command 

**python -m venv tf**        Will create a python VE
 
**source tf/bin/activate**   Activate your VE

**pip install tensorflow**   Install tensorflow (Directly install latest version)

**pip install tensorflow==<version>** If you are much specific about version 


Now let's check whether the setup is confifured successfully or not

Activate your python VE using this command 

**source tf/bin/activate**  (If you are already in your VE then no need to run this command)

enter command **python**(You will be in python shell after entering this commnd)

And paste this pyhton code one by one line or you could use nano to write this code

import tensorflow as tf 
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))

**Output**
**Num GPUs Available:  1**

**Note**: Be specific about your installing versions because you are playing with GPU drivers as an administrator. So, a slight version of drivers overlap could cause severe damage to your root files and operating system, Just an advice with personal experience

I have attached a ipynb file to show you the difference between CPU and GPU performace when it comes to DL models

https://github.com/pruthvi423186/GPU_DL/blob/main/GPU_vs_CPU.ipynb

 
There you go you have installed everything required to use your GPU as main computing device for your DL code 

Thank you for approching the document

Any issues regarding installation
pruthvigundrathi2000@gmail.com 



