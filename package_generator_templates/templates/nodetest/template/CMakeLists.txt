cmake_minimum_required(VERSION 2.8.3)
project({packageName})

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
{forallcomponent}
  {componentPackage}
{endforallcomponent}
)

# protected region additional user defined REQUIREMENTS begin #
# protected region additional user defined REQUIREMENTS end #


###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package()

###########
## Build ##
###########

# protected region additional user defined BUILD STATEMENTS begin #
# protected region additional user defined BUILD STATEMENTS end #

##########
## Test ##
##########

if (CATKIN_ENABLE_TESTING)
  find_package(rostest REQUIRED)
{forallcomponent}
{ifpublisher}
  add_rostest(test/{componentName}_pub.test)
{endifpublisher}
{ifcyclicPublisher}
  add_rostest(test/{componentName}_hz_loop.test)
{endifcyclicPublisher}
{ifdynParameter}
  add_rostest(test/{componentName}_dyn_param.test)
{endifdynParameter}
{endforallcomponent}
endif()

# protected region user Cmake macros begin #
# protected region user Cmake macros end #
