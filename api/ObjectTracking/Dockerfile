#
# Dockerfile for building C++ project
#

# OS image
FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04

# Install
RUN apt-get -y update
RUN apt-get -y install clang byobu curl git htop man unzip vim wget
RUN apt-get -y install libgoogle-glog-dev libgflags-dev liblapack-dev

CMD ["bash"]

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:george-edison55/cmake-3.x
RUN apt-get update
RUN apt-get install -y cmake

RUN apt-get install -y libprotobuf-dev
RUN apt-get install -y protobuf-compiler
RUN apt-get install -y libtbb-dev

RUN apt-get install -y build-essential
RUN apt-get install -y build-essential pkg-config unzip ffmpeg qtbase5-dev python-dev python3-dev python-numpy python3-numpy
RUN apt-get install -y libopencv-dev libgtk-3-dev libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev
RUN apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev
RUN apt-get install -y libv4l-dev libtbb-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev
RUN apt-get install -y libvorbis-dev libxvidcore-dev v4l-utils

RUN \
  cd /root && \
  git clone https://github.com/opencv/opencv_contrib.git && \
  cd

RUN \
  cd /root && \
  git clone https://github.com/opencv/opencv.git && \
  cd opencv && \
  mkdir build && \
  cd build/ && \
  cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D WITH_CUBLAS=ON -DCUDA_NVCC_FLAGS="-D_FORCE_INLINES" -DOPENCV_EXTRA_MODULES_PATH="/root/opencv_contrib-master/modules" .. && \
  make -j $(($(nproc) + 1)) && \
  make install && \
  /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf' && \
  ldconfig && \
  apt-get update

RUN apt-get install -y libleveldb-dev libsnappy-dev libhdf5-serial-dev
RUN apt-get install -y libatlas-base-dev
RUN apt-get install -y --no-install-recommends libboost-all-dev
RUN apt-get install -y liblmdb-dev
RUN apt-get install -y python-pip
RUN apt-get install -y python-dev
RUN apt-get install -y python-numpy python-scipy
RUN apt-get install -y python3-dev
RUN apt-get install -y python3-numpy python3-scipy

RUN \
  cd /root && \
  git clone https://github.com/BVLC/caffe.git && \
  cd caffe && \
  cat python/requirements.txt | xargs -n1 pip install && \
  cp Makefile.config.example Makefile.config

# Set environment variables
ENV HOME /root
# Define working directory
WORKDIR /code
ADD . /code

RUN \
  rm -rf build && \
  mkdir build
RUN \
  cd build && \
  cmake -DCMAKE_CXX_COMPILER=clang++ .. && \
  make -j2 && \
  ./bin/nmf
