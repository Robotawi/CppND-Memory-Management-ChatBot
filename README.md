# CPPND: Memory Management Chatbot

In this project, I have been given ChatBot program that is not implementing modern C++ memory management concepts. The aim is to optimize the ChatBot program from a memory management perspective. I analyzed and modified the ChatBot program to include smart pointers, move semantics, and considered about ownership and memory allocation. This project was meant to be apply the concepts I acquired in Udacity's C++ Nanodegree where I am mentoring students now to master these concepts. 

# The given ChatBot
<img src="images/chatbot_demo.gif"/>

The ChatBot code creates a dialogue where users can ask questions about some aspects of memory management in C++. After the knowledge base of the chatbot has been loaded from a text file, a knowledge graph representation is created in computer memory, where chatbot answers represent the graph nodes and user queries represent the graph edges. After a user query has been sent to the chatbot, the Levenshtein distance is used to identify the most probable answer. The code is fully functional as-is and uses raw pointers to represent the knowledge graph and interconnections between objects throughout the project.

## Installation 
- #### Dependencies for Running Locally
  * cmake >= 3.11
    * All OSes: [click here for installation instructions](https://cmake.org/install/)
  * make >= 4.1 (Linux, Mac), 3.81 (Windows)
    * Linux: make is installed by default on most Linux distros
    * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
    * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
  * gcc/g++ >= 5.4
    * Linux: gcc / g++ is installed by default on most Linux distros
    * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
    * Windows: recommend using [MinGW](http://www.mingw.org/)
  * wxWidgets >= 3.0
    * Linux: `sudo apt-get install libwxgtk3.0-dev libwxgtk3.0-0v5-dbg`
    * Mac: There is a [homebrew installation available](https://formulae.brew.sh/formula/wxmac).
    * Installation instructions can be found [here](https://wiki.wxwidgets.org/Install). Some version numbers may need to be changed in instructions to install v3.0 or greater.

- #### Clone
    ```
    git clone https://github.com/Robotawi/CppND-Memory-Management-ChatBot.git
    ```
- #### Setup
  ```
  cd CppND-Memory-Management-ChatBot
  mkdir build 
  cd build
  cmake ..
  make
  ```

## Running
```
./membot
```
## The Implemented Changes to optimize the program

### 1 : Employ smart pointers instead of raw pointers 1
In file `chatgui.h` / `chatgui.cpp`, I made `_chatLogic` an exclusive resource to class `ChatbotPanelDialog` using unique pointer, and made the required changes to the data structures and functions to reflect the the change from raw pointers to smart pointers.

### 2 : Implement the rule of five
In file `chatbot.h` / `chatbot.cpp`, I made the required changes to the class `ChatBot` to comply with the Rule of Five. The memory allocation/deallocation are properly done in the heap.

### 3 : Employ smart pointers instead of raw pointers 2
In file `chatlogic.h` / `chatlogic.cpp`, I adapted the vector `_nodes` in a way that the instances of `GraphNodes` to which the vector elements refer are exclusively owned by the class `ChatLogic`. This was done using unique pointers. I made the required changes to the data to reflect the the change from raw pointers to smart pointers.

### 4 : Moving smart pointers

In files `chatlogic.h` / `chatlogic.cpp` and `graphnodes.h` / `graphnodes.cpp` I changed the ownership of all instances of `GraphEdge` in a way such that each instance of `GraphNode` exclusively owns the outgoing `GraphEdges` (using smart pointers) and holds non-owning references to incoming `GraphEdges`. Move semantics is utilized when transferring ownership from class `ChatLogic`, where all instances of `GraphEdge` are created, into instances of `GraphNode`. 

### 5 : Moving the ChatBot

In file `chatlogic.cpp`, a local instance of the `ChatBot` was created at the bottom of `LoadAnswerGraphFromFile`. Then, it is passed to the root node using move semantics. I made the required changes in files `chatlogic.h` / `chatlogic.cpp` and `graphnode.h` / `graphnode.cpp`. 

## Contact
If you are interested in the presented work/ideas or if you have any questions, you are welcome to connect with me on [LinkedIn](https://www.linkedin.com/in/mohraess). We can discuss about this project and other interesting projects.