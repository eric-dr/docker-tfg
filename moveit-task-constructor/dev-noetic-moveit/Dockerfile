FROM ros1-eut:dev-noetic
#ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    python3-wstool       
    
RUN rm -R /ros_ws

# Prepare ROS workspace
RUN mkdir -p /ros_ws/src
WORKDIR /ros_ws/src
RUN wstool init .
RUN wstool merge -t . https://raw.githubusercontent.com/ros-planning/moveit/master/moveit.rosinstall
RUN wstool remove  moveit_tutorials  # this is cloned in the next section
RUN wstool update -t .
RUN git clone https://github.com/ros-planning/moveit_tutorials.git -b master
#RUN git clone https://github.com/ros-planning/panda_moveit_config.git -b noetic-devel
ENV DEBIAN_FRONTEND=noninteractive
RUN rosdep install -y --from-paths . --ignore-src --rosdistro noetic
WORKDIR /ros_ws
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash;catkin config --extend /opt/ros/noetic --cmake-args -DCMAKE_BUILD_TYPE=Release ;catkin build"

WORKDIR /ros_ws/src
RUN git clone https://github.com/ros-planning/moveit_task_constructor.git
RUN rosdep install -y --from-paths . --ignore-src --rosdistro noetic
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash; catkin build"

RUN rm -rf /var/lib/apt/lists/*
