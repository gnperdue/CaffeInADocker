FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu14.04
MAINTAINER caffe-maint@googlegroups.com

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        graphviz \
        wget \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        python-dev \
        python-pip && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip

ENV CAFFE_ROOT=/opt/caffe
WORKDIR $CAFFE_ROOT

# FIXME: clone a specific git tag and use ARG instead of ENV once DockerHub supports this.
# Use Sohini's updated Caffe with Gradient Reversal Layer
# See http://sites.skoltech.ru/sites/compvision_wiki/static_pages/projects//grl/
# and https://github.com/sohiniu/caffe -> Sohini used `patch-2`
ENV CLONE_TAG=grad_rev_layer_gnp2017april

RUN git clone -b ${CLONE_TAG} --depth 1 https://github.com/gnperdue/caffe-1.git . && \
    for req in $(cat python/requirements.txt) pydot lmdb; do pip install $req; done && \
    mkdir build && cd build && \
    cmake -DUSE_CUDNN=1 .. && \
    make -j"$(nproc)"

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace
