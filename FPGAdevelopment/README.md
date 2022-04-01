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

Then upload that bitstream to our Workstation already prepared with the Varium C1100 and run it.
Of course, the acceleration of said application was immense in comparison with other boards or machine with just a processor.










