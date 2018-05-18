# faceswap-huang

# computer
```bash
ubuntu 14.04
nvidia-1050TI
```
# software
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
# install
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
### Other package with python3
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
### FFmpeg
FFmpeg is very useful to make more input photo to train.(nearly more than 400 photos). It turns video into a lot of images.
We need to download install package from http://www.ffmpeg.org/download.html
```bash
sudo apt-get install yasm 
sudo apt-get install libx264-dev
sudo apt-get install libfaac-dev 
sudo apt-get install libmp3lame-dev 
sudo apt-get install libtheora-dev 
sudo apt-get install libvorbis-dev 
sudo apt-get install libxvidcore-dev 
sudo apt-get install libxext-dev 
sudo apt-get install libxfixes-dev 
cd ffmpeg-4.0
sudo -s
source configure
make
make install
```
test
```bash
ffmpeg -i "video.mp4" -r 5 -q:v 2 -f image2 image-3%d.jpeg
```
# use
### EXTRACT
So here's a problem. We have a ton of pictures of both our subjects, but they're just pictures of them doing stuff or in an environment with other people. Their bodies are on there, they're on there with other people... It's a mess. We can only train our bot if the data we have is consistent and focusses on the subject we want to swap. This is where faceswap first comes in.
```bash
# To convert trump:
python faceswap.py extract -i ~/faceswap/photo/trump -o ~/faceswap/data/trump
# To convert cage:
python faceswap.py extract -i ~/faceswap/photo/cage -o ~/faceswap/data/cage
```
We specify our photo input directory and the output folder where our training data will be saved. The script will then try its best to recognize face landmarks, crop the image to that size, and save it to the output folder. Note: this script will make grabbing test data much easier, but it is not perfect. It will (incorrectly) detect multiple faces in some photos and does not recognize if the face is the person who we want to swap. Therefore: **Always check your training data before you start training.** The training data will influence how good your model will be at swapping.
You can see the full list of arguments for extracting via help flag. i.e.
```bash
python faceswap.py extract -h
```
### TRAIN
The training process will take the longest, especially on CPU. We specify the folders where the two faces are, and where we will save our training model. It will start hammering the training data once you run the command. I personally really like to go by the preview and quit the processing once I'm happy with the results.
```bash
python faceswap.py train -A ~/faceswap/data/trump -B ~/faceswap/data/cage -m ~/faceswap/models/
# or -p to show a preview
python faceswap.py train -A ~/faceswap/data/trump -B ~/faceswap/data/cage -m ~/faceswap/models/ -p 
```
If you use the preview feature, select the preview window and press ENTER to save your processed data and quit gracefully. Without the preview enabled, you might have to forcefully quit by hitting Ctrl+C to cancel the command. Note that it will save the model once it's gone through about 100 iterations, which can take quite a while. So make sure you save before stopping the process.
You can see the full list of arguments for training via help flag. i.e.
```bash
python faceswap.py train -h
```
### CONVERT
Now that we're happy with our trained model, we can convert our video. How does it work? Similarly to the extraction script, actually! The conversion script basically detects a face in a picture using the same algorithm, quickly crops the image to the right size, runs our bot on this cropped image of the face it has found, and then (crudely) pastes the processed face back into the picture.
Remember those initial pictures we had of Trump? Let's try swapping a face there. We will use that directory as our input directory, create a new folder where the output will be saved, and tell them which model to use.
```bash
python faceswap.py convert -i ~/faceswap/photo/trump/ -o ~/faceswap/output/ -m ~/faceswap/models/
```
It should now start swapping faces of all these pictures.
You can see the full list of arguments available for converting via help flag. i.e.
```bash
python faceswap.py convert -h
```
### GUI
All of the above commands and options can be run from the GUI. This is launched with:
```bash
python faceswap.py gui
```
### Video's
A video is just a series of pictures in the form of frames. Therefore you can gather the raw images from them for your dataset or combine your results into a video.
### EFFMPEG
You can perform various video processes with the built in effmpeg tool. You can see the full list of arguments available by running:
```bash
python tools.py effmpeg -h
```
### Extracting video frames with FFMPEG
Alternatively you can split a video into seperate frames using [ffmpeg](https://www.ffmpeg.org) for instance. Below is an example command to process a video to seperate frames.
```bash
ffmpeg -i /path/to/my/video.mp4 /path/to/output/video-frame-%d.png
```
### Generating a video
If you split a video, using [ffmpeg](https://www.ffmpeg.org) for example, and used them as a target for swapping faces onto you can combine these frames again. The command below stitches the png frames back into a single video again.
```bash
ffmpeg -i video-frame-%0d.png -c:v libx264 -vf "fps=25,format=yuv420p" out.mp4
```
