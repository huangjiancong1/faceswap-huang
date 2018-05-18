# faceswap-huang

## computer
```bash
ubuntu 14.04
nvidia-1050TI
```
## software
```bash
CUDA 8.0
CUDNN 6.0
python 3.5
ipython
opencv 3.3
tensorflow-gpu 1.4
pathlib==1.0.1
scandir==1.6
h5py==2.7.1
Keras==2.1.2
opencv-python==3.3.0.10
scikit-image
dlib
face_recognition
tqdm
matplotlib
```
## install
### CUDA 8.0
download GPU driver run.file http://www.geforce.cn/drivers
my GPU use runflie: NVIDIA-Linux-x86_64-384.111.run
```bash
sudo chmod a+x NVIDIA-Linux-x86_64-384.111.run
sudo gedit /etc/modprobe.d/blacklist.conf 
```
append `backlist nouveau`in the end
```bash
sudo apt-get --purge remove xserver-xorg-video-nouveau
sudo reboot
sudo apt-get --purge remove nvidia-*
sudo init3
sudo /etc/init.d/lightdm stop
```
crtl+alt+F3
Enter username and password
```bash
sudo su
cd /home/usrname/
./NVIDIA-Linux-x86_64-384.111.run -no-x-check -no-nouveau-check -no-opengl-files
```
than perform operations `accept>continue install>Yes>ok.....`
```bash
sudo /etc/init.d/lightdm start
sudo apt-get install mesa-utills
```
Check whether your gpus can be installed with CUDA.
```bash
lspci | grep -i nvidia
```
Check whether your gpus can install CUDA.
```bash
 uname -m && cat /etc/*release
```
Verify whether the operating system installed the GCC
```bash
gcc -v
```
Install the CUDA Toolkit(deb local)
download cuda-repo-ubuntu1404-8-0-local-ga2_8.0.61-1_amd64.deb from https://developer.nvidia.com/cuda-downloads
```bash
sudo dpkg -i cuda-repo-ubuntu1404-8-0-local-ga2_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```
After the installation is complete, declare the environment variable and write it to the end of ~/.bashrc.
`export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}` 
`export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`
```bash
source ~/.bashrc
```
Then set the environment variable and the dynamic link library in the command line input
```bash
sudo gedit /etc/profile
```
Add at the end of the open file
```bash
export PATH=/usr/local/cuda/bin:$PATH
```
After saving, create the link file.
```bash
sudo gedit /etc/ld.so.conf.d/cuda.conf
```
Add at the end of the open file
```bash
/usr/local/cuda/lib64
```
```bash
sudo ldconfig
```
test suda Samples
```bash
cd /usr/local/cuda-7.5/samples/1_Utilities/deviceQuery
make
sudo ./deviceQuery
```
### CUDNN 6.0
download  cudnn 6.0 (cudnn-8.0-linux-x64-v6.0.tgz) in https://developer.nvidia.com/rdp/cudnn-download
extract the tgz file 
entry the include file in the extacted file
```bash
sudo cp cudnn.h /usr/local/cuda/include/ 
```
entry the lib64 file in the extacted file
```bash
sudo cp lib* /usr/local/cuda/lib64/ 
```
then
```bash
cd /usr/local/cuda/lib64/
sudo rm -rf libcudnn.so libcudnn.so.6           
sudo ln -s libcudnn.so.6.0.21 libcudnn.so.6     
sudo ln -s libcudnn.so.6 libcudnn.so            
```
check the cudnn version
```bash
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
```
### python 3.5
note: never remove the python3 or python2 which already in your system
```bash
sudo add-apt-repository ppa:fkrull/deadsnakes  
sudo apt-get update  
sudo apt-get install python3.5 
```
Cancel the original Python 3.4 and link Python3 to the latest 3.5.
```bash
sudo mv /usr/bin/python3 /usr/bin/python3-old  
sudo ln -s /usr/bin/python3.5 /usr/bin/python3 
```
install newest pip3 and ipython
```bash
wget https://bootstrap.pypa.io/get-pip.py  
sudo python3 get-pip.py  
sudo pip3 install setuptools --upgrade  
sudo pip3 install ipython[all] 
```
optional: switch back to the link file
```bash
sudo rm /usr/bin/python3  
sudo mv /usr/bin/python3-old /usr/bin/python3  
```
### opencv-3.3.0
download opencv 3.3.0 in https://opencv.org/releases.html
unzip opencv-3.3.0.zip file
```bash
cd opencv-3.3.0 
sudo apt-get install build-essential libgtk2.0-dev libvtk5-dev libjpeg-dev libtiff4-dev libjasper-dev libopenexr-dev libtbb-dev
mkdir build && cd build 
cmake -D CMAKE_BUILD_TYPE=RELEASE -D WITH_TBB=ON  -D WITH_V4L=ON -D CMAKE_INSTALL_PREFIX=/usr/local/opencv330 .. 
```
or
```bash
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local/opencv330 PYTHON3_EXECUTABLE = /usr/bin/python3 PYTHON_INCLUDE_DIR = /usr/include/python3.5m PYTHON_INCLUDE_DIR2 = /usr/include/x86_64-linux-gnu/python3.5m PYTHON_LIBRARY = /usr/lib/x86_64-linux-gnu/libpython3.5m.so PYTHON3_NUMPY_INCLUDE_DIRS = /usr/local/lib/python3.5/dist-packages/numpy/core/include/ ..
make 
sudo make install  
sudo gedit ~/.bashrc 
```
Add at the end of the file
```bash
 export PKG_CONFIG_PATH=/usr/local/opencv330/lib/pkgconfig  
 export LD_LIBRARY_PATH=/usr/local/opencv330/lib  
```
save and
```bash
source ~/.bashrc 
pkg-config --modversion opencv 
```
use in python3
```bash
sudo pip3 install opencv-python==3.3.0.10
```
### Tensorflow-gpu 1.4
```bash
pip3 install --upgrade tensorflow==1.4
```
test
```bash
python3
>>import tensorflow as tf
```
without any error
### dlib 
download dlib package in http://dlib.net/ ,any version can.
```bash
cd /dlib-19.10/examples
mkdir build
cd build
cmake ..
cmake --build . --config Release
cd ../../
wget https://bootstrap.pypa.io/ez_setup.py -O - | sudo python
sduo python3 setup.py install
```
### Other package
```bash
sudo pip3 install pathlib==1.0.1
sudo pip3 install scandir==1.6
sudo pip3 install h5py==2.7.1
sudo pip3 install Keras==2.1.2
sudo pip3 install scikit-image
sudo pip3 install face_recognition
sudo pip3 install tqdm
sudo pip3 install matplotlib
```
