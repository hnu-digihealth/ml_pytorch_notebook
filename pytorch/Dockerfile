# losely based on https://github.com/iot-salzburg/gpu-jupyter/
# image from https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch
FROM nvcr.io/nvidia/pytorch:23.10-py3

# Set timezone as required by tzdata
ENV TZ=Europe/Berlin
# save to filre required, as ENV does not work everywhere
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt update
RUN apt install -y tzdata
RUN apt update && apt upgrade -y

# Install required OpenSlide and libvips packages
RUN apt-get install -y \
    python3-openslide \
    libvips

# Install required package for cv2
RUN apt-get install -y libgl1

# Install required package for wsidicomizer
RUN apt-get install -y libturbojpeg

# custom user and group
RUN groupadd -g 1000 ml_group
RUN useradd -u 1000 -g ml_group -s /bin/sh -m ml_user
USER ml_user:ml_group

WORKDIR /home/ml_user

ENV PATH="/home/ml_user/.local/bin:${PATH}"
#ENV JUPYTER_ENABLE_LAB=yes

# Install required pip packages
#RUN pip3 install --upgrade pip && \
#    pip3 install jupyterlab jupyterlab-git

CMD ["jupyter-lab"]