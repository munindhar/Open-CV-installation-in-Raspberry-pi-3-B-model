# Open-CV-installation-in-Raspberry-pi-3-B-model
Installation of Open CV in Raspberry pi is a big task, it will not install properly. All of the libraries will be downloaded and saved in the apt buffer in the total process, if we get errors also it will be installed successfully by running the command "sudo apt-get install python3-opencv". 
follow the bellow process.........

step 1: Expand Filesystem

    sudo raspi-config
    
    ==> Select Advanced options => A1 expand filesystem => Press "enter"
   
Step 2: Free up some space

    sudo apt-get purge wolfram-engine
    sudo apt-get purge libreoffice*
    sudo apt-get clean
    sudo apt-get autoremove

Step 3: Install Dependencies
    
    sudo apt-get update
    sudo apt-get upgrade

   If you are having any errors run "sudo apt-get upgrade --fix-missing"
and now reboot the pi
    sudo reboot

   ==> Install CMAKE developer packages
        
        sudo apt-get install build-essential cmake pkg-config -y

   ==> Install Image I/O packages
 
 
         sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev -y

   ==> Install Video I/O packages
          
         sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev -y

Here if you get some failed errors just repeat the command run. This is because of server problem that we are downloading.....

        sudo apt-get install libxvidcore-dev libx264-dev -y

   ==> Install the GTK development library for basic GUI windows

        sudo apt-get install libgtk2.0-dev libgtk-3-dev -y

it will take more time to install all the libraries 

   ==> Install optimization packages (improved matrix operations for OpenCV)

        sudo apt-get install libatlas-base-dev gfortran -y
Step 4: Install python 3, setup tools, dev and numpy

    sudo apt-get install python3 python3-setuptools python3-dev -y
    wget https://bootstrap.pypa.io/get-pip.py
    sudo python3 get-pip.py
    sudo pip3 install numpy

numpy will take atleast half an hour time to install don't do anything untill download

Step 5: Download the OpenCV 3.4 and contrib extra modules

    cd ~
    wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.4.0.zip
    wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.4.0.zip
    unzip opencv.zip    
    unzip opencv_contrib.zip

Step 6: Compile and Install OpenCV 3.4.0 for Python 3
    
    cd opencv-3.4.0
    mkdir build
    cd build
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D BUILD_opencv_java=OFF \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D PYTHON_DEFAULT_EXECUTABLE=$(which python3) \
    -D INSTALL_C_EXAMPLES=OFF \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D BUILD_EXAMPLES=ON\
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.0/modules \
    -D WITH_CUDA=OFF \
    -D BUILD_TESTS=OFF \
    -D BUILD_PERF_TESTS= OFF ..

Step 7: Swap Space size before compiling to add more virtual memory

    sudo nano /etc/dphys-swapfile

change the size 
    # set size to absolute value, leaving empty (default) then uses computed value
    # you most likely don't want this, unless you have an special disk situation
    # CONF_SWAPSIZE=100
    CONF_SWAPSIZE=1024

    sudo /etc/init.d/dphys-swapfile stop
    sudo /etc/init.d/dphys-swapfile start

Final step:
    
    sudo make -j4      /* making with 4 cores
  
Getting some errors here...? it is terminated anytime we should run the above command again and again for 100% installation. ignore the warnings.

it will take approaximately 2 hrs.

after command make -j4 if you have any errors try again with 

    make -j2 or make

and go for below
  
    sudo make install

Don't worry about the make install error if you get the error at 77% or above just run the command "sudo apt-get update"

and run the below command
        
    sudo apt-get install python3-opencv

finally run

    sudo ldconfig


Thank you......

 
