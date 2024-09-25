ARG PYTORCH="2.0.1"
ARG CUDA="11.7"
ARG CUDNN="8"
# https://mmcv.readthedocs.io/en/latest/get_started/installation.html 

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0 7.5 8.0 8.6+PTX" \
    TORCH_NVCC_FLAGS="-Xfatbin -compress-all" \
    CMAKE_PREFIX_PATH="$(dirname $(which conda))/../" \
    FORCE_CUDA="1"

ARG DEBIAN_FRONTEND=noninteractive

# Install the required packages
RUN apt-get update \
    && apt-get install -y ffmpeg libsm6 libxext6 git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install MMEngine and MMCV
# https://mmcv.readthedocs.io/en/latest/get_started/installation.html
RUN pip install openmim 
RUN pip install "mmengine" 
RUN pip install "mmcv==2.0.1" -f https://download.openmmlab.com/mmcv/dist/cu118/torch2.0/index.html

RUN pip install ipykernel notebook ipywidgets
# # # Install MMDetection --> this is done in devcontainer postCreateCommand
# RUN conda clean --all \
#     && git clone https://github.com/open-mmlab/mmdetection.git /mmdetection \
#     && cd /mmdetection \
#     && pip install --no-cache-dir -e .

WORKDIR /mmdetection
