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
