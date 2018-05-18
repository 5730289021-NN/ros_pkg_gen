# Package generator

The following packages are about the automatic creation of ROS packages (so far c++ and python).
To do so the input needed are:

* A _package template_: a template is defined by a _template Designer_.
  The _Developer_ just has to select the template that best fits his needs.
* An _interface specification_: a xml file describing mainly the interface of the package to create, according to the template.
  This is to be completed by the _Developer_ according to his specific needs for the package he is willing to create

**Author(s): Anthony Remazeilles**

**Maintainer: Anthony Remazeilles, anthony.remazeilles@tecnalia.com**

**Affiliation: Tecnalia Research and Innovation, Spain**

## Getting started
### Prerequisites
The component is assuming `ROS` is installed on the machine.

### Installing
The installation procedure follows the standard operations as any ROS package do.

### Use

We assume we are at the ROS workspace root, and that the current git repository is accessible from the ROS workspace.
```
source devel/setup.bash
# go to the place where we would like to place the new package
cd src
# create a ROS interface xml file
gedit my_new_package_spec.ros_package
# launch the code generation (for c++ package)
rosrun package_generator generate_package my_new_package_spec.ros_package cpp_node_update
# launch the code generation (for python package)
rosrun package_generator generate_package my_new_package_spec.ros_package python_node_update
```

The template can be indicated eiher as:
* an absolute path to a template directory
* a relative path from the currently active directory
* a directory name assumed to be existing in the template package (within the `templates` directory)

## content

### `package_generator`

Generates a node / package content based on a xml description.
It contains the following scripts:

See the dedicated [README](package_generator/README.md) for more details on its content.

### `package_generator_templates`

Gathers the currently defined package templates.
So far, it only contains two templates, one for python code and another for C++.
Both follow the same pattern, based on the concept of a central update loop at a given frequency (inspired from BRICS models).

More details in the dedicated [Readme file](package_generator_templates/README.md)


### reminders
* to remap a topic with rosrun:
```
rosrun great_multi_package_pub_sub node_sub sub_int:=/pub_in
```

* for the service, the current implementation is configured to enable initial remapping
```
rosrun great_package_services node_service_server _service_trigger_server_remap:=/service_client
```
* for the action, one can use:
```
rosrun actionlib axclient.py /do_action
```
* for the action, I implemented:
```
rosrun great_package_action_client node_action_client _ac_use_action_remap:=do_action
```

* For the demo, we need to launch:
```
roscore
rosrun great_multi_package_pub_sub node_pub
rosrun great_multi_package_pub_sub node_sub sub_int:=/pub_int
```

## Current actions

Todo:
* insert in package desc added dependencies
* dbcheck param generation (doc)
* see how to handle list and map from parameter server
* retest all packages
* remap for service client
* cpp: change tf for a simple tf example, no action used

* update: if the requested file is generated, refuse it, and mention the use of winmerge to handle it.

Done:
* intensive test maintained content
* cpp: merge action server and client in unique package
* cpp: adapt the content of the python example.
* check the message provided as usage.
* update model examples in the template package (dynParam)
* update doc with dynParam
* add a test for static parameters
* add auto generated in class not supposed to be touched.
* remove the include files in the python template
* adjust class name as said here. Handle the CamelCase stuff in python
* remove includeheaders from cpp pattern
* service client and action client in cpp: move it into passthrough

