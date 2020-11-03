ARG ALWAYSAI_HW="default"
FROM alwaysai/edgeiq:${ALWAYSAI_HW}-0.16.1
#FROM alwaysai/edgeiq-dev:${ALWAYSAI_HW}-0.16.2.dev2-g7793e68

# Installing lsb-release as needed by the next command
RUN apt-get update && apt-get install -y \
    lsb-release \
    apt-utils \
    gnupg && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Setup sources.list
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

# Set up apt keys
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# This environment variable is needed because tzdata is a dependency for ROS
# so the timezone needs to be specified or else install will fail
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get update && apt-get install -y \
    tzdata && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install ROS-Base
RUN apt-get update && apt-get install -y \
    ros-melodic-ros-base && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Environment Setup
RUN echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc && \
    /bin/bash -c "source ~/.bashrc"

# Installing python-rosdep for package dependancies
RUN apt-get update && apt-get install -y \
    python-rosinstall \
    python-rosinstall-generator \
    python-wstool \
    build-essential \
    libxml2-dev \
    libxslt1-dev \
    python-rosdep && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
