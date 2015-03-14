## The <tt>REVOLUTE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_5.2.png' height='400px' />

_Figure 3-5:_ Example of a pin joint connecting two links.
The <tt>REVOLUTE</tt> statement defines a pin joint connecting two links of the system.  This statement also specifies the numeric data which simultaneously locate the two local
coordinate systems attached to the two links on either side of a <tt>REVOLUTE</tt> joint relative to the
absolute (global) frame of reference for the system.

The first point must lie at the common origins of the two
local coordinate systems and the second point must lie on the common local positive _w_,<i>w</i>
axes. The third and fourth points must lie on the local positive _u_ and <i>u</i> axes of the
coordinate systems attached to the first and second links named in the <tt>REVOLUTE</tt> statement,
respectively.


### Format ###
> <tt>REVOLUTE</tt> Joint Name link name link name Point 1 Point 2 Point 3 Point 4;
or
> <tt>REVOLUTE</tt> Joint Name link name link name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub> x<sub>4</sub>,y<sub>4</sub>,z<sub>4</sub>;
where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.  The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are
numeric values for the global coordinates of the four points defining the initial locations of the
two local coordinate systems._

### Example ###
> <tt>REVOLUTE</tt> PIN LK1 LK2 4.1,2.7,0 5.0,2.7,0 8.1,13.2,0;
defines a pinned joint named _PIN_ connecting two links named _LK1_ and _LK2_.  This also specifies the initial locations of the local coordinate systems attached to the two links on either
side of the joint named PIN. The numeric data corresponds approximately to the figure.


### Notes ###
  1. Each revolute joint in the system must be defined by a separate <tt>REVOLUTE</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each <tt>REVOLUTE</tt> statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure). One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident the local w and w' axes must be collinear and must be directed along the joint axis and both local w axes must have the same positive sense (see figure).
  1. The joint variable for a <tt>REVOLUTE</tt> joint is the angle from the positive local u axis to the positive local u' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the magnitude of the joint variable (rotation of the joint).
  1. The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. The four points for which_x<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however (except, perhaps, for the third and fourth points); larger distances achieve more accurate placement of axes.
  1. The angles formed by points _2_,_1_,_3_ and by points _2_,_1_,_4_ need not be right angles. IMP uses the first and second points to locate the common local origins and the common local _w_,<i>w</i> axes; the local _u_ and <i>u</i> axes are then taken in the half-planes defined by the common local _w_,<i>w</i> axes and the third and fourth points, respectively. Right angles are formed for the local _u_ and <i>u</i> axes in these half-planes even though they may not pass through the third and fourth points, respectively.