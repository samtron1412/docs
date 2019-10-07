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
- Inspect the topic
    + `rostopic echo <topic>`
- List all services: `rosservice list`
- Determine what type of data is included in a request/response
    + `rosservice type <service>`
- Calling services: `rosservice call [service] [arguments]`
- Play back all the messages published on a set of topics
    + `rosbag play baxter.bag`
    + You can pause the play back by the space bar
- Bringing up and configuring multiple nodes:
    + `roslaunch my_package foo.launch`
- A XML file that specifies several nodes for ROS to launch, with
  various parameters and topic renaming directions.


# Tools

## MoveIt

- Motion planning library

## tf/tf2

- Echo the transformation between two frames
    + `rosrun tf tf_echo base left_hand`
- Import tf2 package in ROS code
    + `import tf2_ros`
- A `Buffer` is the core of `tf2` and stores a buffer of previous
  transforms.
    + `tfBuffer = tf2_ros.Buffer()`
- A `TransformListener` subscribes to the `tf` topic and maintains the
  tf graph inside the `Buffer`.
    + `tfListener = tf2_ros.TransformListener(tfBuffer)`
- The function `tfBuffer.lookup_transform(...)` looks up the transform
  of the target frame in the source frame.
    + The output is of type `geometry_msgs/TransformStamped`
    + `trans = tfBuffer.lookup_transform(target_frame, source_frame, rospy.Time())`
- Some `tf` exceptions you might want to catch:
    + tf2_ros.LookupException
    + tf2_ros.ConnectivityException
    + tf2_ros.ExtrapolationException

```python
try:
    <code to execute>
except (<exception1> as e1, <exception2> as e2, ...):
    <code to exceute if an exception occurs>
```


## rviz

- 3D visualization utility
- `rosrun rviz rviz`

## rqt_graph

- Display the computation graph of ROS
- `rosrun rqt_graph rqt_graph`


# Write a publisher/subscriber pair

## Create a new package

- Create a new package with the appropriate dependencies
    + `catkin_create_pkg my_package <dependencies>`

## Define a new message type

+ Create a new message file: `NewMessage.msg` in the `msg` folder of the
  package
+ The format of a message:

```
<data_type1> <name1>
<data_type2> <name2>
...

string text
string timestamp
...
```

- Data types
    + int8, int16, int32, int64
    + float32, float64
    + string
    + other msg types specified as `my_package/MessageName`
    + variable-length `array[]` and fixed-length `array[N]`

- Telling `catkin_make` that we have a new message type that needs to be
  built.
    + Uncomment the following two lines in `package.xml` of the package

```
<build_depend>message_generation</build_depend>
<run_depend>message_runtime</run_depend>
```

- Next, update the following functions in `my_package/CMakeLists.txt` so
  they read exactly as follows

```
find_package(catkin REQUIRED COMPONENTS rospy std_msgs message_generation)
add_message_files(FILES <NewMessage>.msg)
generate_messages(DEPENDENCIES std_msgs)
catkin_package(CATKIN_DEPENDS rospy std_msgs message_runtime)
```

- Buld the new message type using `catkin_make` in your workspace
  directory
- You can verify it works by confirming the existence of the file
    + `~/ros_workspaces/lab2/devel/lib/python2.7/dist-packages/my_package/msg/_NewMessage.py`
    + This is how ROS implements your high-level message descriptions as
    Python classes.
- You can confirm the contents of your new message by running
    + `rosmsg show my_package/NewMessage`
- To use the new message, you need to `import` it
    + `from my_package.msg import NewMessage`
- `NewMessage` is a class, and the input message must be instantiated as
  an object of this class.


## A sample publisher

```python
#!/usr/bin/env python
#Don't forget to use "chmod +x [filename]" to make
#this script executable.

#Import the rospy package. For an import to work, it must be specified
#in both the package.xml manifest AND the Python file in which it is used.
import rospy
from my_chatter.msg import TimestampString

#Define the method which contains the main functionality of the node.
def my_chatter():

  #Run this program as a new node in the ROS computation graph
  #called /my_chatter.
  rospy.init_node('my_chatter', anonymous=True)

  #Create an instance of the rospy. Publisher object which we can
  #use to publish messages to a topic. This publisher publishes
  #messages of type my_chatter/TimestampString to the topic
  #/user_messages
  pub = rospy.Publisher('user_messages', TimestampString, queue_size=10)

  # Create a timer object that will sleep long enough to result in
  # a 10Hz publishing rate
  # r = rospy.Rate(10) # 10hz

  # Loop until the node is killed with Ctrl-C
  while not rospy.is_shutdown():
    # Construct a string that we want to publish
    obj = TimestampString()
    obj.text = raw_input("Please enter a line of text and press <Enter>: ")
    obj.timestamp = str(rospy.get_time())

    # Publish our string to the 'chatter_talk' topic
    pub.publish(obj)

    # Use our rate object to sleep until it is time to publish again
    # r.sleep()

if __name__ == '__main__':
  # Check if the node has received a signal to shut down
  # If not, run the talker method
  try:
    my_chatter()
  except rospy.ROSInterruptException: pass
```

## A sample subscriber

```python
#!/usr/bin/env python
#Don't forget to use "chmod +x [filename]" to make
#this script executable.

import rospy
from my_chatter.msg import TimestampString

#Define the callback method which is called whenever this node receives a
#message on its subscribed topic. The received message is passed as the
#first argument to callback().
def callback(message):
    print("Message: %s, Sent at: %s, Received at: %s" % (message.text, message.timestamp, rospy.get_time()))

#Define the method which contains the node's main functionality
def listener():

    #Run this program as a new node in the ROS computation graph
    #called /listener_<id>, where <id> is a randomly generated numeric
    #string. This randomly generated name means we can start multiple
    #copies of this node without having multiple nodes with the same
    #name, which ROS doesn't allow.
    rospy.init_node('listener', anonymous=True)

    #Create a new instance of the rospy. Subscriber object which we can
    #use to receive messages of type my_package/TimestampString from the
    #topic /my_chatter. Whenever a new message is received, the method
    #callback() will be called with the received message as its first
    #argument.
    rospy.Subscriber("user_messages", TimestampString, callback)


    #Wait for messages to arrive on the subscribed topics, and exit the node
    #when it is killed with Ctrl+C
    rospy.spin()


#Python's syntax for a main() method
if __name__ == '__main__':
    listener()
```

# Coordinate transformations

## Forward kinematics

-  Given a specified angle for each joint in the manipulator, can we
   compute the orientation of a selected link of the manipulator
   relative to a fixed world coordinate frame or a frame attached to
   another point on the robot?

