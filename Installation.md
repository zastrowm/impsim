# Introduction #

IMP is a DOS program and so it needs....DOS to run.  Current operating systems have a few options.

  * Windows 7: Dosbox with a dos extender (dos32a) work fine.
  * Windows XP: IMP works fine with XP's dos mode.  Running in XP in Virtual Box has been confirmed to work as well.
  * Linux: Dosbox and dos32a should work fine here too but this has yet to be tested.


# Details #

## Windows 7 ##

### Installing ###

  1. Download and install Dosbox.  http://www.dosbox.com/
  1. Create a folder for dos stuff. Ex: C:\Users\John\dos
  1. Download dos extender (dos4gw stand in ) dos32a. http://dos32a.narechk.net/index_en.html
  1. Put the extracted dos32a\binw\dos32a.exe into folder you created before C:\Users\John\dos\dos32a.exe
  1. Copy dos32a.exe and name the copy dos4gw.exe (also in the dos folder).
  1. Download imp.exe and put it in the C:\Users\John\dos folder
  1. create a new shortcut and you're all set.
```
"C:\Program Files (x86)\DOSBox-0.74\DOSBox.exe" "C:\Users\John\dos\imp.exe"
```

## Windows XP ##

  * You should be able to just run imp.exe from the terminal
  * You can download a virtual machine to run Windows XP if you don't want to use it as your base install. We recommend VirtualBox http://www.virtualbox.org/