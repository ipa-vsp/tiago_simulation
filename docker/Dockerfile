FROM ros:melodic-robot

ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_DISTRO melodic

WORKDIR /home/tiago

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


# Copy scripts
RUN mkdir -p /usr/local/bin/scripts
COPY *entrypoint.sh /usr/local/bin/scripts/
RUN  chmod +x /usr/local/bin/scripts/*.sh