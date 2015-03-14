# Developing IMP How To #

## Software Required ##
  * Java for Developers (not classic) 3.7.1
  * JDK 6 or 7 (JRE is not sufficient)
    * The JDK you install must match the eclipse you use platform wise (x86 vs x86\_64)
  * SVN

## Get the source and jars ##
  1. Checkout the physicsengine project from https://opal.msoe.edu/svn/physicsengine
  1. Checkout the physicsengine-tools project from https://opal.msoe.edu/svn/physicsengine-tools
  1. Download JOGL and Gluegen from jogamp.org http://jogamp.org/deployment/jogamp-current/jar/ or http://imp.msoe.edu/files/ (Custom zips of just the jars you need) you need 4 files:
    * gluegen-rt.jar
    * jogl.all.jar
    * gluegen-rt-natives-PLATFORM.jar (e.g. gluegen-rt-natives-windows-amd64.jar)
    * jogl-all-natives-PLATFORM.jar (e.g. jogl-all-natives-windows-amd64.jar)
  1. Find out where your System.getProperty("user.home") is defined to. On the school image this defaults to "D:\MyDocs" and a pristine windows defaults to "C:\Users\USERNAME".
    * Unzip the jogl zip to ${user.home}/maven-locals (e.g. "D:\MyDocs\maven-locals"). Make sure the jars are not in a subdir of maven-locals.

## Configure Eclipse ##
  1. Setup the workspace jre to use the jdk you installed:
    * Launch Eclipse -> Window menu -> Preferences -> Java -> Installed JREs
  1. Make sure the jdk is checked. If you don't see it listed hit add and find its install folder.

## Import the Project ##

  1. File -> Import -> Maven -> Existing Maven Projects -> Next
  1. Root Directory -> Browse -> Select physicsengine/trunk -> Finish
    * If it whines about not having the connectors then quit the process and add them.
  1. Help -> Install New Software -> Work with ->
    * https://repository.sonatype.org/content/repositories/forge-sites/m2e-extras/0.15.0/N/0.15.0.201202141716/
    * "Add" -> Give it a name like "m2e Extras"
  1. Check the "m2e connector for antlr" box -> Next -> Next -> I accept the agreement -> Finish.
  1. Try Step 1.0 again.


## Import Maven and External Dependencies ##
  1. Right click project root folder -> Run As -> maven test
  1. This downloads all the maven plugins and external jars (except jogl).
    1. If you freeze up at "Downloading..." some random file stop the process by hitting the red square and begin again.
      * This could be caused by any Anti-Virus software you have installed.  A known Anti-Virus that caused issues was AVG.
    1. Right click project root folder -> Maven -> Update Configuration.
      * You can try checking the "Force" checkbox I'm not sure that this helps the process.
    1. You may have to keep doing this several times. It'll get through the downloading stuff eventually.
    1. You'll have to re-add the JOGL jars to the build path (after you finally make it through)