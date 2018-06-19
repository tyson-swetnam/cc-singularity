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
    
    # Add Xenial packages to sources.list
    echo "deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >> /etc/apt/sources.list
    
    # Add /snap to the PATH
    echo 'export PATH=$PATH:/snap/bin'>>$SINGULARITY_ENVIRONMENT
  
    # be sure to have an updated system
    apt-get update && apt-get upgrade -y
    apt-get install -y build-essential software-properties-common
    
    # Install Blender and Meshlab
    apt-get install -y blender meshlab
    
    # Install OpenGL dependencies
    apt-get install -y freeglut3-dev 
    apt-get install -y libcanberra-gtk-module
    apt-get install -y libgl1-mesa-glx  
    apt-get install -y libglu1-mesa-dev
    apt-get install -y mesa-common-dev 
    apt-get install -y mesa-utils 
    apt-get install -y mesa-utils-extra
    apt-get install -y x11-apps

    # Fix broken things
    apt-get install -f 
      
    # See Agisoft Cloud Scripts Github for additional instructions: https://github.com/agisoft-llc/cloud-scripts/blob/master/configure.sh 
    
    # Prepare for NVidia drivers install
    apt-get install -y curl gcc kmod make pkg-config xserver-xorg-dev linux-headers-$(uname -r) wget xterm
    
    # Install latest NVIDIA drivers
    NVIDIA_DRIVER=384.59
    # Installing NVidia driver
    # curl -O http://us.download.nvidia.com/XFree86/Linux-x86_64/${NVIDIA_DRIVER}/NVIDIA-Linux-x86_64-${NVIDIA_DRIVER}.run
    # chmod +x NVIDIA-Linux-x86_64-${NVIDIA_DRIVER}.run
    # ./NVIDIA-Linux-x86_64-${NVIDIA_DRIVER}.run --no-questions --accept-license --no-precompiled-interface --ui=none
    # echo ""
    # echo "************************************************************************************************"
    # echo "*                                                                                              *"
    # echo "* May be you see this warning above:                                                           *"
    # echo "*  - WARNING: Unable to find a suitable destination to install 32-bit compatibility libraries. *"
    # echo "* This is OK.                                                                                  *"
    # echo "*                                                                                              *"
    # echo "************************************************************************************************"
    # echo ""
    # rm NVIDIA-Linux-x86_64-${NVIDIA_DRIVER}.run

    # Preparation for virtualgl like in https://virtualgl.org/Documentation/HeadlessNV
    # nvidia-xconfig -a --use-display-device=None --virtual=1280x1024
 
    # Install VirtualGL
    wget https://sourceforge.net/projects/virtualgl/files/2.5.2/virtualgl_2.5.2_amd64.deb/download -O /tmp/virtualgl_2.5.2_amd64.deb
    dpkg -i /tmp/virtualgl_2.5.2_amd64.deb
    rm /tmp/virtualgl*.deb

    # Install TurboVNC
    # wget https://sourceforge.net/projects/turbovnc/files/2.1.1/turbovnc_2.1.1_amd64.deb/download -O /tmp/turbovnc_2.1.1_amd64.deb
    # dpkg -i /tmp/turbovnc*.deb
    # rm /tmp/turbovnc*.deb

%runscript
    export PATH=$PATH:/snap/bin
    echo "Starting CloudCompare GUI"
    cloudcompare.CloudCompare

%labels	
    Maintainer Tyson Lee Swetnam
    Version v0.1
    Date 2018-06-19
