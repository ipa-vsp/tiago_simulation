FROM ros:melodic-robot

ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_DISTRO melodic

ARG USERNAME=admin
ARG USER_UID=1000
ARG USER_GID=1000

WORKDIR /home/${USERNAME}

RUN mkdir -p catkin_ws/src
COPY tiago.rosinstall catkin_ws

RUN apt-get update && apt-get install -q -y --no-install-recommends \
    wget \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    cd catkin_ws && \
    rosinstall src /opt/ros/melodic tiago.rosinstall \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -q -y --no-install-recommends \
    ros-melodic-rviz \
    ros-melodic-joint-state-publisher-gui \
    && rm -rf /var/lib/apt/lists/*

ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

# Create the 'admin' user if not already exists
RUN if [ ! $(getent passwd ${USERNAME}) ]; then \
        groupadd --gid ${USER_GID} ${USERNAME} ; \
        useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} ; \
    fi

# Update 'admin' user
RUN echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && adduser ${USERNAME} video && adduser ${USERNAME} sudo

# Copy scripts
RUN mkdir -p /usr/local/bin/scripts
COPY *entrypoint.sh /usr/local/bin/scripts/
RUN  chmod +x /usr/local/bin/scripts/*.sh
RUN sed -i -e 's/\r$//' /usr/local/bin/scripts/*.sh

ENV USERNAME=${USERNAME}
ENV USER_GID=${USER_GID}
ENV USER_UID=${USER_UID}