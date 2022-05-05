FROM tensorflow/tensorflow:latest-gpu



#https://github.com/NVIDIA/nvidia-docker/issues/1631#issuecomment-1112828208
RUN rm /etc/apt/sources.list.d/cuda.list
RUN rm /etc/apt/sources.list.d/nvidia-ml.list
RUN apt-key del 7fa2af80
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu2004/x86_64/7fa2af80.pub

RUN apt-get update && apt-get install -y libsndfile1-dev ffmpeg  #https://github.com/readthedocs/readthedocs.org/issues/6086#issuecomment-579671762


#https://github.com/librosa/librosa/issues/1156
RUN mkdir -m 777 /tmp/NUMBA_CACHE_DIR /tmp/MPLCONFIGDIR
ENV NUMBA_CACHE_DIR=/tmp/NUMBA_CACHE_DIR/
ENV MPLCONFIGDIR=/tmp/MPLCONFIGDIR/

#https://stackoverflow.com/questions/44683119/dockerfile-replicate-the-host-user-uid-and-gid-to-the-image
ARG UNAME=dev
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID -o $UNAME
RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME
USER $UNAME

ENV PATH="/home/$UNAME/.local/bin:${PATH}"

COPY requirements.txt .
RUN pip3 install -r requirements.txt

WORKDIR /home/$USER






