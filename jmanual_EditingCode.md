# Editing a class #
  * If you edit a significant amount of similar items within a class, update the topmost comment block (before package and import declarations).
  * The @Edit will be the latest code change notes.
  * Update version number after each code change.

```
/*
* Point.java
* @version 1
* @author dykstran
* @edit zastrowm Removed setters since not all classes will allow setters
* @review username 1
*/
```

# Editing a method #
  * If you edit a single method or algorithm, update that method's comment.

```
/**
* This method does some stuff.
* @param x The thing to do stuff to.
* @return The thing to which stuff was done.
* 
* @author dykstran
* @edit zastrowm Changed the way stuff was done.
*/
```