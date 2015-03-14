# Introduction #

The rack joint is a spinning gear attached to a sliding plane.



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
  1. A <tt>RACK</tt> joint has one internal degree of freedom. The joint variable for a <tt>RACK</tt> joint is the distance from the v axis along positive t to the local v' origin. It has units of length and is considered positive when in the positive u direction.
  1. It is assumed that there is no limit on the travel of the joint variable.
  1. The pitch circle radius of the pinion must be defined by a subsequent <tt>DATA::RACK</tt> statement.
  1. The simulation of a <tt>RACK</tt> joint is treated as though the pinion is a cylinder rolling without slip against a smooth plane for the rack. This causes no problem in motion analysis; however, in force analysis, the pinion is treated as having zero pressure angle.


## The <tt>DATA::RACK</tt> Statement ##
The <tt>DATA::RACK</tt> statement specifies the pinion radius for a <tt>RACK</tt> joint.

### Format ###
> DATA::RACK (joint name) = radius; x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where each _joint name_ is the alphanumeric name of the <tt>RACK</tt> joint and _radius_ is the pitch
circle radius of the second link named in the <tt>RACK</tt> statement, x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> is the center of the wheel, x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> is the point on the u axis of the wheel, x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub> is the point on the w axis of the wheel.

### Example ###
> DATA::RACK (MESH) = 2.5; 0,0,0; 1,0,0; 0,1,0
specifies that the pitch circle radius of the pinion in a <tt>RACK</tt> joint named <tt>MESH</tt> is 2.5 length
units.  The center of the wheel of the rack joint is at the global origin, the rack will move in the direction of the global x axis, and the w axis of the joint is in the global y direction.

### Notes ###
  1. There must be a <tt>DATA::RACK</tt> statement for each joint defined by a <tt>RACK</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
  1. The _joint name_ specified must have been defined by a previous <tt>RACK</tt> statement. If not, the <tt>DATA::RACK</tt> statement is ignored and a message is printed.
  1. If more than one <tt>DATA::RACK</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
  1. The value of _radius_ has units of length. It should be equal to the perpendicular distance from the local <i>u</i>,<i>v</i>,<i>w</i> origin to the local u axis (see figure with the <tt>RACK</tt> statement).
  1. The value of _radius_ may not be zero. If zero is specified for _radius_, the <tt>DATA::RACK</tt> statement is ignored and a message is printed.