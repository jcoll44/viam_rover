# Use the official ROS Noetic base image
FROM ros:noetic

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8


# Install dependencies
RUN apt-get update && apt-get install -y \
    python3-catkin-tools \
    python3-pip \
    ros-noetic-catkin \
    libssl-dev \
    libusb-1.0-0-dev \
    libudev-dev \
    pkg-config \
    libgtk-3-dev \
    git \
    wget \
    cmake \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN sudo mkdir -p /etc/apt/keyrings
RUN curl -sSf https://librealsense.intel.com/Debian/librealsense.pgp | tee /etc/apt/keyrings/librealsense.pgp > /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/librealsense.pgp] https://librealsense.intel.com/Debian/apt-repo `lsb_release -cs` main" | tee /etc/apt/sources.list.d/librealsense.list
    
# Install dependencies
RUN apt-get update && apt-get install -y \
    ros-noetic-realsense2-camera \
    librealsense2-dkms \
    librealsense2-utils \
    librealsense2-dev \
    git \
    wget \
    cmake \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
RUN pip3 install -U \
    catkin_pkg \
    rosdep 


# Create a catkin workspaceet the working directo
RUN mkdir -p /root/catkin_ws/src
WORKDIR /root/catkin_ws

# Install ROS dependencies and build the workspace
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu `lsb_release -sc` main" \
    > /etc/apt/sources.list.d/ros-latest.list'
RUN wget http://packages.ros.org/ros.key -O - | apt-key add -
RUN apt-get install python3-catkin-tools
RUN cd /root/catkin_ws
RUN catkin init
RUN rosdep update \
    && rosdep install --from-paths src --ignore-src -r -y \
    && /bin/bash -c "source /opt/ros/noetic/setup.bash && catkin build"
RUN echo "source /root/catkin_ws/devel/setup.bash" >> /root/.bashrc 

RUN apt-get install ros-noetic-catkin
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash && catkin build"


# Source the setup file
RUN echo "source /catkin_ws/devel/setup.bash" >> ~/.bashrc



RUN apt-get update && apt-get install -y \
    ros-noetic-rgbd-launch \
    && rm -rf /var/lib/apt/lists/*


CMD ["bash"]
