# install-my-dep

it is for my PC of Thinkpad P51

1.install cuda
refer to
  https://blog.csdn.net/yhaolpz/article/details/71375762

0.install the nvidia driver from
system setting -> softupdate -> addional driver -> nvidia driver...

1. install basic deps
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libopenblas-dev liblapack-dev libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install git cmake build-essential

2. install & update ubuntu kernel(core)
sudo apt-get update
sudo apt-get dist-upgrade -y
sudo apt-get install linux-image-extra-virtual
sudo apt-get install linux-source

3.disable nouveau
sudo gedit /etc/modprobe.d/blacklist-nouveau.conf
#add the text in to file & save
blacklist nouveau option nouveau modeset=0 
#active the new setting of disable nouveau
sudo update-initramfs -u

4.update environment setting
sudo gedit ~/.bashrc
#add the text in to file & save
export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH 
#active the new setting
source ~/.bashrc

5.install cuda8.0
#down load runtime file from https://developer.nvidia.com/cuda-downloads.
#notice: select the old version of 8.0. not the new verison that is higher than 9.2
#type the keyboard & log in usieng DOS feature
Ctrl + Alt + F1
#disable the GUI, because the graph GUI is using GPU
sudo service lightdm stop
#run the cuda8 file which is just download.
#notice: the file name may not the same
#notice: we donot want to install opengl
sudo sh cuda_8.0.61_375.26_linux.run --no-opengl-libs
#after the long long loooooooooooooong text. 
accept
n (we install the nvida gpu driver from the setting, so donot install driver here)
y or enter (for last all)
#it finishs soon
reboot

6.update environment setting
sudo gedit ~/.bashrc
#add the text in to file & save
export PATH=/usr/local/cuda-8.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
#active the new setting
source ~/.bashrc

7.Test cuda using its sample
cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery
sudo make
./deviceQuery
