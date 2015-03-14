# Introduction #
The bodies of a screw joint rotate and traverse a common axis, just as those of a cylinder joint. With a screw joint, however, the rotation and slide movements are linked to each other by the lead angle. This means that as the distance between the bodies changes, the angle also changes by a specified amount calculated from the slide distance and the lead.

# The <tt>SCREW</tt> Statement #
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
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined by a subsequent <tt>DATA::SCREW</tt> statement. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear and must be directed along the joint axis; both must have the same positive sense. The local u and u' axes must be chosen such that, at one position of the joint, they are collinear and the two local origins coincide (see figure).
  1. If an appropriate <tt>DATA::SCREW</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate system(s) is (are) coincident with the link coordinate system; no message is printed.
  1. The joint variable for a joint is the distance from the positive local u axis to the positive local u' axis. It has units of length and is considered positive when in the same direction as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variable (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the travel of the joint variable.
  1. The lead of the screw thread of each <tt>SCREW</tt> joint must be defined by a subsequent <tt>DATA::SCREW</tt> statement. Notice that the sign of the lead distinguishes a right-hand from a left-hand thread.




## The <tt>DATA::SCREW</tt> Statement ##
The <tt>DATA::SCREW</tt> statement specifies the lead of a screw joint, the location of the joint, and the location of the two local coordinate systems.

### Format ###
> DATA::SCREW (joint name) = value; x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>SCREW</tt> joint, _value_ is the numeric
value of the lead of the <tt>SCREW</tt> joint thread, and the x,y,z coordinates define three points which are used to define the two local coordinate systems.

### Example ###
> DATA::SCREW (THRD) = -0.750; -1.0,1.0,0.0; -1.0,4.0,0.0; 0.0,1.0,-0.5

specifies the lead as 0.750 length units per revolution with a
left-hand thread and specifies the initial locations of the coordinate systems attached to the two links for a <tt>SCREW</tt> joint named <tt>THRD</tt>.

### Notes ###
  1. There must be a <tt>DATA::SCREW</tt> statement for each joint defined by a <tt>SCREW</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
  1. The _joint name_ specified must have been defined by a previous <tt>SCREW</tt> statement. If not, the <tt>DATA::SCREW</tt> statement is ignored and a message is printed.
  1. If more than one <tt>DATA::SCREW</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
  1. The coordinate systems of the bodies are defined such that the distance and angle between the bodies are initially zero.
  1. The dimensions of _value_ are length units of advance of the screw per revolution. A right-hand thread has a positive _value_ and a left-hand thread has a negative _value_.
  1. The _value_ of the lead may not be zero. A <tt>REVOLUTE</tt> statement should be used instead of a <tt>SCREW</tt> for this case. If zero is specified for _value_, the <tt>DATA::SCREW</tt> statement is ignored and a message is printed.