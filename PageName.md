#Step by Step Instructions to Build and Compile IMP from the C Code and run it.


# A Guide to the C #
DON’T PANIC

 
Located in the root directory of the IMP repository is a folder labeled trunk (this should not surprise you). Inside of the trunk folder are three more folders (this might surprise you).  Check out this folder (the trunk folder) onto your local filesystem.  Do not re-arrange any subfolders or files with in the folder.  The trunk folder is organized in a way the IDE you will be using, Open Watcom, sees as a project workspace.

This guide will walk you through the process of installing the IDE, Open Watcom, making the different libraries of IMP, and finally making an executable of IMP.  Then once you have the executable, we’ll tell you how to run the 16-bit executable on 64-bit Windows 7 (which is a trick in itself).  The following instructions assume that you are running on 64-bit Windows 7 Professional.  Instructions for Windows XP are at the end.  No instructions exist for Windows Vista, Mac OS or Linus.

## Open Watcom Installation ##

These instructions assume installation on Windows 7 64-bit.  These instructions might work for 32-bit Windows 7.  This author assumes no responsibility for those running 32 bit.
In the folder you checked out from the repository, navigate to the lib folder and open up the Open Watcom folder.  Without wincing, double click the executable.
  1. Select the ‘I Agree’ button on the license agreement
  1. Choose the default installation directory
  1. On the next window pop-up,
    1. Select the ‘Include 16-bit compilers’ checkbox box
    1. Click the button labeled ‘Target’
      1. Select the checkbox labeled ‘DOS’
      1. Press the button labeled ‘OK’
    1. Press the ‘Next’ button
  1. You should see ‘Setup will now copy any selected files’ on a new pop-up window
    1. Press the ‘Next’ button
  1. It will now install, don’t get up
  1. A window might pop up that asks if Setup can modify environment variables in the registry for you.
    1. Select ‘Make all the modifications for you’ (unless you want headaches later)
    1. Press the ‘OK’ button
  1. A new window will pop up that asks to if Setup can modify associations for you.
    1. Select the ‘Modify Associations’ option
    1. Press the ‘OK’ button
  1. You’ll get a message that tells you that Setup is complete.  It’ll ask you to reboot your computer.  Reboot your computer now, unless you need to save things first.

## Opening the project workspace ##

If you accepted all the default installations settings, you should be able to start the OpenWatcom IDE by finding the link in the start menu (under the Open Watcom folder, it’ll be labeled IDE).  If you didn’t accept the default installation settings, good luck.
  1. Once in the IDE, go to File > Open Project
  1. Go to the directory where you checked out the directory from the repository (Remember, it was the trunk directory from the root directory)
  1. Go inside the folder labeled workspace inside of the IMP folder
  1. Inside of the workspace folder is a file called imp.wpj. This is the project file. Open this project file.

## Building and Compiling IMP ##

Once inside the project, you will be bombarded with windows that contain lists of files.  These are the different libraries of IMP.  They need to be made and compiled in the proper order.
  1. Go to Actions>Mark All Targets for Remake
  1. Now go to Windows > More Windows
    1. Each entry that you see labeled **.lib in the More Windows window needs to be made first
    1. Bring each**.lib labeled window into focus in turn and press F4 (this makes the lib file) (F4 is mapped to Target>Make).
    1. After all the lib files have been made, you can make the IMP executable.
      1. Go to the window titled imp.exe and press F4.
      1. Go to the window titled eclplt.exe and press F4 (this is a program that runs example problems for IMP).
  1. In the workspace directory (where you opened the project file) is where the .exe’s are created.
    1. Navigate to the workspace directory in the IMP directory.  There will be a lot of files there.  The following file types can be deleted (and probably should be, don’t check them into the repository)
      1. .OBJ
      1. .LB1
      1. .LIB
      1. .Lk1
      1. .MAP
      1. .MK
      1. .MK1
      1. .SYM
    1. Save the following file types
      1. .tgt
      1. .wpj
      1. .exe
  1. Now that you have the .exe’s, double click to run them.
    1. Note, the above step is impossible to do because IMP was designed to run on DOS.
      1. The project is set up to compile the IMP program for DOS (that’s 16-bit) with the 4G extensions (a 32 bit extension to DOS that allows programs to access more than 640KB of memory (up to 64 MB))
    1. Normally running this program wouldn’t be an issue on Windows OS’es.  However, Windows 7 no longer contains the NTVDM (NT Virtual Dos Machine).  It can’t run legacy programs like IMP natively.
    1. In order to run IMP, we’ll use the Windows XP mode of Windows 7.

## Running Windows XP Mode On Windows 7 ##

There is a trick to getting IMP to run in Windows XP Mode due to the implementation of Windows XP Mode on Windows 7.

Follow this link here:
http://www.microsoft.com/windows/virtual-pc/download.aspx

The link will get you to everything you need to download for Windows XP Mode.  This does require you to validate your copy of windows (which shouldn’t be a problem for you, should it?)

After installing the Validation update, you might have to restart your browser and/or computer ( I don’t know why, it doesn’t seem like you should, but I had to)

Download everything and install it.

Specific information for how Windows XP works is available here.   Read while installing (for best time efficiency)

http://www.withinwindows.com/2009/04/25/windows-xp-mode-internals-part-1-overview/
http://www.withinwindows.com/2009/04/28/windows-xp-mode-internals-part-2-application-publishing-magic/

## Using Windows XP Mode ##

  1. In your start menu, navigate to the Windows Virtual PC Folder, open it and click on the link to Windows XP Mode
  1. You’ll have to accept a license agreement, create an account, select an update pattern and then click Start setup.  It’ll now do some magical setup stuff.
  1. After setup, it should bring you into the familiar Windows XP environment.
  1. Open Windows Explorer on the Windows XP VM.  Click on the Computer Node.  You should see icons that correspond to your partitions that Windows 7 is installed on
  1. Using these icons, navigate to the directory where you checked out the IMP directory from the repository.
    1. Get the IMP.exe and copy it to the desktop.
    1. You still won’t be able to run it
  1. To Run IMP
    1. Go to the bin directory of the directory you checked out from the repository
      1. Get a file called DOS4GW and copy it onto the desktop where IMP should be copied (the purpose of this is to make sure both files stay relative to each other)
    1. Go to Control Panel > Performance and Maintenance > Administrative Tools > Services.
      1. Find the service called Terminal Services, go to its properties and change its startup type to disabled
      1. Note, doing the above will turn off Application Publishing (and by extension Remote Applications.  Read the above links if this confuses you).  This means that Windows 7 and Windows XP Mode won’t talk to each other and Windows XP Mode becomes just another virtual machine
      1. The reason Terminal Services has to be disabled is because it prevents IMP from running in full screen mode (which it does no matter your needs or wants)
    1. Reboot the Windows XP Mode System
    1. When it starts back up, double click IMP.
    1. The executable should run now, type in ‘graphic’ for the display mode.
    1. For instructions on the commands to use with IMP, see another document.

If you don’t have IMP running at this time, please make sure you followed all of the instructions

## Windows XP ##

With a native installation, IMP should run no problem.  If you encounter any issues, try following the instructions above that disable the Terminal Service service in the Control Panel.  Also try placing the DOS4GW executable in the same directory as the imp executable.  Anything beyond this and the author of this document cannot help as he is not running Windows XP natively anymore.