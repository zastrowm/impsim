# Introduction #

A gear joint is when the connection between the two bodies is in the form of interlocking gears.


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
  1. A <tt>GEAR</tt> joint has one internal degree of freedom. The joint variable for a <tt>GEAR</tt> joint is the angle from the positive local u axis to positive t. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w axis.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variable (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the rotation of the joint variable.
  1. The gear ratio of each <tt>GEAR</tt> joint must be defined by a subsequent <tt>DATA::GEAR</tt> statement.
  1. The simulation of the <tt>GEAR</tt> joint is treated as though they are two cylinders rolling against each other with no slip. This causes no problem in motion analysis; however, in force analysis, the gears are treated as having zero pressure angle.


## The <tt>DATA::GEAR</tt> Statement ##
The <tt>DATA::GEAR</tt> statement specifies the gear ratio and the center to
center distance for a <tt>GEAR</tt> joint.

### Format ###
> DATA::GEAR (joint name) = ratio, distance; x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>GEAR</tt> joint, _ratio_ is the numeric value of
the gear ratio for the joint, and _distance_ is the numeric value of the center to center distance
(the sum of the pitch radii) for the two mating <tt>GEAR</tt> sectors,
x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> represent the point defining the center of the first gear,
x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> represents the common u axis of the two gears, which can be used along with the distance to determine the center of the second gear,
x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub> represents a point along the w axis of the first gear which is parallel to the w' axis.

### Example ###
> DATA::GEAR (SPUR) = 2.625, 6.25; 0,0,0; 1,0,0; 0,0,1

specifies that the gear ratio of a spur gear joint named <tt>SPUR</tt> is 84:32 = 2.625, and that the sum
of the pitch radii of the mating gear sectors is 4.526 + 1.724 = 6.25 length units.  This first gear is located at the global origin, and the second is located along the global x axis, with the w axes of both gears in the z direction.

### Notes ###
  1. There must be a <tt>DATA::GEAR</tt> statement for each joint defined by a <tt>GEAR</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
  1. The _joint name_ specified must have been defined by a previous <tt>GEAR</tt> statement. If not, the <tt>DATA::GEAR</tt> statement is ignored and a message is printed.
  1. If more than one <tt>DATA::GEAR</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
  1. The value of _ratio_ is dimensionless; the value of _distance_ has units of length.
  1. The value of _ratio_ is the ratio of the number of teeth (or the pitch diameter) of the first gear named in the <tt>GEAR</tt> statement to the number of teeth (or pitch diameter) of the second gear named. A positive value of _ratio_ indicates that both are external gears, while a negative _ratio_ indicates an internal-external gear combination.
  1. A value of zero may not be used for _ratio_ to represent a gear-rack combination. A zero value for _ratio_ causes the <tt>DATA::GEAR</tt> statement to be ignored and a message to be printed.