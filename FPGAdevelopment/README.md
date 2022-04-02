# Xilinx Varium C1100 FPGA development through Vitis

Of course the better course of action here is to join the Xilinx Developer Program to have access to several training opportunities and content!

<img src="https://i.ibb.co/HCNQmMh/developerprogram.png">

You probably won't get the training sessions for the Adaptive computing Challenge, but all the training for Vitis and Vivado is great.

<img src="https://i.ibb.co/4sRRfdz/Vitissuite.png">

#### In essence we want to do exactly what Amazon is doing on that image, but for Decentralized cloud via Flux.

The amount of documentation to develop and run Vitis and Vivado is staggering but let's go to the basics.

#### If you followed Chapter 0 of the project, you already have a linux PC/Server/Machine with Ubuntu (a linux distro) and with the perfect configuration to start with Vitis and Vivado as you already have OpenCL installed!

And we also have to mention that if you folloed Chapter 1 you also have several examples of Machine learning examples (done on the ZCU104) that can also be adapted for the C1100 as a Cloud service.

https://colab.research.google.com/github/altaga/Artic/blob/main/Minner%20Jetson/Python%20AI/YoloV3.ipynb

These examples are for just YoloV3 Machine Learning algorithms, but that can be accelerated via the Vitis Vision Library.

What you need to do now is to set up Vitis and its environment.

Follow this set of tutorials, you can stop at number four.

<img src="https://i.ibb.co/G930vR1/vdev.png">

Once done that you can choose which Vitis Library would be perfect for your application (depending on your SoC it might not run appropriately, but in essence every board can handle it as long as Vitis supports it.

For example, for our application we would use the Vitis Vision Library found in this documentation:

https://xilinx.github.io/Vitis_Libraries/index.html

Then upload that bitstream to the Varium C1100 in our already set up workstation and run the example application that you wwant to accelerate.
Of course, the acceleration of said application was immense in comparison with other boards or machine with just a processor.

We have done a "guide" for Vitis development in the past, we are quite familiarized as we have now developed on vitis for years. Here is the excert from that that was allocated in this past project: https://github.com/altaga/Facemask-Detector-ZCU104

Of course it is heavily based on Xilinx's own documentation nevertheless here are the most important aspects:
-----------------------------------------------------------------------------------------------------------------

## **Train Environment Setup**

To perform the neural network training correctly, it is necessary to use the environment that Xilinx offers us for AI adapted to models focused on DPU which runs on Ubuntu 18.04.3.

http://old-releases.ubuntu.com/releases/18.04.3/

NOTE: ONLY IN THIS UBUNTU VEERSION IS ENVIROMENT COMPATIBLE, ONCE YOU INSTALL THE VIRTUAL MACHINE, DO NOT UPDATE ANYTHING, SINCE YOU WILL NOT BE ABLE TO USE THE ENVIROMENT AND YOU WILL HAVE TO INSTALL EVERYTHING AGAIN.

<img src="https://i.ibb.co/pnjvwMm/image.png" width="1000">

In my case I use a machine with Windows 10, so to do the training I had to use a virtual machine in VMware.

https://www.vmware.com/mx.html

Within the options to install the environment there is one to use the GPU and another CPU, since I use the virtual machine I will use the CPU installation.

https://github.com/Xilinx/Vitis-AI

Open the linux terminal and type the following commands.

In the Scripts folder I have already left several .sh files with which you can easily install all the necessary files, these files must be in the /home folder for them to work properly.

1. Install Docker (1 - 2 minutes) if you already have Docker go to Script 2.

        sudo bash install_docker.sh

2. Install Vitis (10 - 20 minutes).

        sudo bash install_vitis.sh

NOTE: install only one of the following ENV according to your preference.

3. Install CPU or GPU Support.

   - Installing CPU (20 - 30 minutes).

           sudo bash install_cpu.sh 

   OR

   - Installing the GPU environment (20 - 30 minutes).

           sudo bash install_gpu.sh
        
4. Start base Env.

        sudo bash run_env.sh

5. Start Vitis-AI-TensorFlow

        conda activate vitis-ai-tensorflow

6. Run this command once (IMPORTANT).
        
        yes | pip install matplotlib keras==2.2.5

<img src="https://i.ibb.co/yQ4qtXJ/image.png" width="1000">

If you did everything right, you should see a console like this one.

In the [Appendix A](#appendix-a) you can see the Scripts content.

## **Training the model**

To carry out the training, copy all the files inside the "Setup Notebook and Dataset" repository folder to the Vitis-AI folder for the code to run properly.

Just as in the picture.

<img src="https://i.ibb.co/zFyKSDM/image.png" width="1000">

Now in the command console we will execute the following command to open Jupyter Notebooks.

    jupyter notebook --allow-root

<img src="https://i.ibb.co/9n01Vhn/image.png" width="1000">

Open the browser and paste the link that appeared in the terminal and open the file.

<img src="https://i.ibb.co/Zd4ZLsQ/image.png" width="1000">

Once the code is open in the Kernel tab, it executes everything as shown in the image.

<img src="https://i.ibb.co/5K1xhmF/image.png" width="1000">

All the code is explained in detail. To understand it fully, please review it.

https://github.com/altaga/Facemask-Detector-ZCU104/blob/main/Setup%20Notebook%20and%20Dataset/train_facemask_model.ipynb

After the excecution, if everything worked well we should see the following result.

<img src="https://i.ibb.co/RvhDfpD/image.png" width="1000">

From this process we will obtain a file called "dpu_face_binary_classifier_0.elf".

This file has saved the model that we will use later and that has been already provided in the "Main Notebook" folder.

What would change is instead of dowloading everything to the ZCU104 now we deploy that into the Varium C1100 

The next step we thought for this project, that regretably requires probably half a year to develop is actually to run IPFS or Arweave infrastructure through this Varium C1100 powered workstation. But, to do that while the workstation is a Flux Node and we can select it from a Flux service. That would be "next level" as you have a Blockchain based algorythm running through a cloud based FPGA-powered workstation having complete decentralization. As we know IPFS now is the backbone of NFTs and some of the Metaverse so having that would be in essence incredible and the true future for these applications.  

For now we have a complete suite of FPGA-powered services that a user can choose to accelerate via Flux cloud infrastructure and powered by an Aurora-Near EVM.

Hopefully you liked it!









