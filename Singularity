BootStrap: debootstrap
OSVersion: xenial
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%setup

    # Thread about Snap install on Singularity: https://groups.google.com/a/lbl.gov/forum/#!topic/singularity/wGfm_nf-b2I
    # presumes snap is already installed on my host system
    snap install cloudcompare
    snap refresh --edge cloudcompare

    # copy a snap installed directory to the container root file system
    SNAP_BASE=/snap
    mkdir -p ${SINGULARITY_ROOTFS}$SNAP_BASE

    # Copy cloudcompare
    cp -R $SNAP_BASE ${SINGULARITY_ROOTFS}

%environment
    PATH=$PATH:/snap/bin
    export PATH

%post
    set -e 
    
    echo "deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >> /etc/apt/sources.list

    # be sure to have an updated system
    apt-get update && apt-get upgrade -y
    apt-get install -y build-essential software-properties-common
    
    # Install Blender and Meshlab
    apt-get install -y blender meshlab
    
    # Install OpenGL dependencies
    apt-get install -y libglu1-mesa-dev freeglut3-dev mesa-common-dev
    apt-get install -y libcanberra-gtk-module
    
    # Add /snap to the PATH
    echo 'export PATH=$PATH:/snap/bin'>>$SINGULARITY_ENVIRONMENT

    # Fix broken things
    apt-get install -f 
    
# See Agisoft Cloud Scripts Github for instructions: https://github.com/agisoft-llc/cloud-scripts/blob/master/configure.sh 
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
