# The bundle types defined by CFEngine

The bundle types defined by CFEngine are

## agent

Bundles of type agent are “executable” bundles that can be called from the main
bundlesequence declaration, or as method calls in the methods: section of another
agent bundle. In this respect they could be compared to subroutines in other programming languages. They are the most extensive and powerful type of bundle,
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

# common
Bundles of this type are just like agent bundles, but are special in that the variables
and classes defined in them are automatically available to every other bundle in
your policy. As such, they are a good place to define globally useful variables and
classes. 

For example:

```
bundle common g
{
	vars:
		"localdir" string => "/usr/local";
		"confdir" string => "/etc";
	classes:
		"testhost" or => { "testhost1", "testhost2" };
}
```

This example defines two variables with strings that will be useful in other parts
of the policy, and which we can reference as $(g.localdir) and $(g.confdir) (in
general, any variable can be accessed from anywhere else by prefixing it with the
name of the bundle where it was defined). Also defined is a class based on whether
either of the classes testhost1 or testhost2 is defined (this would be the case if the
current host has any of those names, and is a common way of defining a class for
a certain group. This class is automatically made global, which means it can
be used in any other bundle.

## edit_line
Bundles of type edit_line can be used to change a file, one of the most common
and most complex operations performed by CFEngine. These bundles must be
specified as the value of the edit_line attribute in a file-editing promise (this is, a
promise of type files: ). edit_line bundles themselves can be quite complex and
contain their own set of allowable promise types, which include:

* insert_lines: to add lines to a file
* delete_lines: to remove lines from a file
* field_edits: to make field-oriented changes in a file
* replace_patterns: to make regular expression substitutions in a file

## server
Bundles of type server control the behavior of the cf-serverd process, which has
the task of serving files to other CFEngine machines that request them (cf-serverd normally runs on the CFEngine policy hub). This type of bundle can contain
two promise types:

* access: to define access permissions to different resources on the server.
* roles: to define which users can indicate classes (and which classes they can define) in the server process, to alter the behavior of the cf-serverd daemon. One of CFEngine’s strong security features is that remote machines can never execute arbitrary commands. Instead, they can execute certain bundles. Some users, as defined by roles: promises, may have the ability to set custom classes when invoking those remote promises, thus allowing them to modify the promises’ behavior, but only as allowed by the remote bundle and its handling of the defined classes. 

## knowledge
Bundles of type knowledge are fully supported only in commercial editions of
CFEngine, and allow you to document high-level system knowledge in the CFEngine configuration. This can be used to analyze the system, and to both keep and
deduce information about its behavior and its configuration.

* inferences: specifies relationships between different concepts in the knowledge base, and performs some simple contextual reasoning
* things: specifies tangible objects in the knowledge map, and how they are called, how they behave, how they are connected to others, and other properties (for example, who does a machine belong to, and where it is located)
* topics: defines the elements (subjects and objects) that will be used in the knowledge representations, and the relationships between them
* occurrences: defines documents or resources (e.g., URLs) that refer to certain topics, and provides more information about them

Knowledge bundles can be analyzed by the cf-know command to produce and analyze knowledge maps. CFEngine’s knowledge-management 
features are an advanced topic that we will not discuss further in this book.

## monitor
Bundles of this type are supported only in commercial editions of CFEngine. They
define custom parameters that CFEngine can monitor automatically, and specify
how to react to changes in their values. CFEngine natively knows how to monitor
a large set of system values, such as CPU and memory utilization. This type of 
bundle supports only one section called measurements: , which contains promises
defining what and how to monitor it, and how to react to changes.

Certain generic promise types are allowed in all bundle types:

* vars: to define variables
* classes: to define classes
* reports: to define produced output