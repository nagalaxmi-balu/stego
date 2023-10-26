FROM cr.siemens.com/sas-resources/base-images/dev_cpp_cuda_11.6.0-cudnn8-devel-ubuntu20.04
ENV PROJECT_WS=/stego
WORKDIR $PROJECT_WS
COPY requirements.txt $PROJECT_WS
# Set httpX_proxyies if CODE_PROXY is defined
ENV BASH_ENV="/etc/bash.bashrc"
RUN sed -i.old '1iif [ -v CODE_PROXY ]; then declare -x HTTP_PROXY=\$CODE_PROXY; declare -x HTTPS_PROXY=\$CODE_PROXY; declare -x http_proxy=\$CODE_PROXY; declare -x https_proxy=\$CODE_PROXY; declare -x no_proxy="code.siemens.com,docker.siemens.com"; declare -x NO_PROXY=\$no_proxy; fi\n' /etc/bash.bashrc
RUN /bin/bash -c 'if [ "$OS_NAME" == "ros" ]; then echo "source /opt/ros/$OS_VERSION/setup.bash" >> /etc/bash.bashrc; fi'
RUN apt-get update && apt-get install wget -yq
#RUN apt-get install libc6/stretch libc6-dev/stretch libc-dev-bin/stretch libc-bin/stretch locales/stretch sudo/stretch
RUN apt-get install build-essential -yq
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get install libgl1-mesa-glx libglib2.0-0 -yq
RUN apt-get install openmpi-bin openmpi-common libopenmpi-dev libgtk2.0-dev git -yq
ARG CI_PROJECT_DIR 
 
RUN apt update \
    && apt install -y python3-dev python3-pip \
    python3-distutils-extra python3-setuptools \
    libboost-all-dev

RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install --upgrade wheel
RUN python3 -m pip install --upgrade setuptools
RUN pip3 install -r $PROJECT_WS/requirements.txt
#RUN cp $CI_PROJECT_DIR/requirements.txt . && pip3 install -r requirements.txt
RUN export PYTHONPATH=${PYTHONPATH}:/workspaces/stego
