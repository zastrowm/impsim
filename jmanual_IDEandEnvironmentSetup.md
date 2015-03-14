## Overview ##
The project is setup to use the most recent version of Eclipse (Indigo) found [here](http://www.eclipse.org/downloads/).  Download the Eclipse IDE for Java Developers which has several plugins the project uses pre-installed.  We also use several XMLs for code cleanup and formatting.
### Procedure ###
  1. IMP currently is targeted at Java 1.6 since Cobertura cannot run on 1.7 yet. You can have 1.7 installed as your main JDK and JRE and IMP will run fine since the project file is set to 1.6 compliance.  However there will be a warning about not having a "strictly compatible" jre available.
    * To make this go away (so you can have no yellow warning flag on your project explorer view) just install JDK 1.6.
    * During the install you can safely deselect "public JRE" (assuming you already have the public 1.7 JRE) and "source code" to avoid some cruft.
    * After the 2nd JDK is installed you'll have to add it to eclipse.
      1. Window -> Preferences -> Java -> Installed JREs -> Add -> Standard VM
      1. Browse to where you installed 1.6 by hitting the Directory button.
      1. Finish -> Ok (you can leave 1.7 checked as the default jre)
  1. Download Eclipse (Eclipse IDE for Java Developers)
  1. Place the CoffeeBytes (attached) code folding JAR into your plugins folder
  1. Open Eclipse, go to Help->Eclipse Marketplace...
    * Search for and install Eclipse Color Theme
  1. Install Eclipse Plugins: Help->Install New Software...
    * Add Antler http://antlrv3ide.sourceforge.net/updates/
    * Add JAutoDoc for JavaDoc auto-generation http://jautodoc.sourceforge.net/update/
    * Add eCobertura for code coverage http://ecobertura.johoop.de/update
    * Add "Eclipse Plug-In Development Environment". Work with: "http://download.eclipse.org/releases/indigo" "Search "Plug-In".
    * Add "PDE/API Tools Environment Descriptions". Work with: "http://download.eclipse.org/releases/indigo" "Search "PDE".
  1. Add the OPTIMIZE tag to the Task Tags
    * See the [Commenting Standards](jmanual_CommentStandards.md) if you are unsure of how to do this
  1. Add custom code folding
    * See the [Formatting Standards](jmanual_FormattingStandards.md) if you are unsure of how to do this
  1. Add XMLs for formatting and code cleanup
    * Both XMLs are in the tools repo (or navigate to https://opal.msoe.edu/svn/physicsengine-tools/trunk/ and download them manually)
    * In Eclipse go to Window->Preferences->Java->Code Style
    * Select Code Cleanup->Import... and select SDL Clean Up.xml
    * Select Formatter->Import... and select SDLJavaFormat.xml
    * Press OK
  1. Edit the Save Actions in Eclipse
    * Window->Preferences->Java->Editor->Save Actions
    * Check the boxes to Format all lines and Organize Imports

### Setting up the Core Project ###

  * See the [maven install walkthrough](jmanual_MavenInstallWalkthrough.md).

Maven will automatically pull in up-to-date libraries that IMP depends on.  If you have errors, go to Project->Clean and clean the current project.  It should build with no errors.
Sometimes Maven uses the wrong Java source.  It should use the JDK, however if you have the JRE installed as well it may cause issues.  If you are still experiencing build issues, uninstall the JRE through the Windows Control Panel and install the most up to date JDK (the JDK is a superset of anything you needed the jre for).

### Setting up the Plugin Project ###

  * See the [plugin setup guide](jmanual_PluginSetup.md).

This guide talks you through on how to import the plugin and then on how to run it from within the Eclipse environment.


### Using the IDE Integrations ###
#### JAutoDoc ####
  * Press Alt+Shift+J to auto generate method comments when a method is selected
#### Color Theme ####
  * The current team suggests using a dark color theme to save your eyes
    * Window->Preferences->General->Appearance->Color Theme
    * Most of the team uses Obsidian
#### eCobertura ####
  * Right click on a package, source, or project and select Cover As...JUnit Test from the context menu
  * Coverage results will be in an output window, no files are created from the Eclipse plugin
    * Window->Show View and look for the Coverage Session View