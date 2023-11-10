# losely based on https://github.com/iot-salzburg/gpu-jupyter/
# image from https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch
FROM nvcr.io/nvidia/pytorch:23.10-py3

# # Secify required arguments
# ARG USER_ID
# ARG GROUP_ID

# ENV GROUP_ID GROUP_ID
# ENV USER_ID USER_ID

# RUN ECHO $GROUP_ID
# RUN ECHO $USER_ID

# Set timezone as required by tzdata
ENV TZ=Europe/Berlin
# save TZ to file required, as ENV does not work everywhere
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

# copy setup script and files to ml_user dir
COPY setup/ /home/ml_user/setup/
RUN apt-get install -y $(grep -vE "^\s*#" /home/ml_user/setup/apt_packages.txt | tr "\n" " ")
RUN pip install -r  /home/ml_user/setup/requirements.txt

# switch to user
USER ml_user:ml_group

WORKDIR /home/ml_user

ENV PATH="/home/ml_user/.local/bin:${PATH}"