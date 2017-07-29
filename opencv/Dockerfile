FROM rwightman/pytorch-extra:v0.1.12

ENV PATH /opt/conda/envs/pytorch-py35/bin:$PATH

# This pulls in a whole bunch of crap, python2.7!? how to improve?
RUN apt-get update -qq && apt-get install -y --no-install-recommends \
    libtiff5-dev \
    libpng-dev \
    libjpeg-dev \
    libjasper-dev \
    libavcodec-dev \
    libavformat-dev \
    libavresample-dev \
    libavutil-dev \
    libswscale-dev \
    libdc1394-22-dev \
    libgtk2.0-dev \
    libv4l-dev \
    libtbb-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN git clone --branch 3.2.0 --depth 1 https://github.com/opencv/opencv.git /workspace/opencv && \
    cd /workspace/opencv && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE -DWITH_OPENGL=ON -DWITH_TBB=ON -DWITH_CUDA=OFF \
    -D BUILD_EXAMPLES=OFF -D BUILD_PERF_TESTS=OFF -D BUILD_TESTS=OFF \
    -D CMAKE_INSTALL_PREFIX=$(python -c "import sys; print(sys.prefix)") \
    -D PYTHON3_EXECUTABLE=$(which python3) \
    -D PYTHON_INCLUDE_DIR=$(python -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
    -D PYTHON3_PACKAGES_PATH=$(python -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") \
    -D PYTHON3_NUMPY_INCLUDE_DIRS=/opt/conda/envs/pytorch-py35/lib/python3.5/site-packages/numpy/core/include \
    -D PYTHON_LIBRARY=/opt/conda/lib/libpython3.5m.so \
    .. && \
    make -j"$(nproc)"  && \
    make install && \
    ldconfig && \
    cd /workspace && \
    rm -rf /workspace/opencv
