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
``bash
sudo chmod a+x NVIDIA-Linux-x86_64-384.111.run
sudo gedit /etc/modprobe.d/blacklist.conf 
``
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
