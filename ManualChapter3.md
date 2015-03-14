

# Chapter 3: Definition Statements #
The various definition statements recognized by the IMP interpreter are presented in this chapter. The first word of each statement is a keyword instructing the IMP system to interpret the remainder of the statement according to one of the formats on the following pages.

## The <tt>LINK</tt> Statement ##
The <tt>LINK</tt> statement defines one rigid link of the system.

### Format ###
> <tt>LINK</tt> = link name
where _link name_ refers to an alphanumeric name given to the link.

### Example ###
> <tt>LINK</tt> = PART
defines a link named _PART_ to be a part of the system model.

### Notes ###
  1. Use of the <tt>LINK</tt> statement is optional. Links may also be defined by the use of their _link name_ in a statement defining a joint.
  1. If the _link name_ used in a <tt>LINK</tt> statement has not been previously defined, a new link is created and assigned that _link name_.
  1. No other link may be defined having the same _link name_. If an attempt is made to do so, no new link results; a warning message is printed instead.
  1. Each link of the system has attached to it a unique coordinate system which moves whenever the link moves. At the time of its first creation by a <tt>LINK</tt> statement or a joint definition statement, this link coordinate system is assumed coincident with the global coordinate system. It may be moved to another location or orientation by use of a <tt>DATA LINK</tt> statement.
  1. One or more <tt>SHAPE</tt> statements may be given to provide shape(s) to the link defined with this _link name_. If such a <tt>SHAPE</tt> statement is not found, the _link name_ has no defined shape. Points may still be attached to the link in such a case, however, and their locations may still be defined relative to the link coordinate system. Using such points, a schematic representation may be drawn for the link. However, a solid shape for the link is not known, and collision with other link shapes cannot be detected.
  1. Each _link name_ defined must be attached, either directly or indirectly, by properly defined joints to the fixed link. If a _link name_ does not appear in at least one valid joint definition statement, the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement causes a message to be printed and that link (along with any data dependent on it) to be deleted from the system.


## The <tt>GROUND</tt> Statement ##
The <tt>GROUND</tt> statement designates the link which remains stationary, that is, the link which contains the global coordinate system.

### Format ###
> <tt>GROUND</tt> = link name
where _link name_ is the alphanumeric name assigned to the fixed link.

### Example ###
> <tt>GROUND</tt> = FRAME
The link named _FRAME_ is selected as the fixed link of the system.

### Notes ###
  1. The use of the <tt>GROUND</tt> statement is optional. Although every IMP simulation model must contain a fixed link, IMP recognizes the name <tt>BASE</tt> as designating the fixed link unless overridden by a <tt>GROUND</tt> statement.
  1. Not more than one _link name_ may be defined as stationary. If the <tt>GROUND</tt> statement appears more than once, only the most recent <tt>GROUND</tt> statement is in effect at any time. Thus, the <tt>GROUND</tt> statement can be used to perform kinematic inversion.
  1. All remaining links of the system must be attached by properly defined joints to the fixed link. If a _link name_ does not appear in at least one valid joint definition statement, the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement causes a message to be printed and the link (and any data dependent on it) to be deleted from the system model.
  1. Each link of the system has attached to it a unique coordinate system which moves whenever the link moves. At the time of its first creation by a <tt>LINK</tt> statement or a joint definition statement, this link coordinate system is assumed to be coincident with the global coordinate system. It may be moved to another location or orientation by use of a <tt>DATA LINK</tt> statement.


## The <tt>SOLID READ</tt> Statement ##
The <tt>SOLID READ</tt> statement defines one or more solid shapes with data stored in a previously prepared file.

### Format ###
> <tt>SOLID READ</tt> (solid name) = filename
where _solid name_ refers to the alphanumeric name given to the solid, and _filename_ is the name of the file containing data for the solid to be read. The file may be in either the JML standard 3-D Solid file format (Appendix A) with _filename_ extension of _.geo_, or in the stereo-lithography (<tt>STL</tt>) standard file format with _filename_ extension of _.stl_.

### Example ###
> <tt>SOLID READ</tt> (PART) = shape.geo
defines a solid named _PART_ with data from a previously prepared JML format file named _shape.geo_.

### Notes ###
  1. The solid named _solid name_ defined by _filename_ is assumed to be attached to the stationary link unless defined otherwise by a subsequent <tt>SHAPE</tt> statement.
  1. The data read from the file is assumed referenced to the coordinate system of the link to which the solid is attached unless modified by a subsequent <tt>DATA SHAPE</tt> statement.
  1. The _filename_ used must refer to a previously prepared file containing data for the solid shape; this file must be prepared in either the JML standard 3-D Solid file format (Appendix A) with the _filename_ extension of _.geo_, or in the stereo-lithography (<tt>STL</tt>) standard file format with the _filename_ extension of _.stl_. If such a file is not found or cannot be read, no solid is created; a message is printed.
  1. If the JML standard file format is used it is possible that more than one solid may be contained in the file. If so, multiple solid shapes are created in the system model with _solid names_ defined in the file. The _solid name_ defined in the <tt>SOLID READ</tt> statement will override the _solid name_ from the file for the first solid shape read.


## The <tt>SHAPE</tt> Statement ##
The <tt>SHAPE</tt> statement defines a geometry for a link or for one part of a link.

### Format ###
> <tt>SHAPE</tt> (link name) = solid1, solid2, ...
where _link name_ refers to the alphanumeric name given to the link and each _solid name_ is the name of a previously defined solid defining the shape of that part of the link.

### Example ###
> <tt>SHAPE</tt> (PART) = bar, ball
defines the shape of a link named _PART_ to be composed of two previously defined solids named _bar_ and _ball_.

### Notes ###
  1. When each solid is first defined by a <tt>SOLID</tt> statement it is assumed to be part of the fixed link until it is attached to some other link by a <tt>SHAPE</tt> statement.
  1. It is necessary to refer to each _solid name_ in a <tt>SHAPE</tt> statement for the attachment of that solid to its corresponding _link name_.
  1. A maximum of 33 _solid names_ may be defined in a single <tt>SHAPE</tt> statement (with continuation lines). There is no restriction, however, on defining additional _solid names_ attached to the same _link name_ with one or more additional <tt>SHAPE</tt> statements.
  1. If the same _solid name_ is used in more than one <tt>SHAPE</tt> statement, the most recent occurrence of that _solid name_ takes precedence and earlier relationships are replaced.
  1. Each _solid name_ may be given a location on the _link name_ by a subsequent <tt>DATA SHAPE</tt> statement. If this is not done before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, then _shape names_ are defined with their coordinate data measured with respect to the link coordinate system.
  1. _Solid names_ attached to different _link names_ may not be defined in the same <tt>SHAPE</tt> statement.
  1. The _link name_ referred to in a <tt>SHAPE</tt> statement must have appeared in at least one previous <tt>LINK</tt> statement or a statement defining a joint. If not, the <tt>SHAPE</tt> statement is ignored and a message is printed.


## The <tt>CONTACT</tt> Statement ##
The <tt>CONTACT</tt> statement defines a logical association between two solid shapes of different links which may be monitored for possible collision during the motion of the system.

### Format ###
> <tt>CONTACT</tt> (solid name, solid name) = contact name
where each _solid name_ refers to the alphanumeric name given to one of the two solid shapes and _contact name_ is an arbitrarily chosen alphanumeric name assigned to the contact.

### Example ###
> <tt>CONTACT</tt> (KNOB, POCKET) = BUMPER
defines a contact named _BUMPER_ between two shapes named _KNOB_ and _POCKET_.

### Notes ###
  1. <tt>A CONTACT</tt> statement is never required, but may be useful to form an association between two link shapes of the system such that a possible collision may be detected and proper momentum transfer can be simulated.
  1. Each contact in the system must be defined by a separate <tt>CONTACT</tt> statement.
  1. No other contact may be defined having the same _contact name_. An attempt to do so results in the deletion of the previously defined contact of the same _contact name_ (and all data associated with it); a warning message is printed.
  1. The same _solid name_ may appear in more than one statement defining a contact.
  1. Each <tt>CONTACT</tt> statement must refer to two distinct _solid names_ of solids on two different links. An attempt to associate a solid shape with itself or with another solid shape on the same link causes the statement to be ignored and a message to be printed.
  1. The order in which the two _solid names_ appear is arbitrary.
  1. Each <tt>CONTACT</tt> statement should be associated with a corresponding <tt>DATA CONTACT</tt> statement. If an appropriate <tt>DATA CONTACT</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the coefficient of restitution normal to the surface is unity and all other contact data is zero. No message is printed.


## The <tt>IMPACT</tt> Statement ##
The <tt>IMPACT</tt> statement is used to specify the nature of the change of momentum equations to be used at the moment of collision between contacting solids defined by <tt>CONTACT</tt> statements.

### Format ###
> <tt>IMPACT</tt> = ktangent, kmoment, ktorsion
where _ktangent_, _kmoment_, and _ktorsion_ define the types of models to be used for tangential, moment, and torsional impulses, respectively, at modeled contacts; each may be chosen as 0 for undefined, 1 for a coefficient of restitution model, 2 for a Coulomb friction model, or 3 for a bilinear restitution and Coulomb friction model.

; Example: <tt>IMPACT</tt> = 2, 1, 3
specifies that the mathematical model used for simulating impacts at each <tt>CONTACT</tt> will be Coulomb friction for any tangential impulses, coefficient of restitution for moment impulses, and bilinear for torsional impulses.

### Notes ###
  1. An <tt>IMPACT</tt> statement should be defined for any model which includes a <tt>CONTACT</tt> statement. If this does not appear before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, any tangential, moment, or torsional impulses found within contacts are ignored.
  1. If more than one <tt>IMPACT</tt> statement is encountered, the later statement takes precedence; earlier data are replaced; no message is printed.
  1. If integer values other than 0 through 3 are used for _ktangent_, _kmoment_, or _ktorsion_, no error is detected immediately. However 0 is used for the offending value and corresponding impulses are ignored; no message is printed.


## The <tt>RIGID</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_1.png' height='400px' />
_Figure 3-1:_ Example of a rigid joint.
The <tt>RIGID</tt> statement defines a non-movable joint connecting two links of the system (see figure 3-1).

### Format ###
> <tt>RIGID</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>RIGID</tt> (LK1, LK2) = WELD
defines a rigid joint named _WELD_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each rigid joint in the system must be defined by a separate <tt>RIGID</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each <tt>RIGID</tt> statement must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA RIGID</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The two coordinate systems may be located and oriented arbitrarily but both coordinate systems must be coincident (see figure).
  1. If an appropriate <tt>DATA RIGID</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system. No message is printed.
  1. The <tt>RIGID</tt> joint is immobile and has no joint variables.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the signs of the constraint force and torque components within the joint. (See, for example, the <tt>PRINT FORCE</tt> statement).


## The <tt>XPIN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_2.png' height='400px' />
_Figure 3-2:_ Example of a pinned joint parallel to the X axis.
The <tt>XPIN</tt> statement defines a pinned joint connecting two links of the system (see figure 3-2), with its pin axis initally parallel to the global X axis.

### Format ###
> <tt>XPIN</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>XPIN</tt> (LK1, LK2) = PIN
defines a pinned joint named _PIN_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each X-oriented pin joint in the system must be defined by a separate <tt>XPIN</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA XPIN</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident, the local u and u' axes must be collinear and initially parallel to the global X axis and must be directed along the joint axis, and both local u axes must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA XPIN</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system. No message is printed.
  1. The joint variable for an <tt>XPIN</tt> joint is the angle from the positive local v axis to the positive local v' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local u,u' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (rotation of the joint).


## The <tt>YPIN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_3.png' height='400px' />
_Figure 3-3:_ Example of a pinned joint parallel to the Y axis.
The <tt>YPIN</tt> statement defines a pinned joint connecting two links of the system (see figure 3-3), with
its pin axis initially parallel to the global Y axis.

### Format ###
> <tt>YPIN</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>YPIN</tt> (LK1, LK2) = PIN
defines a pinned joint named _PIN_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each Y-oriented pin joint in the system must be defined by a separate <tt>YPIN</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA YPIN</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident, the local v and v' axes must be collinear and initially parallel to the global Y axis and must be directed along the joint axis, and both local v axes must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA YPIN</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system; no message is printed.
  1. The joint variable for a <tt>YPIN</tt> joint is the angle from the positive local w axis to the positive local w' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local v,v' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (rotation of the joint).


## The <tt>ZPIN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_4.png' height='400px' />
_Figure 3-4:_ Example of a pinned joint parallel to the Z axis.
The <tt>ZPIN</tt> statement defines a pinned joint connecting two links of the system (see figure 3-4), with
its pin axis initially parallel to the global Z axis.

### Format ###
> <tt>ZPIN</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>ZPIN</tt> (LK1, LK2) = PIN
defines a pinned joint named _PIN_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each Z-oriented pin joint in the system must be defined by a separate <tt>ZPIN</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA ZPIN</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident, the local w and w' axes must be collinear and initially parallel to the global Z axis and must be directed along the joint axis, and both local w axes must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA ZPIN</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system. No message is printed.
  1. The joint variable for a <tt>ZPIN</tt> joint is the angle from the positive local u axis to the positive local u' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (rotation of the joint).


## The <tt>REVOLUTE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_5.png' height='400px' />
_Figure 3-5:_ Example of a pin joint connecting two links.
The <tt>REVOLUTE</tt> statement defines a pin joint connecting two links of the system (see figure 3-5).

### Format ###
> <tt>REVOLUTE</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>REVOLUTE</tt> (LK1, LK2) = PIN
defines a pinned joint named _PIN_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each revolute joint in the system must be defined by a separate <tt>REVOLUTE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each <tt>REVOLUTE</tt> statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA REVOLUTE</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident the local w and w' axes must be collinear and must be directed along the joint axis and both local w axes must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA REVOLUTE</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system; no message is printed.
  1. The joint variable for a <tt>REVOLUTE</tt> joint is the angle from the positive local u axis to the positive local u' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (rotation of the joint).


## The <tt>XSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_6.png' height='400px' />
_Figure 3-6:_ Example of a sliding joint with its axis parallel to the X axis.
The <tt>XSLIDE</tt> statement defines a sliding joint connecting two links of the system (see figure 3-6), with its axis initially parallel to the global X axis.

### Format ###
> <tt>XSLIDE</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>XSLIDE</tt> (LK1, LK2) = SLIP
defines a sliding joint named _SLIP_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each X-oriented sliding joint in the system must be defined by a separate <tt>XSLIDE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA XSLIDE</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local u and u' axes must be collinear and parallel to the global X axis and must both be directed parallel to the relative motion of the joint. Both local u axes must have the same positive sense, and the local v and v' axes must be parallel and must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA XSLIDE</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system; no message is printed.
  1. The joint variable for an <tt>XSLIDE</tt> joint is the distance from the positive local v axis to the positive local v' axis. It has units of length and is considered positive when in the same direction as the positive local u,u' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (sliding motion of the joint).

## The <tt>YSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_7.png' height='400px' />
_Figure 3-7:_ Example of a sliding joint with its axis parallel to the Y axis.
The <tt>YSLIDE</tt> statement defines a sliding joint connecting two links of the system (see figure 3-7), with its axis initially parallel to the global Y axis.

### Format ###
> <tt>YSLIDE</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>YSLIDE</tt> (LK1, LK2) = SLIP
defines a sliding joint named _SLIP_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each Y-oriented sliding joint in the system must be defined by a separate <tt>YSLIDE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA YSLIDE</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local v and v' axes must be collinear and initially parallel to the global Y axis and must both be directed parallel to the relative motion of the joint. Both local v axes must have the same positive sense, and the local w and w' axes must be parallel and must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA YSLIDE</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system. No message is printed.
  1. The joint variable for a <tt>YSLIDE</tt> joint is the distance from the positive local w axis to the positive local w' axis. It has units of length and is considered positive when in the same direction as the positive local v,v' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (sliding motion of the joint).


## The <tt>ZSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_8.png' height='400px' />
_Figure 3-8:_ Example of a sliding joint with its axis parallel to the Z axis.
The <tt>ZSLIDE</tt> statement defines a sliding joint connecting two links of the system (see figure 3-8), with its pin axis initially parallel to be global Z axis.

### Format ###
> <tt>ZSLIDE</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>ZSLIDE</tt> (LK1, LK2) = SLIP
defines a sliding joint named _SLIP_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each Z-oriented sliding joint in the system must be defined by a separate <tt>ZSLIDE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA ZSLIDE</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear, and initially parallel to the global Z axis and must both be directed parallel to the relative motion of the joint. Both local u axes must have the same positive sense, and the local u and u' axes must be parallel and must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA ZSLIDE</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system. No message is printed.
  1. The joint variable for a <tt>ZSLIDE</tt> joint is the distance from the positive local u axis to the positive local u' axis. It has units of length and is considered positive when in the same direction as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (sliding motion of the joint).


## The <tt>PRISM</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_9.png' height='400px' />
_Figure 3-9:_ Example of a sliding joint connecting two links.
The <tt>PRISM</tt> statement defines a sliding joint connecting two links of the system (see figure 3-9).

### Format ###
> <tt>PRISM</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>PRISM</tt> (LK1, LK2) = SLIP
defines a sliding joint named _SLIP_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each prismatic joint in the system must be defined by a separate <tt>PRISM</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA PRISM</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear and must both be directed parallel to the relative motion of the joint. Both local w axes must have the same positive sense, and the local u and u' axes must be parallel and must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA PRISM</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system. No message is printed.
  1. The joint variable for a <tt>PRISM</tt> joint is the distance from the positive local u axis to the positive local u' axis. It has units of length and is considered positive when in the same direction as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (sliding motion of the joint).


## The <tt>GEAR</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_10.png' height='400px' />
_Figure 3-10:_ Example of a gear joint connecting two links.
The <tt>GEAR</tt> statement defines a gear joint between two links of the system (see figure 3-10).

### Format ###
> <tt>GEAR</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the gear joint.

### Example ###
> <tt>GEAR</tt> (SUN, PLAN) = SPUR
defines a gear joint named _SPUR_ connecting two links named _SUN_ and _PLAN_.

### Notes ###
  1. Each gear joint in the system must be defined by a separate <tt>GEAR</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must coincide with the centers of the first and second _link names_, respectively, and must both be positively directed on the same side of the gears. The local u,v and u',v' axes must all lie in a common plane parallel to the plane of motion of the two gears. The line of centers of the two gears through the local origins is defined as t and is positive in the sense defined from w to w'. The local u and u' axes must be chosen such that, at one position of the gear joint, positive local u, positive local u', and positive t all lie along the same line and have the same sense (see figure).
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system(s); no message is printed.
  1. A <tt>GEAR</tt> joint has one internal degree of freedom. The joint variable for a <tt>GEAR</tt> joint is the angle from the positive local u axis to positive t. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w axis.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variable (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the rotation of the joint variable.
  1. The gear ratio of each <tt>GEAR</tt> joint must be defined by a subsequent <tt>DATA GEAR</tt> statement.
  1. The simulation of the <tt>GEAR</tt> joint is treated as though they are two cylinders rolling against each other with no slip. This causes no problem in motion analysis; however, in force analysis, the gears are treated as having zero pressure angle.


## The <tt>BEVEL</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_11.png' height='400px' />
_Figure 3-11:_ Example of a bevel gear joint connecting two links.
The <tt>BEVEL</tt> statement defines a bevel gear joint between two links of the system (see figure 3-11).

### Format ###
> <tt>BEVEL</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>BEVEL</tt> (SUN, PLAN) = BVL
defines a bevel gear joint named _BVL_ connecting two links named _SUN_ and _PLAN_.

### Notes ###
  1. Each bevel gear joint in the system must be defined by a separate <tt>BEVEL</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must coincide with the pitch cone axes directed outward from their common apexes. The local u,v and u',v' axes must lie in the planes of the pitch circles of the first and second _link names_, respectively. The local u and u' axes must be chosen such that, at one position of the bevel gear joint, the positive local u axis is directed toward the pitch point and the positive local u' axis is directed away from the pitch point at that position of the bevel gears; u,w,w' and u' all lie in the plane defined by the two cone axes.
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. A <tt>BEVEL</tt> joint has one internal degree of freedom. The joint variable for a <tt>BEVEL</tt> joint is the angle from the positive local u axis to the positive local w' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w axis.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variable (see Note 7 above), and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the rotation of the joint variable.
  1. The gear ratio and pitch circle radius of each <tt>BEVEL</tt> joint must be defined by a subsequent <tt>DATA BEVEL</tt> statement.
  1. The simulation of a <tt>BEVEL</tt> joint is treated as though the two pitch cones are rolling against each other with no slip. This causes no problem in motion analysis; however, in force analysis, the bevel gears are treated as having zero presure angle.


## The <tt>RACK</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_12.png' height='400px' />
_Figure 3-12:_ Example of a rack and pinion joint connecting two links.
The <tt>RACK</tt> statement defines a rack and pinion joint between two links of the system (see figure 3-12).

### Format ###
> <tt>RACK</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>RACK</tt> (RAIL, WHEL) = MESH
defines a rack and pinion joint named _MESH_ connecting a link named _RAIL_ (the rack) with a link named _WHEL_ (the pinion).

### Notes ###
  1. Each rack and pinion joint in the system must be defined by a separate <tt>RACK</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. The first _link name_ must be that of the rack, and the second _link name_ refers to the pinion link the order is not arbitrary and cannot be reversed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local u axis must lie in the plane of the pitch circle of the pinion, along the pitch line of the rack, while the local w axis is perpendicular to the plane of the pitch circle and the local v axis is in the plane of the pitch circle and positively directed toward the pinion side of u. The local w' axis coincides with the center of the pitch circle and is parallel to and positively directed the same as w. The local u' and v' axes lie in the plane of and radiate from the center of the pitch circle of the pinion. The line parallel to u through the center of the pitch circle and positively directed in the same sense as u is defined as t. The local coordinate systems must be chosen such that, at one position of the <tt>RACK</tt> joint, the positive local u axis is aligned along positive t and the pinion center lies on the local v axis with positive v' directed in the same sense as the positive local v axis (see figure).
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. A <tt>RACK</tt> joint has one internal degree of freedom. The joint variable for a <tt>RACK</tt> joint is the distance from the v axis along positive t to the local v' origin. It has units of length and is considered positive when in the positive u direction.
  1. It is assumed that there is no limit on the travel of the joint variable.
  1. The pitch circle radius of the pinion must be defined by a subsequent <tt>DATA RACK</tt> statement.
  1. The simulation of a <tt>RACK</tt> joint is treated as though the pinion is a cylinder rolling without slip against a smooth plane for the rack. This causes no problem in motion analysis; however, in force analysis, the pinion is treated as having zero pressure angle.


## The <tt>SCREW</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_13.png' height='400px' />
_Figure 3-13:_ Example of a screw joint connecting two links.
The <tt>SCREW</tt> statement defines a screw joint connecting two links of the system (see figure 3-13).

### Format ###
> <tt>SCREW</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>SCREW</tt> (BOLT, NUT) = THRD
defines a screw joint named _THRD_ connecting two links named _BOLT_ and _NUT_.

### Notes ###
  1. Each screw joint in the system must be defined by a separate <tt>SCREW</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear and must be directed along the joint axis; both must have the same positive sense. The local u and u' axes must be chosen such that, at one position of the joint, they are collinear and the two local origins coincide (see figure).
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. The joint variable for a joint is the distance from the positive local u axis to the positive local u' axis. It has units of length and is considered positive when in the same direction as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variable (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the travel of the joint variable.
  1. The lead of the screw thread of each <tt>SCREW</tt> joint must be defined by a subsequent <tt>DATA SCREW</tt> statement. Notice that the sign of the lead distinguishes a right-hand from a left-hand thread.


## The <tt>CAM</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_14.png' height='400px' />
_Figure 3-14:_ Example of a cam and follower joint connecting two links.
The <tt>CAM</tt> statement defines a cam and follower joint between two links of the system (see figure 3-14).

### Format ###
> <tt>CAM</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>CAM</tt> (DISK, ROLR) = CURV
defines a <tt>CAM</tt> joint named _CURV_ connecting a cam shaped link named _DISK_ with a follower link named _ROLR_.

### Notes ###
  1. Each cam and follower joint in the system must be defined by a separate <tt>CAM</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. The first _link name_ referenced must be that with the cam profile and the second _link name_ refers to the follower link the order is not arbitrary and cannot be reversed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must both lie normal to the plane of the pitch curve and both must be positively directed on the same side of this plane. The local u,v and u',v' axes must all lie in this same plane; the (u,v,w) local origin may be located arbitrarily on the first _link name_ but the (u',v',w') local origin must be located on the pitch curve. The line directed from the origin of (u,v,w) to the origin of (u',v',w') is defined as positive t (see figure).
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. A <tt>CAM</tt> joint has two internal degrees of freedom. The first joint variable is the angle from the positive local u axis to positive t; it has units of degrees and is considered positive when counterclockwise as seen from the positive local w axis. The second joint variable is the angle from positive t to the positive local u' axis; it has units of degrees and is considered positive when counterclockwise as seen from the positive local w' axis.
  1. It is assumed there are no limits on the rotation of either joint variable.
  1. The shape of the pitch curve (see figure) must be defined by a subsequent <tt>DATA CAM</tt> statement.


## The <tt>SLOT</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_15.png' height='400px' />
_Figure 3-15:_ Example of a pin-in-slot joint between two links.
The <tt>SLOT</tt> statement defines a pin-in-slot joint between two links of the system (see figure 3-15).

### Format ###
> <tt>SLOT</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.
### Example ###
> <tt>SLOT</tt> (PLAT, BAR) = CURV
defines a <tt>SLOT</tt> joint named _CURV_ connecting a profile slotted link named _PLAT_ with a follower link named _BAR_.

### Notes ###
  1. Each slot joint in the system must be defined by a separate <tt>SLOT</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. The first _link name_ referenced must be that containing the slot profile and the second _link name_ refers to the follower link; the order is not arbitrary and cannot be reversed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must both lie normal to the plane of the profiled slot and both must be positively directed on the same side of the plane. The local u,v and u',v' axes must all lie in this same plane the (u,v,w) local origin may be located arbitrarily on the first _link name_, but the (u',v',w') local origin must be located on the centerline of the profiled slot (see figure).
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. A <tt>SLOT</tt> joint has two internal degrees of freedom. The first joint variable is the u projection of the distance from the first local coordinate origin to the second local coordinate origin it has units of length and is considered positive if in the same direction as the positive local u axis. The second joint variable is the angle from a line paralleling the positive local u axis to the positive local u' axis it has units of degrees and considered positive when counterclockwise as seen from the positive local w' axis.
  1. It is assumed there are no limits on the travel of either joint variable (see notes for the <tt>DATA SLOT</tt> statement).
  1. The shape of the profiled slot in the first _link name_ must be defined by a subsequent <tt>DATA SLOT</tt> statement.


## The <tt>CYLINDER</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_16.png' height='400px' />
_Figure 3-16:_ Example of a cylindric joint connecting two links.
The <tt>CYLINDER</tt> statement defines a cylindric joint (allowing turning and sliding motions about and along a common axis) connecting two links of the system (see figure 3-16).

### Format ###
> <tt>CYLINDER</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>CYLINDER</tt> (LK1, LK2) = CYL
defines a cylindric joint named _CYL_ connecting two links named _LK1_ and _LK2_.

### Notes ###
  1. Each cylindric joint in the system must be defined by a separate <tt>CYLINDER</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it) a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>CYLINDER</tt> _joint name_ (see figure) and defined by a subsequent <tt>DATA CYLINDER</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear and must be directed along the axis of relative motion of the joint. Both local w axes must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA CYLINDER</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. Each <tt>CYLINDER</tt> joint has two internal degrees of freedom. The first joint variable is the angle from the positive local u axis to the positive local u' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w,w' axes. The second joint variable is the distance from the local u axis to the local u' axis measured along the common local w,w' axes it has units of length and is considered positive when the relative displacement is in the same sense as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the travel of either joint variable.


## The <tt>UJOINT</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_17.png' height='400px' />
_Figure 3-17:_ Example of a universal joint connecting two links.
The <tt>UJOINT</tt> statement defines a Hooke universal joint connecting two links of the system (see figure 3-17).

### Format ###
> <tt>UJOINT</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>UJOINT</tt> (SHFT, ROD) = UJNT
defines a Hooke universal joint named _UJNT_ connecting two links named _SHFT_ and _ROD_.

### Notes ###
  1. Each universal joint in the system must be defined by a separate <tt>UJOINT</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it) a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>UJOINT</tt> _joint name_ (see figure) and defined by a subsequent <tt>DATA UJOINT</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident; the local w and w' axes must coincide with the two pin axes on the cross of the universal joint and they must be mutually perpendicular. The common perpendicular to the local w and w' axes is defined as t and is positive in the direction specified by the right hand rule applied from positive w to positive w' (see figure).
  1. If an appropriate <tt>DATA UJOINT</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. A <tt>UJOINT</tt> joint has two internal degrees of freedom. The first joint variable is the angle from the positive local u axis to positive t it has units of degrees and is considered positive when counterclockwise as seen from positive w. The second joint variable is the angle from positive t to the positive local u' axis it also has units of degrees and is considered positive when counterclockwise as seen from the positive w' axis.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the rotation of either of the joint variables.


## The <tt>FLAT</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_18.png' height='400px' />
_Figure 3-18:_ Example of a flat joint connecting two links.
The <tt>FLAT</tt> statement defines a flat joint (two flat surfaces constrained to remain in contact but free to turn and slide in the plane) connecting two links of the system (see figure 3-18).

### Format ###
> <tt>FLAT</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>FLAT</tt> (BASE, PAD) = PLATE
defines a <tt>FLAT</tt> joint named _PLATE_ connecting two links named _BASE_ and _PAD_.

### Notes ###
  1. Each flat joint in the system must be defined by a separate <tt>FLAT</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>FLAT</tt> _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The u,v and u',v' planes must be chosen coplanar and parallel to the mating surfaces of the joint the local w and w' axes must be parallel and must be directed to the same side of the mating surfaces (see figure).
  1. Care should be taken in choosing the two local coordinate systems to insure that, as the joint moves, the origins of the two local coordinate systems never become coincident. If these origins do become coincident the first and third joint variables become redundant (see note 8 below, and see figure); numeric difficulties may be encountered at or very near to such a position.
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. <tt>A FLAT</tt> joint has three internal degrees of freedom. The common perpendicular between the local w and w' axes is designated as t. The first joint variable is the angle from the positive local u axis to positive t; it has units of degrees and is considered positive when counterclockwise as seen from positive local w. The second joint variable is the distance from w to w' measured along t; it has units of length and is considered positive when measured in the same sense as positive t. The third joint variable is the angle from positive t to positive local u'; it has units of degrees and is considered positive when counterclockwise as seen from the positive local w' axis (see figure).
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 8 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there are no limits on the travel of any of the joint variables.


## The <tt>PLANE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_19.png' height='400px' />
_Figure 3-19:_ Example of a planar joint connecting two links.
The <tt>PLANE</tt> statement defines a planar joint (two flat surfaces constrained to remain in contact but free to turn and slide in the plane) connecting two links of the system (see figure 3-19).

### Format ###
> <tt>PLANE</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>PLANE</tt> (BASE, PAD) = PLATE
defines a planar joint named _PLATE_ connecting two links named _BASE_ and _PAD_.

### Notes ###
  1. Each planar joint in the system must be defined by a separate <tt>PLANE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>PLANE</tt> _joint name_ (see figure), and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The u,v and u',v' planes must be chosen coplanar and parallel to the mating surfaces of the joint; the local w and w' axes must be parallel and must be directed to the same side of the mating surfaces (see figure).
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. <tt>A PLANE</tt> joint has three internal degrees of freedom. The first and second joint variables are the u and v components, respectively, of the location of the (u',v',w') origin with respect to the (u,v,w) axes. These have units of length and are considered positive according to the sense of the u and v axes. The third joint variable is the angle from a line parallel to the positive local u axis to the positive local u' axis it has units of degrees and is considered positive when counterclockwise as seen from the positive local w' axis (see figure).
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there are no limits on the travel of any of the joint variables.


## The <tt>SPHERE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_20.png' height='400px' />
_Figure 3-20:_ Example of a ball and socket joint connecting two links.
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_21.png' height='400px' />
_Figure 3-21:_ Kinematically equivalent model of a ball and socket joint connecting two links.
The <tt>SPHERE</tt> statement defines a ball and socket joint connecting two links of the system (see figure 3-20, 3-21).

### Format ###
> <tt>SPHERE</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>SPHERE</tt> (BALL, SCKT) = SPHR
defines a spheric joint named _SPHR_ connecting two links named _BALL_ and _SCKT_.

### Notes ###
  1. Each spheric joint in the system must be defined by a separate <tt>SPHERE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>SPHERE</tt> _joint name_ (see figure), and defined by a subsequent <tt>DATA SPHERE</tt> statement or by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident with the center of the spheric joint. Care should be taken in choosing the coordinate systems such that, as the joint moves, the local u and w' axes never become collinear. If these axes do become collinear, the first and third joint variables become redundant (see Note 8 below, and see figure). Numeric difficulties may be encountered at or very near to such a position.
  1. If an appropriate <tt>DATA SPHERE</tt> statement or <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. A spheric joint has three internal degrees of freedom. The three joint variables are the three Eulerian angles describing the relative orientation of the local coordinate systems (see figure). All three joint variables have units of degrees and are considered positive when counterclockwise as seen from the positive ends of the local u axis, the line of nodes, and the local w' axis, respectively.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there are no limits on the rotations of any of the joint variables.


## The <tt>OPEN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_22.png' height='400px' />
_Figure 3-22:_ Example of a logical association between two links without physical constraints.
The <tt>OPEN</tt> statement defines a logical association between two links of the system without producing any physical constraints (see figure 3-22).

### Format ###
> <tt>OPEN</tt> (link name, link name) = joint name
where each _link name_ refers to the alphanumeric name given to one of the two associated links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> <tt>OPEN</tt> (BASE, BALL) = FREE
defines a logical association named _FREE_ between two links named _BASE_ and _BALL_.

### Notes ###
  1. An <tt>OPEN</tt> statement is never required, but may be useful to form an association between two links of the system such that, for example, some of the variables can be driven with a prescribed motion while others remain free.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>OPEN</tt> _joint name_ (see figure) and defined by two subsequent <tt>DATA LINK</tt> statements. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. Care should be taken in choosing the coordinate systems such that, as the joint moves, the local u and w' axes never become parallel. If these axes do become parallel the fourth and sixth joint variables become redundant (see note 7 below, and see figure). Numeric difficulties may be encountered at or very near to such a position.
  1. If an appropriate <tt>DATA LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. An <tt>OPEN</tt> joint has six internal degrees of freedom. The first three joint variables are the u, v, and w components of the location (translation) of the u',v',w' local origin with respect to the u,v,w axes, respectively. These three variables have units of length and are considered positive according to the senses of the positive local u, v, and w axes. The final three joint variables are the three Eulerian angles describing the relative orientation of the local These three angles are coordinate systems (see figure). defined identically to those of the <tt>SPHERE</tt> statement.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 7 above), and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there are no limits on the travel of any of the joint variables.


## The <tt>POINT</tt> Statement ##
The <tt>POINT</tt> statement defines one or more points of interest attached to one link of the system model. This statement can also be used to define lines to be drawn by the <tt>DRAW</tt> statement.

### Format ###
> <tt>POINT</tt> (link name) = point name, point name, point name, ...
where _link name_ is the alphanumeric name of the link to which the points are attached and each _point name_ is an arbitrarily selected alphanumeric name for one of the points being defined. If more than one _point name_ is listed, the order of the _point names_ also defines a series of straight line segments to be drawn by subsequent <tt>DRAW</tt> statements.

; Examples
: <tt>POINT</tt> (LEVR) = PT1
: <tt>POINT</tt> (BASE) = A, B, P, PT2, Q
These two statements define a point named _PT1_ attached to a link named _LEVR_, and five points named _A_, _B_, _P_, _PT2_, and _Q_ attached to another link named _BASE_. If a <tt>DRAW</tt> statement is issued, the above statements cause no lines to be drawn for link _LEVR_; however, the link named _BASE_ will be drawn as a series of straight line segments from _A_ to _B_ to _P_ to _PT2_ to _Q_.

### Notes ###
  1. Each point to be referenced by its _point name_ in an IMP model must be defined by a <tt>POINT</tt> statement.
  1. It is necessary to define _point names_ for the attachment points of every spring or damper, for the points of application of every force, and to define the direction of every force or torque. Also, it is often useful to define _point names_ so that their motions can be printed, so that their locations can be used in supplying data, or to control the visible outline of a link when using the <tt>DRAW</tt> statement.
  1. A maximum of 33 _point names_ may be defined in a single <tt>POINT</tt> statement (with continuation lines). There is no restriction, however, on defining additional _point names_ attached to the same _link name_ with one or more additional <tt>POINT</tt> statements.
  1. The same _point name_ may be used more than once, either in the same or in different <tt>POINT</tt> statements. This is often useful when defining a closed figure for the <tt>DRAW</tt> statement. If the same _point name_ is defined on more than one link, the first occurrence of that _point name_ is treated as primary and used for the attachment point of a spring, for example, if requested.
  1. Each different _point name_ must be given a location on the _link name_ by a subsequent <tt>DATA POINT</tt> statement. If this is not done before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, those _point names_ with missing data are placed coincident with the global origin; no message is printed.
  1. _Point names_ attached to different _link names_ may not be defined in the same <tt>POINT</tt> statement.
  1. There is no restriction against attaching one or more _point names_ to the stationary _link name_.
  1. The _link name_ referred to in a <tt>POINT</tt> statement must have appeared in at least one previous <tt>SHAPE</tt> statement or a statement defining a joint. If not, the <tt>POINT</tt> statement is ignored and a message is printed.
  1. The vertices of a link shape defined by a filename in a <tt>SHAPE</tt> statement have no associated _point name_ and cannot be referenced as points. An additional coincident point may be defined for this purpose, however, by a <tt>POINT</tt> statement.

## The <tt>SPRING</tt> Statement ##
The <tt>SPRING</tt> statement defines a spring connecting two points of the system.

### Format ###
> <tt>SPRING</tt> (point name, point name) = spring name
where each _point name_ is the alphanumeric name of one of the two points to which the ends of the spring are attached, and _spring name_ is an arbitrarily selected alphanumeric name assigned to the spring.

### Example ###
> <tt>SPRING</tt> (PT1, PT2) = PULL
defines a spring named _PULL_ connected between two points named _PT1_ and _PT2_.

### Notes ###
  1. Each spring not acting within a joint (see <tt>DATA SPRING</tt> statement) must be defined by a separate <tt>SPRING</tt> statement.
  1. Defining a spring as acting within a joint (see <tt>DATA SPRING</tt> statement) is preferable to use of the <tt>SPRING</tt> statement when possible; the numerical accuracy is better and efficiency is much improved.
  1. No two springs may be defined having the same _spring name_. An attempt to do so results in the deletion of the previously defined spring with the same _spring name_ (and associated data) and causes a message to be printed.
  1. The two _point names_ used may not be identical; if identical _point names_ are used the <tt>SPRING</tt> statement is ignored and a message is printed.
  1. The two _point names_ used must have been defined by previous <tt>POINT</tt> statements. If not, the <tt>SPRING</tt> statement is ignored and a message is printed.
  1. Each spring defined by a <tt>SPRING</tt> statement must be further characterized by a subsequent <tt>DATA SPRING</tt> statement. If a <tt>DATA SPRING</tt> statement does not appear for each _spring name_ before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given then any _spring name_ with missing data is deleted at that time; a message is printed.
  1. Care should be taken to insure that, as the system moves, the two end points of the spring are never located at the same position since, in such a case, the direction of the spring force becomes undefined. If this does occur during the simulation, the effect of that spring is ignored for that position; a message is printed.


## The <tt>DAMPER</tt> Statement ##
The <tt>DAMPER</tt> statement defines a viscous damper (dashpot) connecting two points of the system.

### Format ###
> <tt>DAMPER</tt> (point name, point name) = damper name
where each _point name_ is the alphanumeric name of one of the two points to which the ends of the damper are attached and _damper name_ is an arbitrarily selected alphanumeric name assigned to the damper.

### Example ###
> <tt>DAMPER</tt> (PT1, PT2) = SLOW
defines a viscous damper named _SLOW_ connected between two points named _PT1_ and _PT2_.

### Notes ###
  1. Each damper not acting within a joint (see <tt>DATA DAMPER</tt> statement) must be defined by a separate <tt>DAMPER</tt> statement.
  1. Defining a damper as acting within a joint (see <tt>DATA DAMPER</tt> statement) is preferable to use of the <tt>DAMPER</tt> statement when possible; the numerical accuracy is better and efficiency is much improved.
  1. No two viscous dampers may be defined having the same _damper name_. An attempt to do so results in the deletion of the previously defined damper with the same _damper name_ (and associated data), and causes a message to be printed.
  1. The two _point names_ used may not be identical; if identical _point names_ are used the <tt>DAMPER</tt> statement is ignored and a message is printed.
  1. The two _point names_ used must have been defined by previous <tt>POINT</tt> statements; if not, the <tt>DAMPER</tt> statement is ignored and a message is printed.
  1. Each damper defined by a <tt>DAMPER</tt> statement must be further characterized by a subsequent <tt>DATA DAMPER</tt> statement. If a <tt>DATA DAMPER</tt> statement does not appear for each _damper name_ before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, then any _damper name_ with missing data is deleted at that time; a message is printed.
  1. Care should be taken to insure that, as the system moves, the two end points of the damper are never located at the same position since, in such a case, the direction of the damper's force becomes undefined. If this does occur during the simulation, the effect of that damper is ignored for that position; a message is printed.


## The <tt>FORCE</tt> Statement ##
The <tt>FORCE</tt> statement defines an externally applied force acting at a defined point on one link of the system. The direction of the force is defined by two points giving its line of action.

### Format ###
> <tt>FORCE</tt> (point name / point name, point name) = force name
where the first _point name_ is the alphanumeric name of the point of application of the force and also implicitly defines the link to which the force is applied; the second and third _point names_ are the alphanumeric names of two points which define the line of action of the force; the _force name_ is an arbitrarily selected alphanumeric name assigned to the force.

### Example ###
> <tt>FORCE</tt> (PT1 / PT2, PT3) = PUSH
defines a force named _PUSH_ applied at point _PT1_ and acting along a line parallel to the line from _PT2_ to _PT3_.

### Notes ###
  1. Each externally applied force not acting within a joint (see <tt>DATA FORCE</tt> statement) must be defined by a separate <tt>FORCE</tt> statement.
  1. Defining a force as acting within a joint (see <tt>DATA FORCE</tt> statement) is preferable to use of the <tt>FORCE</tt> statement, when possible; the numerical accuracy is better and efficiency is much improved.
  1. No two forces may be defined having the same _force name_. An attempt to do so results in the deletion of the previously defined force with the same _force name_ (and associated data) and causes a message to be printed.
  1. The second and third _point names_ used may not be identical. If identical _point names_ are used the statement is ignored and a message is printed.
  1. There is no restriction against the first and second or first and third _point names_ used being identical; this may often be desirable.
  1. The three _point names_ used must have been defined by previous <tt>POINT</tt> statements. If not, the <tt>FORCE</tt> statement is ignored and a message is printed.
  1. Each externally applied force defined by a <tt>FORCE</tt> statement must be further characterized by a subsequent <tt>DATA FORCE</tt> statement. If a <tt>DATA FORCE</tt> statement does not appear for each _force name_ before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given then any _force name_ with missing data is deleted at that time; a message is printed.
  1. The second and third _point names_ serve only to define a line parallel to the force, a direction for the force's line of action. These _point names_ may be attached to any link(s) of the system including the stationary link.
  1. Care should be taken to insure that, as the system moves, the second and third _point names_ used are never located at the same position since, in such a case, the direction of the applied force becomes undefined. If this does occur during the simulation, the effect of that _force name_ is ignored for that position; a message is printed.
  1. The force is considered positive when directed from the second _point name_ toward the third _point name_ specified in the <tt>FORCE</tt> statement.
  1. The reaction force for each _force name_ is assumed to be applied to the fixed link of the system unless explicitly defined by another <tt>FORCE</tt> statement.


## The <tt>TORQUE</tt> Statement ##
The <tt>TORQUE</tt> statement defines an externally applied torque acting on one link of the system. The direction of the torque is also defined by specifying two points which determine the direction of its axis.

### Format ###
> <tt>TORQUE</tt> (link name / point name, point name) = torque name
where _link name_ is the alphanumeric name of the link to which the torque is applied; the _point names_ are the alphanumeric names of each of two points which define a line parallel to the axis of the torque; the _torque name_ is an arbitrarily selected alphanumeric name assigned to the torque.

### Example ###
> <tt>TORQUE</tt> (LEVR / PT1, PT2) = TURN
defines a torque named _TURN_ acting on a link named _LEVR_; its axis is parallel to the line connecting points named _PT1_ and _PT2_.

### Notes ###
  1. Each externally applied torque not acting within a joint (see <tt>DATA FORCE</tt> statement) must be defined by a separate <tt>TORQUE</tt> statement.
  1. Defining a torque as acting within a joint (see <tt>DATA FORCE</tt> and <tt>DATA TORQUE</tt> statements) is preferable to use of the <tt>TORQUE</tt> statement, when possible; the numerical accuracy is better and efficiency is much improved.
  1. No two torques may be defined having the same _torque name_. An attempt to do so results in the deletion of the previously defined torque with the same _torque name_ (and associated data), and causes a message to be printed.
  1. The two _point names_ used may not be identical. If identical _point names_ are used, the statement is ignored and a message is printed.
  1. The _link name_ used must have been defined in at least one previous statement defining a joint; if not, the <tt>TORQUE</tt> statement is ignored and a message is printed.
  1. The two _point names_ used must have been defined by previous <tt>POINT</tt> statements; if not, the <tt>TORQUE</tt> statement is ignored and a message is printed.
  1. Each externally applied torque defined by a <tt>TORQUE</tt> statement must be further characterized by a subsequent <tt>DATA TORQUE</tt> statement. If a <tt>DATA TORQUE</tt> statement does not appear for each _torque name_ before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, then any _torque name_ with missing data is deleted at that time; a message is printed.
  1. Either or both of the two _point names_ used may be attached _link name_ to which the torque is applied, but this to the is not necessary. Either or both may be attached to any link of the system, including the stationary link.
  1. Care should be taken that, as the system moves, the two _point names_ used are never located at the same position since, in such a case, the direction of the axis of the torque becomes undefined. If this does occur during the simulation, the effect of that _torque name_ is ignored for that position; a message is printed.
  1. The torque is considered positive when acting counterclockwise (right-hand rule) about the axis directed from the first _point name_ toward the second _point name_ specified.
  1. The reaction torque for each _torque name_ is assumed applied to the fixed link of the system unless explicitly defined by another <tt>TORQUE</tt> statement.