# Docker image for benchmarking DGL

FROM nvidia/cuda:9.0-cudnn7-devel

COPY install/ubuntu_install_core.sh /install/ubuntu_install_core.sh
RUN bash /install/ubuntu_install_core.sh

COPY install/ubuntu_install_python.sh /install/ubuntu_install_python.sh
RUN bash /install/ubuntu_install_python.sh

COPY install/ubuntu_install_python_package.sh /install/ubuntu_install_python_package.sh
RUN bash /install/ubuntu_install_python_package.sh

# add user
RUN useradd -ms /bin/bash user

# add user to sudoers
RUN chmod u+w /etc/sudoers
RUN echo 'user\tALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chmod u-w /etc/sudoers

USER user
WORKDIR /home/user

# use python3 as default python
RUN echo 'alias python=python3' >> /home/user/.bashrc

# Environment variables
ENV PATH=/usr/local/cuda/bin:${PATH}
ENV CPLUS_INCLUDE_PATH=/usr/local/cuda/include:${CPLUS_INCLUDE_PATH}
ENV C_INCLUDE_PATH=/usr/local/cuda/include:${C_INCLUDE_PATH}
ENV LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/nvidia/lib64:${LIBRARY_PATH}
ENV LD_LIBRARY_PATH=/usr/local/cuda/lib64:/usr/local/nvidia/lib64:${LD_LIBRARY_PATH}
