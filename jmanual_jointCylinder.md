# Introduction #

Cylinder joints are combinations of Revolute joints and Prism joints.  That means they can spin around an axis and slide up and down that axis.


## The <tt>CYLINDER</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch3_16.2.png' height='400px' />
_Figure 3-16:_ Example of a cylindric joint connecting two links.
The <tt>CYLINDER</tt> statement defines a cylindric joint (allowing turning and sliding motions about and along a common axis)connecting two links of the system (see figure 3-16).

### Format ###
> <tt>CYLINDER</tt> Joint Name Link Name Link Name Point1 Point2 Point3;
> or
> > <tt>CYLINDER</tt> Joint Name Link Name Link Name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub> x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub> x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>;

where each _link name_ refers to the alphanumeric name given to one of the two connected links and _joint name_ is an arbitrarily chosen alphanumeric name assigned to the joint.

### Example ###

> <tt>CLYINDER</tt> CYL LK1 LK2 0.0,1.0,2.0 1.0,1.0,2.0 0.0,2.0,2.0;

defines a cylindric joint named CYL connecting two links named LK1 and LK2.

### Notes ###
  1. Each cylindric joint in the system must be defined by a separate <tt>CYLINDER</tt> statement.
  1. The same _link name_ may appear in more than one statement defining a joint.
  1. Each statement defining a joint must refer to two distinct _link names_. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. Two local coordinate systems must be chosen for each <tt>CYLINDER</tt> _joint name_ (see figure) and defined in the <tt>CYLINDER</tt> statement. One local coordinate system (u,v,w) is rigidly attached to the first _link name_, while the other (u',v',w') is rigidly attached to the second _link name_. The local w and w' axes must be collinear and must be directed along the axis of relative motion of the joint. Both local w axes must have the same positive sense (see figure).
  1. Each <tt>CYLINDER</tt> joint has two internal degrees of freedom. The first joint variable is the angle from the positive local u axis to the positive local u' axis. It has units of degrees and is considered positive when counterclockwise as seen from the positive local w,w' axes. The second joint variable is the distance from the local u axis to the local u' axis measured along the common local w,w' axes it has units of length and is considered positive when the relative displacement is in the same sense as the positive local w,w' axes.
  1. The order in which the two _link names_ appear is arbitrary. This choice, however, does affect the designation of the joint variables (see Note 7 above) and also the signs of the constraint force and torque components within the joint (see the <tt>PRINT FORCE</tt> statement).
  1. It is assumed that there is no limit on the travel of either joint variable.
  1. The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>CYLINDER</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.
  1. The angle formed by points _2_,_1_,_3_ need not be a right angle. IMP uses the first point to locate the two coincident local origins; extending a vector toward the second point, it then forms the common local _w_ and <i>w</i> axes. The common local positive _u_ and <i>u</i> axes are then taken in the half-plane defined by the common local _w_ and <i>w</i> axes and the third point; a right angle is formed for the common local _u_ and <i>u</i> axes in this half-plane even though they may not exactly pass through the third point.