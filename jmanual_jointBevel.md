# Introduction #

Bevel gears are two gears whose teeth are at an angle to the gear itself instead of jutting out from it.


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
  1. A <tt>BEVEL</tt> joint has one internal degree of freedom. The joint variable for a <tt>BEVEL</tt> joint is the angle from the positive local u axis to the positive local w' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w axis.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variable (see Note 7 above), and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the rotation of the joint variable.
  1. The gear ratio and pitch circle radius of each <tt>BEVEL</tt> joint must be defined by a subsequent <tt>DATA::BEVEL</tt> statement.
  1. The simulation of a <tt>BEVEL</tt> joint is treated as though the two pitch cones are rolling against each other with no slip. This causes no problem in motion analysis; however, in force analysis, the bevel gears are treated as having zero presure angle.



## The <tt>DATA::BEVEL</tt> Statement ##
The <tt>DATA::BEVEL</tt> statement specifies the gear ratio and the size of the two bevel gears defined by a
previous <tt>BEVEL</tt> statement.

### Format ###
> DATA::BEVEL (joint name) = ratio, radius; x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where each _joint name_ is the alphanumeric name of the <tt>BEVEL</tt> joint, _ratio_ is the numeric
value of the gear ratio for the joint, and _radius_ is the pitch circle radius of the second link
named in the <tt>BEVEL</tt> statement, x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> is the point defining the center of the first bevel gear, this can be used along with the ratio and the radius to determine the center of the second bevel gear x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> is the point defining the w axis of the first bevel gear, x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub> is the point defining the u axis of the first gear which is parallel to the w axis of the second gear.

### Example ###
> DATA::BEVEL (BVL) = 2.625, 2.0; 0,0,0; 0,0,1; 1,0,0

specifies that the gear ratio of a <tt>BEVEL</tt> joint named <tt>BVL</tt> is 84/32 = 2.625 and that the back-face
pitch circle radii of the two bevel gears are 5.25 and 2.0 length units, respectively.  The first bevel gear is located at the global origin, the axis of rotation of the first bevel gear is along the global z axis, and the u axis, which is parallel to the axis of rotation of the second gear is located along the global x axis.

### Notes ###
  1. There must be a <tt>DATA::BEVEL</tt> statement for each joint defined by a <tt>BEVEL</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
  1. The _joint name_ specified must have been defined by a previous <tt>BEVEL</tt> statement. If not, the <tt>DATA::BEVEL</tt> statement is ignored and a message is printed.
  1. If more than one <tt>DATA::BEVEL</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
  1. The value of _ratio_ is dimensionless; the value of _radius_ has units of length.
  1. The value of _ratio_ is the ratio of the number of teeth of the first bevel gear named in the <tt>BEVEL</tt> statement to the number of teeth of the second.
  1. The value of _ratio_ must be a positive number. A zero or negative value for _ratio_ causes the <tt>DATA::BEVEL</tt> statement to be ignored and a message to be printed.
  1. The angle between the two intersecting shafts of a <tt>BEVEL</tt> joint is always 90 ° . The two local coordinate systems defined by the two <tt>DATA::LINK</tt> statements are assumed to be at consistent distances from the intersection of the two shafts, that is, the u,v and u’,v’ planes are both chosen to go through the point of contact of the respective pitch circles (see figure with <tt>BEVEL</tt> statement). The _radius_ specified is the pitch circle radius of the second gear named, measured in the u,v plane. It should equal the distance from the shaft intersection to the u,v plane.