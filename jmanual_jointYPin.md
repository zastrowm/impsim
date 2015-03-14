# YPin #
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_3.png' height='400px' />

## The <tt>YPIN</tt> Statement ##
The <tt>YPIN</tt> statement defines a pinned joint connecting two links of the system (see figure 3-5), with
its pin axis initially parallel to the global Y axis.

### Format ###
> YPIN Joint Name Link Name Link Name Point 1 Point 2 Point 3
or
> YPIN Joint Name Link Name Link Name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>;

where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###
> YPIN PINY LinkA LinkB 3,2,0 1,0,0 3,4,0;
defines a pinned joint named _PINY_ connecting two links named _LinkA_ and _LinkB_.

### Notes ###
  1. Each Y-oriented pin joint in the system must be defined by a separate <tt>YPIN</tt> statement.
  1. No other joint of any type may be defined having the same _joint name_. An attempt to do so results in the deletion of the previously defined joint of the same _joint name_ (and all information dependent on it); a warning message is printed.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Local coordinate systems must be chosen for each _joint name_ (see figure). One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The origins of the two local coordinate systems must be coincident, the local v and v' axes must be collinear and initially parallel to the global Y axis and must be directed along the joint axis, and both local v axes must have the same positive sense (see figure).
  1. If an appropriate <tt>DATA::YPIN</tt> statement or <tt>DATA::LINK</tt> statement is not defined before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered, it is assumed that the corresponding local coordinate systems(s) is (are) coincident with the link coordinate system; no message is printed.
  1. The joint variable for a <tt>YPIN</tt> joint is the angle from the positive local w axis to the positive local w' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local v,v' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the sign of the joint variable and its derivatives.
  1. It is assumed that there is no limit on the magnitude of the joint variable (rotation of the joint).
  1. The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>YPIN</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a_<tt>YPIN</tt> joint.
  1. The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however (except, perhaps, for the second and third points); larger distances achieve more accurate placement of axes.
  1. The angles formed by points _2_,_1_,_3_ need not lie in a plane perpendicular to the global Y axis. IMP uses the first point to locate the common local origins and the common local _v_,<i>v</i> axes; the local _w_ and <i>w</i> axes are then taken in the half-planes defined by the common local _v_,<i>v</i> axes and the second and third points, respectively. Right angles are formed for the local _w_ and <i>w</i> axes in these half-planes even though they may not pass precisely through the second and third points, respectively.