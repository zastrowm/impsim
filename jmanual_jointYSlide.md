## The <tt>YSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_8.png' height='400px' />

_Figure 4-7:_ The <tt>YSLIDE</tt> statement defines a joint that slides along the Y axis connecting two links in the system.

The <tt>YSLIDE</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of an <tt>YSLIDE</tt> joint relative to the absolute (global) frame of
reference for the system.  The slideing axis is initially aligned parrallel to the global Y axis.

### Format ###
> YSLIDE Joint Name Link Name Link Name Point1;

> or

> YSLIDE Joint Name Link Name Link Name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>;

where _joint name_ is the alphanumeric name of the <tt>YSLIDE</tt> joint connecting the two links to which the local coordinate systems are
attached.   The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_are numeric values for the global coordinates of the point defining the initial location
of the origin of the two local coordinate systems._

### Examples ###
> YSLIDE ypinslide LK1 LK2 -5.0,1.0,0;

specifies the initial locations of the coordinate systems attached to the two links on either side of a <tt>YSLIDE</tt> joint named <tt>ypinslide</tt>.
The numeric data corresponds approximately to the figure.

### Notes ###
  1. The dimensions for the _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_numeric data in a_<tt>YSLIDE</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. Each YSlide statement defining a joint must refer to two distinct link names. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. The joint name specified must have been defined in the YSLIDE statement.  If not, the YSLIDE statement is ignored and a message is printed.