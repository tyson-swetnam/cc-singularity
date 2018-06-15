BootStrap: debootstrap
OSVersion: bionic
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%setup
    apt-get install -y debootstrap && apt-get install build-essential
    apt install -y snapd

%environment
    PATH=$PATH:/snap/bin/

%post
    echo "deb http://us.archive.ubuntu.com/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list

    # be sure to have an updated system
    apt-get update && apt-get upgrade -y
    
    # Install OpenGL
    apt-get install -y libglu1-mesa-dev freeglut3-dev mesa-common-dev

    # Install CloudCompare with snap
    apt install -y snapd
    snap install cloudcompare
    snap refresh edge

 %runscript
    echo "Starting CloudCompare GUI"
    cloudcompare.CloudCompare   

# Install latest NVIDIA drivers
#   add-apt-repository ppa:graphics-drivers/ppa
#   apt-get update -y
#   apt-get install -y nvidia-390

# Install VirtualGL
#   wget https://sourceforge.net/projects/virtualgl/files/2.5.2/virtualgl_2.5.2_amd64.deb/download -O /tmp/virtualgl_2.5.2_amd64.deb
#   apt-get -y install mesa-utils mesa-utils-extra x11-apps
#   dpkg -i /tmp/virtualgl_2.5.2_amd64.deb

%labels
Maintainer Tyson Lee Swetnam
Version v0.1
Date 2018-06-15
