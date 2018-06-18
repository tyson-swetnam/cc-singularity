BootStrap: debootstrap
OSVersion: xenial
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%setup

    # snap is already installed on my host
    snap install cloudcompare
    snap refresh --edge cloudcompare

    # copy a snap directory to your container somewhere
    SNAP_BASE=/snap
    mkdir -p ${SINGULARITY_ROOTFS}$SNAP_BASE

    # Copy cloudcompare
    cp -R $SNAP_BASE ${SINGULARITY_ROOTFS}

%environment
    PATH=$PATH:/snap/bin
    export PATH

%post
    echo "deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >> /etc/apt/sources.list

    # be sure to have an updated system
    apt-get update && apt-get upgrade -y
    apt-get install -y build-essential software-properties-common
    
    # Install OpenGL
    apt-get install -y libglu1-mesa-dev freeglut3-dev mesa-common-dev
    apt-get install -y libcanberra-gtk-module
    
    # Add /snap to the PATH
    echo 'export PATH=$PATH:/snap/bin'>>$SINGULARITY_ENVIRONMENT

# Install latest NVIDIA drivers
#   add-apt-repository ppa:graphics-drivers/ppa
#   apt-get update -y
#   apt-get install -y nvidia-390
 
# Install VirtualGL
#   wget https://sourceforge.net/projects/virtualgl/files/2.5.2/virtualgl_2.5.2_amd64.deb/download -O /tmp/virtualgl_2.5.2_amd64.deb
#   apt-get -y install mesa-utils mesa-utils-extra x11-apps
#   dpkg -i /tmp/virtualgl_2.5.2_amd64.deb

%runscript
    echo "Starting CloudCompare GUI"
    cloudcompare.CloudCompare

%labels	
    Maintainer Tyson Lee Swetnam
    Version v0.1
    Date 2018-06-15
