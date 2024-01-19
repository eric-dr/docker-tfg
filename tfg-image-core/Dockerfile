FROM eut-moveit:dev-noetic-task-constructor
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-pymodbus \ 
    python3-pyasn1 python3-twisted\
    qtbase5-dev \
    libqt5svg5-dev \
    libzmq3-dev \
    libdw-dev \
    libboost-dev \
    ros-noetic-behaviortree-cpp-v3 #Install BTCpp     
    

#Install Groot and build WS
WORKDIR /ros_ws/src
RUN git clone https://github.com/BehaviorTree/Groot.git
WORKDIR /ros_ws
RUN rosdep install -y --from-paths src --ignore-src --rosdistro noetic

RUN rm -rf /var/lib/apt/lists/*

# Hand gesture
RUN pip3 install mediapipe
RUN pip3 install opencv-python
RUN pip3 install tensorflow

# MySQL
RUN apt-get install python3-dev default-libmysqlclient-dev build-essential pkg-config
RUN pip install mysqlclient

# PyMYSQL
RUN python3 -m pip install PyMySQL
