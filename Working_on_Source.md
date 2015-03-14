# Instructions on how to contribute to the imp core #
So you want to help contribute to the imp core.  That is very easy to do.  All you need to do is follow these simple steps:

  1. Create a local repository on your computer.
  1. Do a SVN Checkout on the repository.  The url of the core is:
> > impsim.googlecode.com/svn/impsim-java
  1. Download [Eclipse IDE for Java Developers](http://www.eclipse.org/downloads/) for your version of windows or what ever operating system you use.
  1. Install Eclipse
  1. Run Eclipse and when it asks you for your work space point it to the trunk folder in your repository
  1. Import the project as an Existing Maven Project
  1. Install the m2e connector for antlr
    1. Go to Install new Software in Eclipse
    1. Add this site:  https://repository.sonatype.org/content/repositories/forge-sites/m2e-extras/0.15.0/N/0.15.0.201202141716/
    1. Install only the m2e connector for antlr
  1. Right click on the project and go down to the maven sub menu and click on update project configuration.
  1. When that window comes up just click ok
  1. Then right click on the project again and go down to Run As submenu and then select Maven install.
  1. Add in the corresponding jogl jars to your build path and you are done.
    1. [JOGL jars found here](http://jogamp.org/deployment/jogamp-current/archive/)
    1. In your eclipse project, add IMP, Jogl, and Gluegen to your project build path.
      1. Right click your project
      1. Go to Build Path -> Configure Build Path
      1. Click "Add External  JARs" in the Libraries tab
      1. Select IMP\_1.0.jar, jogl-all.jar, and gluegen-rt.jar libraries

Note that for the Jogl and Gluegen libraries, you will also need to include the appropriate platform natives. There should be a total of five external jars on your build path including the IMP library after this step.