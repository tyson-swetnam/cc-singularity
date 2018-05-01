BootStrap: debootstrap
OSVersion: xenial
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%setup
    cp gis_dependency.makefile $SINGULARITY_ROOTFS/tmp/

%environment
    
%post
    echo "deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >> /etc/apt/sources.list

    # be sure to have an updated system
    apt-get update && apt-get upgrade -y
    
    # install PROJ
    apt-get install libproj-dev proj-data proj-bin -y

    # install Ubuntu dependencies
    apt-get update && apt-get install -y --no-install-recommends \
        apt-transport-https \
        bison \
        build-essential \
        ccache \
        checkinstall \
        cmake \
        curl \
        ffmpeg2theora \
        flex \
        g++ \
        gcc \
        gettext \
        ghostscript \
        htop \
        libavcodec-dev \
        libavformat-dev \
        libav-tools \
        libavutil-dev \
        libboost-program-options-dev \
        libboost-thread-dev \
        libcairo2 \
        libcairo2-dev \
        libcanberra-gtk-module \
        libcanberra-gtk3-module \
        libffmpegthumbnailer-dev \
        libfftw3-3 \
        libfftw3-dev \
        libfontconfig1 \
        libfreetype6-dev \
        libgcc1 \
        libglu1-mesa-dev \
        libgsl0-dev \
        libgtk2.0-dev \
        libgtkmm-3.0-dev \
        libjasper-dev \
        liblas-c-dev \
        libncurses5-dev \
        libnetcdf-dev \
        libperl-dev \
        libpng12-dev \
        libpnglite-dev \
        libpq-dev \
        libproj-dev \
        libreadline6 \
        libreadline6-dev \
        libsqlite3-dev \
        libswscale-dev \
        libtiff5-dev \
        libwxbase3.0-dev   \
        libwxgtk3.0-dev \
        libxmu-dev \
        libxmu-dev \
        libzmq3-dev \
        mesa-common-dev \
        netcdf-bin \
        openjdk-8-jdk \
        pkg-config \
        proj-bin \
        proj-data \
        python3 \
        python-dateutil \
        python-dev \
        python-numpy \
        python-opengl \
        python-wxgtk3.0 \
        python-wxtools \
        python-wxversion \
        rsync \
        sqlite3 \
        subversion \
        swig \
        unzip \
        vim \
        wget \
        wx3.0-headers \
        wx-common \
        zlib1g-dev 

# Install non-gis specific tools
    apt-get install -y texlive-extra-utils 
    apt-get install -y software-properties-common # to ease the adding of new ppas
    apt-get install -y libudunits2-dev # udunits2

# Install CMAKE
    apt purge cmake
    wget https://cmake.org/files/v3.11/cmake-3.11.1-Linux-x86_64.tar.gz
    tar -xvzf cmake-3.11.1-Linux-x86_64
    cd cmake-3.11.1
    cp -r bin /usr/
    cp -r share /usr/
    cp -r doc /usr/share/
    cp -r man /usr/share/
    cd ..
    rm -rf cmake-3.11.1-Linux-x86_64
    rm cmake-3.11.1-Linux-x86_64.tar.gz
    
# Install QT
    
    wget http://download.qt.io/official_releases/qt/5.10/5.10.1/qt-opensource-linux-x64-5.10.1.run
    chmod +x qt-opensource-linux-x64-5.10.1.run
    ./qt-opensource-linux-x64-5.10.1.run
    apt-get install -y synaptic
    apt-get update
    apt-get install -y qt4-dev-tools libqt4-dev libqt4-core libqt4-gui
    apt-get install -y "^libxcb.*" libx11-xcb-dev libxrender-dev

# Install LASZip

    git clone https://github.com/LASzip/LASzip/releases/download/3.2.2/laszip-src-3.2.2.tar.gz

# Install CloudCompare

    git clone --recursive https://github.com/cloudcompare/trunk.git

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
Date 2018-05-01
