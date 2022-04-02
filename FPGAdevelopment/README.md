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

To perform the neural network training correctly, it is necessary to use the environment that Xilinx offers us for AI adapted to models which runs on Ubuntu.

If you had some problem following the most up to date documentation might be in order: https://github.com/Xilinx/Vitis-Tutorials/blob/2021.2/Getting_Started/Vitis/Part2.md


You have to get an image just like this one to se that you have everything set up correctly!

Additional tips:

-Yes, the Varium C1100 is NOT an ARM device, treat it like an Alveo Data analytics card.
-Do the Install on Linux, Ubuntu 20.4 LTS in my case.
-The XRT environment is ALWAYS needed
-Install in the order provided.


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

What would change is dowloading everything to Varium C1100 

Remember that I told you you need to have OpenCL perfectly installed on your Workstation? If not everything will collapse at this point requiring a full install.

Follow his guide for that from this point:

https://docs.xilinx.com/r/en-US/ug1393-vitis-application-acceleration/Building-and-Running-the-Application

And read this one to understand what is happenning:

https://github.com/Xilinx/Vitis-Tutorials/blob/2021.2/Getting_Started/Vitis/Part4-data_center.md

Some Best Practices:

https://docs.xilinx.com/r/en-US/ug1393-vitis-application-acceleration/Best-Practices-for-Acceleration-with-Vitis

And some examples that you might want to test (not all work on the Varium card)
https://github.com/Xilinx/Vitis_Accel_Examples


# Final remarks

The next step we thought for this project, that regretably requires probably half a year to develop is actually to run IPFS or Arweave infrastructure through this Varium C1100 powered workstation. But, to do that while the workstation is a Flux Node and we can select it from a Flux service. That would be "next level" as you have a Blockchain based algorythm running through a cloud based FPGA-powered workstation having complete decentralization. As we know IPFS now is the backbone of NFTs and some of the Metaverse so having that would be in essence incredible and the true future for these applications.  

For now we have a complete suite of FPGA-powered services that a user can choose to accelerate via Flux cloud infrastructure and powered by an Aurora-Near EVM.

Hopefully you liked it!









