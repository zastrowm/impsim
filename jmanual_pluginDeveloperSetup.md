## Overview ##
The plugin was designed for Eclipse Indigo, but should run on any Eclipse platform of 3.4 or later (unless the newer API does not support backwards compatibility).  You need to be running a version of eclipse that supports Plug-in Projects, the '''classic''' version of Eclipse has this and so do some others.  To make sure you have an Eclipse that will work for Plug-in Development download the classic found on the Eclipse download page [here](http://www.eclipse.org/downloads/packages/eclipse-classic-372/indigosr2).

## Setting Up ##
If you have Eclipse for Java Developers installed you will need to install additional Eclipse plugins to allow for Eclipse plugin development.
  1. Run Eclipse as Administrator mode.
  1. Start by going to Install new Software under the help menu.
  1. Select the site Indigo - http://download.eclipse.org/releases/indigo .
  1. Once it has loaded the available installs search for the following and select them:
    * Eclipse Plug-in Development Environment
    * PDE/API Tools Environment Descriptions
  1. Install these plugins.
  1. Restart Eclipse.

## Procedure ##
You can open the Plugin Project by importing it into the workspace.

### Method 1: Importing ###
  1. Using the classic (or another supporting version), navigate to the import menu (File->Import or in Project Explorer rightClick->Import)
  1. Under General select "Existing Project into Workspace" hit Next
  1. Click on browse to browse for the root directory.  Select **\physicsengine\trunk\src\main\java\imp\ui** from the checked out copy of the repository on your machine.
  1. Uncheck "Copy projects into workspace" and click Finish.

## Add reference to IMP core jar ##
You need to build or [download](http://imp.msoe.edu/files/imp-20120403.jar) a jar of imp core for the plugin to reference. Do this by adding it as an external lib on the build path.

## Showing the Views ##
This is the steps to actually see the plugin views inside of Eclipse once you get the plugin working.  There are 2 methods to showing the views, either use the IMP Perspective or manual show each view.

### Method 1: Showing the Perspective ###
  1. Open up Eclipse
  1. Select Window drop down menu from navigation bar
  1. From the Window menu select Show Perspective and click other
  1. Select IMP from the choices and Click ok

### Method 2: Manual Display ###
  1. Look at the file menu bar on top, select Window
  1. from the Window drop down click on Show View -> Other
  1. Select the "Other" Folder (TODO: Change to IMP Folder once code is updated)
  1. Select Both imp views (impCanvasView and impPropertiesView)