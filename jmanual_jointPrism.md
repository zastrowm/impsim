## The <tt>PRISM</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_9.2.png' height='400px' />

_Figure 3-9:_ Example of a sliding joint connecting two links.  The <tt>PRISM</tt> statement defines a sliding joint connecting two links of the system (see figure 3-9).

### Format ###
> <tt>PRISM</tt> Joint Name Link Name Link Name Point1 Point2 Point3;

> or

> <tt>PRISM</tt> Joint Name Link Name Link Name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>;

where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name> is an arbitrarily chosen alphanumeric name assigned to the joint.  The_x<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are
numeric values for the global coordinates of the three points defining the initial locations of the
two local coordinate systems.  The first point defines the common origins of the two local coordinate systems.  The second point must be located on the common local positive_w_,_<i>w</i> axes.  The third point must lie in the half-plane defined by the common local _w_,<i>w</i>
> axes and the common local positive _u_,<i>u</i> axes.

### Example ###
> <tt>PRISM</tt> PPin LK1 LK2 0,6.5,4 2,6.8,4  2,6.5,7;
defines a sliding joint named _PPin_ connecting two links named _LK1_ and _LK2_.  This also specifies the initial locations of the local coordinate systems attached to the two links on either side of the joint named PPin.  The numeric data
corresponds approximately to the figure.

### Notes ###

  1. Each prismatic joint in the system must be defined by a separate <tt>PRISM</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in an exception being thrown.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes an exception to be thrown.
  1. The joint variable for a <tt>PRISM</tt> joint is the distance from the positive local u axis to the positive local u' axis. It has units of length and is considered positive when in the same direction as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives (see Note 4 above) and also the signs of the constraint force and torque components within the joint (see, for example, the <tt>PRINT FORCE</tt> statement).
  1. Two local coordinate systems must be chosen for each _joint name_ (see figure), and defined in the <tt>PRISM</tt> statement. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear and must both be directed parallel to the relative motion of the joint. Both local w axes must have the same positive sense, and the local u and u' axes must be parallel and must have the same positive sense (see figure).
  1. It is assumed that there is no limit on the magnitude of the joint variable (sliding motion of the joint).
  1. The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>PRISM</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.
  1. The angle formed by points _2_,_1_,_3_ need not be a right angle. IMP uses the first point to locate the common local origins extending vectors from there toward the second point; it forms the common local _w_,<i>w</i> axes. The common local positive _u_,<i>u</i> axes are taken in the half-plane defined by the common local _w_,<i>w</i> axes and the third point; a right angle is then formed for the common local _u_,<i>u</i> axes in the half-plane even though they may not pass through the third point.
  1. If the _x_<sub>3</sub>_,_y<sub>3</sub>_,_z<sub>3</sub>_numeric data are not given for the third point, the coordinates of the global origin are used. In view of note 11) above, this does not produce an error unless the common local_w_,_<i>w</i> axes pass through the global origin. This may be a convenient shortcut (see final example above) if the user is not concerned about the particular placement of the local _u_ and <i>u</i> axes.
