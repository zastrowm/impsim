## The <tt>XSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_7.png' height='400px' />

_Figure 4-7:_ The <tt>XSLIDE</tt> statement defines a joint that slides along the X axis connecting two links in the system.

The <tt>XSLIDE</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of an <tt>XSLIDE</tt> joint relative to the absolute (global) frame of
reference for the system.  The sliding axis is initially aligned parallel to the global X axis.

### Format ###
> XSLIDE Joint Name Link Name Link Name Point1;

> or

> XSLIDE Joint Name Link Name Link Name x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>;

where _joint name_ is the alphanumeric name of the <tt>XSLIDE</tt> joint connecting the two links to which the local coordinate systems are
attached.   The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_are numeric values for the global coordinates of the point defining the initial location
of the origin of the two local coordinate systems._

### Examples ###
> XSLIDE xpinslide LK1 LK2 -5.0,1.0,0;

specifies the initial locations of the coordinate systems attached to the two links on either side of a <tt>XSLIDE</tt> joint named <tt>xpinslide</tt>.
The numeric data corresponds approximately to the figure.

### Notes ###
  1. The dimensions for the _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_numeric data in a_<tt>XSLIDE</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. Each XSlide statement defining a joint must refer to two distinct link names. An attempt to join a link to itself causes the statement to be ignored and a message to be printed.
  1. The joint name specified must have been defined in the XSLIDE statement. If not, the XSLIDE statement is ignored and a message is printed.
