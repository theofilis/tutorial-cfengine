# The bundle types defined by CFEngine

The bundle types defined by CFEngine are:

## agent

Bundles of type agent are “executable” bundles that can be called from the main
bundlesequence declaration, or as method calls in the methods: section of another
agent bundle. In this respect they could be compared to subroutines in other pro-
gramming languages. They are the most extensive and powerful type of bundle,
and the ones that actually implement any changes that we want to make in the
system. 

These bundles can contain the following promise types:

* commands: to specify commands to be executed
* files: to edit and manipulate files
* methods: to call other agent bundles
* packages: to query and manipulate software packages in the system
* processes: to query and manipulate running processes
* storage: to query and configure file systems
* services: to configure system services in Unix-like systems

In addition, the commercial editions of CFEngine support the following types of
promises in agent bundles:

* databases: to manipulate and configure databases
* environments: to manipulate and configure virtual environments
* outputs: to more conveniently configure the logging levels of different bundles
* services: to configure Windows system services