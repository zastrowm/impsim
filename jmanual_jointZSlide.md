## The <tt>ZSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_9.png' height='400px' />

_Figure 4-7:_ The <tt>ZSLIDE</tt> statement defines a joint that slides along the Z axis connecting two links in the system.

The <tt>ZSLIDE</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of an <tt>YSLIDE</tt> joint relative to the absolute (global) frame of
reference for the system.  The slideing axis is initially aligned parrallel to the global Z axis.

### Format ###
> ZSLIDE Joint Name Link Name Link Name Point1;

> or

> ZSLIDE Joint Name Link Name Link Name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>;

where _joint name_ is the alphanumeric name of the <tt>ZSLIDE</tt> joint connecting the two links to which the local coordinate systems are
attached.   The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_are numeric values for the global coordinates of the point defining the initial location
of the origin of the two local coordinate systems._

### Examples ###
> ZSLIDE zpinslide LK1 LK2 -5.0,1.0,0;

specifies the initial locations of the coordinate systems attached to the two links on either side of a <tt>ZSLIDE</tt> joint named <tt>zpinslide</tt>.
The numeric data corresponds approximately to the figure.

### Notes ###
  1. The dimensions for the _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_numeric data in a_<tt>ZSLIDE</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. Each ZSlide statement defining a joint must refer to two distinct link names. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. The joint name specified must have been defined in the ZSLIDE statement.  If not, the ZSLIDE statement is ignored and a message is printed.
