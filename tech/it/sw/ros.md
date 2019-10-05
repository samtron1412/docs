# Overview

Robot Operating System

- A meta-operating system
    + hardware abstraction
    + low-level device control
    + implementation of commonly-used functionality
    + message-passing between processes
    + package management
    + tools and libraries for otaining, building, writing, and running
    code across multiple computers.
- The ROS runtime/computation "graph" is a peer-to-peer network of processes that
  are loosely coupled using the ROS communication infrastructure
    + synchronous RPS-style communicaito over services
    + asynchronous streaming of data over topics
    + storage of data on a Parameter Server

# Computation graph

- Each individual control loop is a *node* within the computation graph.
- A node is simply an executable file that performs some tasks.
- Nodes exchange control messages, error readings, and other data by
  publishing or subscribing to *topics* or by sending requests to
  *services* offered by other nodes.
   + *topics* are edges in the graph
- Message: a ROS datatype used to exchange data between nodes

# File system

- Organizing ROS code into logical units and managing dependencies
  between units
    + Packages
```
ros_workspaces
  lab1
    build
    devel
      setup.bash
    src
      CMakeLists.txt
      foo
        CMakeLists.txt
        package.xml
        launch
          zap.launch
        scripts
        src
          foo.py
        include
        lib
```

# Workspaces and Packages

- A workspace is a collection of packages that are built together.
- ROS uses the *catkin* tool to build all code in a workspace.
- Each time you start a new project you will want to create and
  initialize a new catkin workspace.
    + Create a workspace directory: `lab01`
    + Create `src` directory inside the workspace
    + Run `catkin_init_workspace` inside the new `src` directory
        * It will create a new file `CMakeLists.txt` inside `src`
- Build all packages by running `catkin_make` from the workspace
  directory `lab01`
    + `build` directory: building related information
    + `devel` directory: header files
- Remember to source `devel/setup.bash` after building packages

# Commands

- Find a package: `rospack find baxter_examples`
- List content of the package: `rosls baxter_examples`
- Change directory to the package: `roscd baxter_examples`
- Creating a workspace: `catkin_init_workspace`
    + Create a single file: `CMakeLists.txt`
- Build packages of a workspace: `catkin_make`
- Creating a new package: `catkin_create_pkg foo`
    + Run this inside the `src` directory of the workspace
    + Create a package with dependencies
        `catkin_create_pkg bar rospy std_msgs geometry_msgs tutlesim`
- Run the core: `roscore`
    + A server that all other ROS nodes use to communicate
- List all nodes: `rosnode list`
    + Get more information of the node: `rosnode info <node>`
- Run a node or a piece of code:
    + `rosrun <node>`
    + `rosrun <node> <script_name.py> [arguments for the script]`
- List all topics: `rostopic list`
- Find the type of the topic (message type):
    + `rostopic type <topic_name>`
- Echo messages of a topic: `rostopic echo <topic>`
- Show the structure of the message type:
    + `rosmsg show <message_type>`
- Find all the topics that contain a particular message type:
    + `rostopic find <message_type>`
- List all services: `rosservice list`
- Determine what type of data is included in a request/response
    + `rosservice type <service>`
- Calling services: `rosservice call [service] [arguments]`


# Tools

## rviz

- 3D visualization utility
- `rosrun rviz rviz`

## rqt_graph

- Display the computation graph of ROS
- `rosrun rqt_graph rqt_graph`



