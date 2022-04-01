# Decentralized Cloud Accelerator

Accelerating Blockchain Transfer System on Flux Using the Xilinx Varium C1100 FPGA.

<img src="https://i.ibb.co/RB0zZ3G/logo.png" width="500">

# Prologue: The Merge is coming
https://ethereum.org/en/upgrades/merge/

One if not the main selling point of the Varium C1100 board is that it is an excepcional performer in accelerating Blockchain applications such as algorythm acceleration, transaction validation and all around what we call "mining". Both of our boards are mining at about 70+Mh/s each and around only 100W at the wall each which outperform many of the top GPUs used today to mine Ethereum.

<img src="https://hackster.imgix.net/uploads/attachments/1429520/image_toKS7hWQWh.png?auto=compress%2Cformat&w=740&h=555&fit=max">

And let's be frank, nowadays the only coin that is profitable to mine is Ethereum, other blockchains are not offering the same incentives as ETH and all that is just about to end.

The Merge is coming and all Proof of work activities will cease altogether including Hardware mining. Making ETH a validator chain only.

<img src="https://hackster.imgix.net/uploads/attachments/1429531/image_zE4Et8uCJZ.png?auto=compress%2Cformat&w=740&h=555&fit=max">

When is it happening? Well, they say:

<img src="https://hackster.imgix.net/uploads/attachments/1429533/image_xb5rlvs9Bk.png?auto=compress%2Cformat&w=740&h=555&fit=max">

This might be delayed as some ETH upgrades have been in the past, but I wouldn't bet on that that much.

We could say, what is the problem? We can just develop on other chain and just reap the benefits there. Well there is NOT a single PoW (apart from Bitcoin) in the top 10.

And of the PoW ones there are only three other candidates for FPGA mining which are ERGO, Ravencoin and ETC all without the dividends that ETH has.

There are others like Flux that have anti-FPGA mechanisms and most of the top PoW ones depend on ASICS to do their mining and FPGAs have no business there. Other alternative would be to use it to accelerate Hedera, IPFS and some others, but after some research we found that this application is not really substantiated and it is remakably rare.

Then, what now? Will my sparkling new Varium C1100 work great for a couple months and later become an expensive paperweight?

<img src="https://hackster.imgix.net/uploads/attachments/1429544/image_5yaGzwIasR.png?auto=compress%2Cformat&w=740&h=555&fit=max">

I don't think so, let us offer an alternative...a Web3 based alternative.

# Chapter 0. How to mine on teamredminer...using the last few months till the merge.
Anticipating that many other submissions to this challenge will use the official Xilinx documentation to mine Ethereum we will showcase an alternative to that with two Varium C1100 boards as we each received one.
You can find instructions for that here: https://github.com/xilinx/blockchainacceleration

This to emulate a common GPU-like miner setup that in essence makes use of the proprietary tools that the ecosystem has produced, namely applications such as HiveOS and some others to manage a mining farm.

Let's be realistic, there's no medium to large mining operation that will use a custom program and bitstreams to farm as it becomes increasingly difficult to mine and coordinate all the farm with just a few FPGA in their operation (also considering that they have a 52 week backorder as of the 31st of March 2022). What is better is just to connect their Varium C1100 boards to Hive OS and use the only available bitstream that has support with those kind of tools which is TeamRedMiner: https://github.com/todxx/teamredminer/releases

Now, let's go step by step on how to configure that.

This will be for an AMD-based system running Ubuntu.

Of course it might be easier on windows, but as Vitis/Vivado requires a great deal of RAM and a linux based system to run, we decided to go for Ubuntu.

1. Install Ubuntu and the proper Drivers

You can install Ubuntu on a partition of your Hard Drive or another Hard Drive I decided the latter to avoid any misconfigurations for my system.

You can follow this guide for that:

https://www.youtube.com/watch?v=CWQMYN12QD0

Now that you have Ubuntu installed the next steps are the MOST IMPORTANT.

Go ahead and install all necessary upgrades and reboot your system.

Then go ahead to Terminal and update further just in case

sudo apt-get update 
sudo apt-get upgrade

If you have an AMD GPU then go to this page and search the EXACT model of your GPU. I have to stress this or else you will not be able to mine! In my case it was the RX6700xt

https://www.amd.com/en/support

<img src="https://hackster.imgix.net/uploads/attachments/1429446/image_GiYFoq6yOp.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Click submit and download the driver for Ubuntu 20.4 LTS

Now you can go to Terminal and extract it or just go to your folder and extract it there.

Go to terminal and navigate to that repository.

And now follow these instructions, what we are maily looking to install is OpenCL:

https://amdgpu-install.readthedocs.io/en/latest/install-installing.html

<omg src="https://hackster.imgix.net/uploads/attachments/1429482/image_tKAROboFpw.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Then go to Installing the Workstation use case:
  
<img src="https://hackster.imgix.net/uploads/attachments/1429483/image_HuQeoymf5z.png?auto=compress%2Cformat&w=740&h=555&fit=max">

And type this command into your terminal:

$ amdgpu-install --usecase=workstation -y --vulkan=pro --opencl=rocr,legacy
Wait for some minutes till the install is complete and reboot your system.

Install clinfo and allow render and video on your profile:

$ sudo usermod -a -G render $LOGNAME 
$ sudo usermod -a -G video $LOGNAME 

$ sudo apt-get install clinfo
Reboot again

Go to terminal again and type:

$ sudo clinfo
There you shoud see that OpenCL is installed so everything should be working correctly.

If you installed the wrong version of the AMD driver for your graphics card everything would have failed and you need to reinstall Ubuntu regretfully or recover its system to a factory install.

If you succeeded then let's install Teamredminer as it is the only integration-compatible miner with support for the Varium C1100.

Go to: https://github.com/todxx/teamredminer/releases

And download the latest Linux release. Extract that package.

That is most of the work done on the software side now let's talk Hardware.

Fistly you need a workstation/server/mining rig with the minimal requirements for the Varium C1100:
  
<img src="https://hackster.imgix.net/uploads/attachments/1429496/image_QL6Ml3rNy4.png?auto=compress%2Cformat&w=740&h=555&fit=max">

I.E. the most stringent requirements are a machine with minimum 64GB of RAM if you are going to develop bitstreams, 1 PCIE lane, and that's pretty much it, most other systems will have the other requirements.

Second, depending on your situation you will need some way of handling thermals.

I say this with a lot of love, the Varium C1100 is extraordinarily well put together and its design is superior to almost any GPU in what it does. But, the Thermals are not good. Several users and in some Discords and forums have reported this and even went ahead and changed the Heatsink and Thermal paste/pads in order to improve this situation because the board is not designed to work outside a Server situation.

In our case we are going to emulate a "GPU mining rig" so to battle the thermal situation we will need a couple of Radial fans.

<img src="https://hackster.imgix.net/uploads/attachments/1429504/image_R40CpUTjON.png?auto=compress%2Cformat&w=740&h=555&fit=max">

These will be attached to the back of the Varium C1100.

In adition to that any Mining "rig" support such as the one we provide at the bottom is probably excelent for this application and we will need a couple Risers such as this one (link provided in "things"):

<img src="https://hackster.imgix.net/uploads/attachments/1429506/image_kh7olPWv0V.png?auto=compress%2Cformat&w=740&h=555&fit=max">

If you are only going to connect one board the you are set just go ahead and connect it to the Riser, if you need to connect several boards and you just have one PCIE slot on your workstation then get one of these:

https://www.amazon.com/dp/B092R64W2V

A PCIE splitter card that will allow you to connect several of them.

<img src="https://hackster.imgix.net/uploads/attachments/1429508/image_J0KkipdFJ0.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Now assemble everything. Depending on your PSU and situation you might need more splitter power cables and so forth.

Also if you don''t have a rig and have a 3D printer you can print the design I left you at the bottom of this tutorial:

https://www.youtube.com/watch?v=ngCzJ4ey_DQ  

Just one warning: avoid connecting anything through Sata, go always PCIE or Molex.

This is my setup:
  
<img src="https://hackster.imgix.net/uploads/attachments/1429571/20220331_160826_hvk50v5nYK.jpg?auto=compress%2Cformat&w=740&h=555&fit=max">

Video Recap:
  
https://www.youtube.com/watch?v=Azlqubo3aDc

Now let's try to mine:

Go to your terminal and navigate to the folder where you extracted Teamredminer, after that input a command such as this one where Address is your Ethereum address where you want to mine, I recommend a Metamask or Exodus. And choose the pool that's nearest to you, in my case it is an Ethermine US pool.

Video:

https://www.youtube.com/watch?v=6POWEaSibYg


That is the first part and that might be a complete project by itself, but remember THE MERGE IS COMING, and we need to find another kind of application for the boards or they will become paperweights.

For that, we think Web3 is the answer.

# Chapter 1. Web3 to the rescue: Decentralized cloud computing via Artic Protocol and Flux
Introduction and Problem

Computer vision is a field of artificial intelligence that trains computers to interpret and understand the visual world. Using digital images from cameras and videos and deep learning models, machines can accurately identify and classify objects and then react to what they “see.”

<img src="https://hackster.imgix.net/uploads/attachments/1429254/68747470733a2f2f6d69726f2e6d656469756d2e636f6d2f6d61782f3830302f312a38676d6761416b4664492d394f4859356341393378512e706e67.png?auto=compress%2Cformat&w=740&h=555&fit=max">

In fact, as the most mature field in modern AI, it is permeating every sector of the economy. The opportunities that automating visual capabilities bring endless market opportunities across every sector.

The global computer vision market size was valued at $9.45 billion in 2020, and is projected to reach $41.11 billion by 2030, registering a CAGR of 16.0% from 2020 to 2030.
  
<img src="https://hackster.imgix.net/uploads/attachments/1429255/68747470733a2f2f692e6962622e636f2f7a4e3843636e582f414d522e706e67.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Most AI and cloud providers nowadays such as Google Cloud, Amazon AWS, Azure and many others offer AI, Machine learning and also to some degree Computer Vision services in their repertoire. One of the recent moves of this industry has been into the adoption of Edge Computing as the demand for computer power increases. Edge computing is computing that takes place at or near the physical location of either the user or the source of the data. By placing computing services closer to these locations, users benefit from faster, more reliable services while companies benefit from the flexibility of hybrid cloud computing. Edge computing is one way that a company can use and distribute a common pool of resources across a large number of locations.

Edge computing is in use today across many industries, including telecommunications, manufacturing, transportation, utilities, and many others. The reasons people implement edge computing are as diverse as the organizations they support.

<img src="https://hackster.imgix.net/uploads/attachments/1429613/007798d1_wJsKP14MXa.jpg?auto=compress%2Cformat&w=740&h=555&fit=max">

The key areas that will be forever impacted by AI+Edge computing will be 5G, IoT and Self driving and vehicle communications.

The main issue with this field is that it is primordially in the hands of certain Big tech incumbents thus it is highly centralized.

We think Near through Aurora and Flux can provide us with the tools to launch a highly decentralized web3 service for Computer Vision with incentives for those who would run our “nodes”.

### Solution

So our plan is to create what we will call Decentralized AI infrastructure. By providing Decentralized Computer Vision services where you can mine through Edge Devices, employing Flux oracles and the Near-Aurora Blockchain. Thus, making it a true Web3 project.

<img src="https://hackster.imgix.net/uploads/attachments/1429704/image_lPhhlq8WTO.jpg?auto=compress%2Cformat&w=740&h=555&fit=max">


But first: What is Flux?

Flux markets itself as the New Web3 for a Decentralized Internet.

It is comprehensive suite of decentralized computing services and blockchain-as-a-service solutions. The Flux ecosystem consists of: Fluxnodes' decentralized infrastructure, FluxOS cloud operating system, Zelcore self-custody multi-asset wallet and blockchain app suite, and finally the Flux blockchain for on-chain governance, economics, and parallel assets to provide interoperability with other blockchains and DeFi access.

Flux provides the critical, high availability infrastructure for the New Internet. Projects and development teams are not forced to rely on the Flux blockchain to utilize FluxOS, so they have access to necessary infrastructure while maintaining all the unique properties of their own chains. Flux makes up one important piece of a well-balanced distributed computing portfolio focused on the next generation of the Internet.

<img src="https://hackster.imgix.net/uploads/attachments/1429309/image_PhKSFHWszG.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Whitepaper: https://fluxwhitepaper.app.runonflux.io/?_gl=1*15zg29o*_ga*MjAxNzAyNDY5MS4xNjQ2MTAwMTQ0*_ga_M3VPBDLWV7*MTY0ODc3NzM3MC40LjEuMTY0ODc3ODAzOS4zMQ..

Webpage: https://runonflux.io

The Varium C1100 will be used for this application primarily to run Flux Nodes as a very capable, high performing and hardware updatable server providing cloud infrastructure to the network like few servers do. But we also need our "offshoot" nodes that will perform the AI and Computer Vision. For that we had several options including the Nvidia Jetson Nano, Ultra96 board but we decided to take out a Xillinx ZCU104 board to stay on the FPGA thematic. Not to mention it is about 5 times more powerful for these applications.

<img src="https://hackster.imgix.net/uploads/attachments/1429275/image_iVpswlyGjw.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Hi, if you are a judge and want to review the AI model running in GoogleColab here are the notebooks.

https://colab.research.google.com/github/altaga/Artic/blob/main/Minner%20Jetson/Python%20AI/YoloV3.ipynb

To test the product follow this link:

https://www.articprotocol.online

If you need more help and to check our codebase go to Appendix I

All the Smart Contracts codebase (Near-Aurora and Flux) is at: https://github.com/altaga/Artic/tree/main/Contracts

How it's Built
This is the main schematic of our solution:

<img src="https://hackster.imgix.net/uploads/attachments/1429276/general.png?auto=compress%2Cformat&w=740&h=555&fit=max">

So the development has been done in three parts:

1. The Near-Aurora blockchain incentive infrastructure and service base:

The project will be named Artic so we will create a token called TIC to give monetary incentives to people who run our Jetson Nano based nodes. This will include the landing page, UI, Smart Contracts that will be linked to a Flux oracle and so forth. For now we are running a number of Jetson Nano Devices, each of them send to four different Smart contracts the results of their computations using Flux oracles and then this is fed into an Aurora Smart contract and later the main UI.

Here is the landing page:

<img src="https://hackster.imgix.net/uploads/attachments/1429277/ui1.png?auto=compress%2Cformat&w=740&h=555&fit=max">

The AI service (Notice the four computations that come from four contracts each):

<img src="https://hackster.imgix.net/uploads/attachments/1429278/ui2.png?auto=compress%2Cformat&w=740&h=555&fit=max">

And a temporal Faucet for you to test the system:

<img src="https://hackster.imgix.net/uploads/attachments/1429279/token2.png?auto=compress%2Cformat&w=740&h=555&fit=max">

You can pay for AI services in this other screen through Metamask:

<img src=""https://hackster.imgix.net/uploads/attachments/1429280/pay2.png?auto=compress%2Cformat&w=740&h=555&fit=max>

You can see all the Aurora-based smart contracts that run on this layer here, including the ones that come from Flux oracles: https://github.com/altaga/Artic/tree/main/Contracts

Now, while we are speaking about flux...

2. Flux Infrastructure.

This infrastructure runs then from the Edge device all the way to Flux oracles and ends with the Aurora Smart contract.

Jetson Nano:

<img src="https://hackster.imgix.net/uploads/attachments/1429281/ai.png?auto=compress%2Cformat&w=740&h=555&fit=max">

ZCU104:

<img src="https://hackster.imgix.net/uploads/attachments/1429282/ai2.png?auto=compress%2Cformat&w=740&h=555&fit=max">

On our AI service page you can see one of our oracles feeding their contract in real time, you can check all of this directly in the Aurora Explorer.

In this case this oracle obtains its data from the edge processing of images in a jetson nano and ZCU104 through the YoloV3 model, this is a practical example of how the oracle could be fed with an AI model.

<img src="https://hackster.imgix.net/uploads/attachments/1429283/ui2.png?auto=compress%2Cformat&w=740&h=555&fit=max">

3. Edge Device running Machine Learning CV services.

We are using two Jetson Nanos and one ZCU104 to run these services and for this PoC they are running a YoloV3 image classification algorithm that has several use cases including automotive applications.

This is a mini demo of this application:
  
https://www.youtube.com/watch?v=yygXL4Zh7i4


ZCU104 Demo:

https://www.youtube.com/watch?v=Y-GctH4aNCE

You can go to this section to see several inference models and how it would be used:
https://github.com/altaga/Artic#appendix-ii

Let's see a hype demo of this solution:

https://www.youtube.com/watch?v=_Ww-3GVH3r4

# Chapter 2. The Varium C1100 as a high performing and hardware updatable Server for Web 3..the future for the Varium C1100
Now for the last part of this project and the best application we could find for the Varium C1100 board.

What we will try to do now is to run the workstation as a Flux Node that will be upgradable via the FPGAs that it has in its interior. This makes it quite more powerful and also an incredible tool for anyone trying to not only use an FPGA via cloud but as a way to expand the capabilities of cloud servers.

What is our angle with this and why does it is important?

Well, several companies have begun to attach FPGAs to their servers from a couple years ago till now and most of them think it is the future of Cloud computing and we agree!

https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-fpga-web-service

<img src="https://hackster.imgix.net/uploads/attachments/1429561/image_3Bfgzr8Ivo.png?auto=compress%2Cformat&w=740&h=555&fit=max"> 

And another one.

<img src="https://hackster.imgix.net/uploads/attachments/1429563/image_ndkEYJVdKd.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Well we can infer from the picture above that Xilinx is already on the move for this one and understands it.

We envision a future in which we will have the Centralized clouds such as AWS (let's be realistic) but not all the cloud computing needs for the future at the rate that we are growing in population can be solved by centralized services and there's where Decentralized Clouds like Flux and Akash enter.

They can solve those side issues and alleviate some of the bandwitdth that AWS and others may consume.

Now that we saw in Chapter 1 how to connect and configure an AMD workstation for these FPGAs, let's run a Flux node trough them.

Running a Flux Node

For that follow this documentation:

https://medium.com/@mmalik4/flux-light-node-setup-as-easy-as-it-gets-833f17c73dbb

Some tips and tricks:

- If the Benchhmark fails, it is your internet connection.

- Have more than 50Mb internet.

Here is my workstation running a Cumulus node which is quite overpowered for that application but well, I didn't have the collateral for a bigger one.

<img src="https://hackster.imgix.net/uploads/attachments/1429668/image_UBGaTBFiKq.png?auto=compress%2Cformat&w=740&h=555&fit=max"> 

Of course, for this application apart from running a Flux Cloud Node on our workstation we want to accelerate these application through our FPGA.

For that we need Vitis/Vivado installed on our workstation.

Just follow this documentation:

https://www.hackster.io/prithvi-mattur/big-data-analytics-935e3a

Xilinx offers ample documentation on how to use Vitis, so I can be brief on that:

https://www.xilinx.com/video/software/vitis-unified-software-platform-accelerated-libraries.html

<img src="https://hackster.imgix.net/uploads/attachments/1429671/image_7xriuXZyR0.png?auto=compress%2Cformat&w=740&h=555&fit=max">

Here we provide an example of how one of these Vitis Libraries can be used for a server AI acceleration application that can later be changed to any other application thanks to the power of FPGAs:

https://github.com/EddOliver/DecentralizedCloudAccelerator/tree/main/FPGAdevelopment

Summary and Foreword
So, after all that let's go part by part.

Prologue: we emphasized our reasons to switch from mining Ethereum to more Cloud based applications as all the other alternatives are not consequential for miners or cloud developers alike.

Chapter 0: We showed how to mine ETH using teamredminer and to arrange a setup that everybody may have access two, no servers, no difficult to obtain parts (with exceptions, namely the boards).

Chapter 1.: Showcase of our Decentralized Cloud AI solution with UI, UX and it is live on Aurora Testnet and Flux! We also explained Flux and how it is changing how we perceive Cloud solutions.

Chapter 2: How the FPGA on the Xilinx C1100 can go from a miner accelerator to an AI cloud provider via Flux nodes and through Vitis how that can be renewed each time a new application arises.

After all that we can see how that is the way to go forward, naturally we think that a utility proposition such as the one we can have through Flux and the use of powerful FPGAs such as the Varium C1100 is much better than only being a transaction Validator and solving cryptographic Proof of Work algorithms. To use the FPGAs integrated in a workstation as a server to solve difficult AI, fluid dynamics or any other kind of problem that require flexible computation is a much more fulfilling way to see the future of these technologies and in essence we think that it is also a way for Xilinx to continue the path they already were treading. Of course, centralized cloud platforms such as AWS are here to stay. But with the population that will require cloud computing in the years to come growing exponentially more now than ever Decentralized alternatives are needed and Xilinx can provide that edge through devices such as the Varium C1100!

Hopefully you liked the project, it was great building with the Xillinx Varium C1100.

References:
https://www.sas.com/en_us/insights/analytics/computer-vision.html

https://www.precisionag.com/digital-farming/how-computer-vision-is-fast-becoming-the-backbone-of-next-generation-agronomy/

https://www.alliedmarketresearch.com/computer-vision-market-A12701#:~:text=The%20global%20computer%20vision%20market,around%20it%20just%20like%20humans.

https://runonflux.io

https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-fpga-web-service

https://github.com/xilinx/blockchainacceleration

https://www.datacenterknowledge.com/edge-computing/why-microsoft-betting-fpgas-machine-learning-edge

https://www.xilinx.com/products/design-tools/acceleration-zone/aws.html

