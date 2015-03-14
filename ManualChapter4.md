# Chapter 4: Data Statements #
The definition statements of the previous chapter are used to define the components of the system
and the relationships between the various components. Before the system can be analyzed, however, it
is necessary to supply the numeric data appropriate to each of the entities defined. This is the
purpose of the <tt>DATA</tt> statements presented in this chapter.

Each of the <tt>DATA</tt> statements begins with the keyword <tt>DATA</tt> followed by a separator. The second
word of each <tt>DATA</tt> statement is also treated as a keyword, instructing the IMP system to interpret
the remainder of the statement according to one of the following formats:


## The <tt>DATA LINK</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_1.png' height='400px' />
_Figure 4-1:_
The <tt>DATA LINK</tt> statement specifies the numeric data which locate one of the coordinate systems
attached to one of the links relative to the absolute (global) frame of reference for the system.

The <tt>DATA LINK</tt> statements, taken together with the <tt>DATA</tt> statements for the various joint types
(<tt>DATA SPHERE</tt> statements, etc.), describe the relative locations of the various links and joints
of the system at the initial (design) position.

The initial location of one local coordinate system, attached to one of the links is defined by each
<tt>DATA LINK</tt> statement by specifying the global coordinates of three points (see figure). The first
point must lie at the origin of the local coordinate system; the second point must be chosen on the
local positive _w_ or _z_ axis; the third point should lie on the positive _u_ or _x_ axis
of the local _u_,_v_,_w_ coordinate system attached to the joint element or the local
_x_,_y_,_z_ coordinate system attached to the link.

### Format ###
There are two forms of the <tt>DATA LINK</tt> statement.

The first form is used to specify the location of one local coordinate system attached to an element
of a joint. The format is

> DATA LINK(link name,joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _link name_ and _joint name_ are the alphanumeric names of the link and joint to which
this local coordinate system is attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric
values for the global coordinates of the three points defining the initial location of a local
(_u_,_v_,_w_) joint element coordinate system._

The second form is identical to the first except the _joint name_ is replaced by the keyword
<tt>LINK</tt>. This format is:

> DATA LINK (link name, LINK) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

which indicates that the primary local coordinate system for the _link name_ is being located.

### Examples ###
> DATA LINK (BAR,PIN) = -1.0,2.5,0.0; -1.0,3.5,0.0; -2.0,2.5,1.0

specifies the location of a joint named _PIN_ at one end of a link named _BAR_. The numeric data
corresponds approximately to the figure.

The above example might also take any of the following forms:

> DATA LINK (BAR, PIN) = -1,2.5,0; -1,3.5,0; -2,2.5,1

> DATA LINK (BAR, PIN) = -1,2.5, ; -1,3.5, ; -2,2.5,1

> DATA LINK (BAR, PIN) = PT1; PT2; -2,2.5,1

### Notes ###
  1. When a _link name_ is first defined in the system model (whether by a <tt>LINK</tt> statement or by a joint definition statement) a local coordinate system for the link is formed in the system memory. This link coordinate system is initially located coincident with the global coordinate system, but may be moved to another location by the <tt>LINK</tt> form of the <tt>DATA LINK</tt> statement.
  1. When a _joint name_ is first defined by a joint definition statement, two local joint coordinate systems are formed in the system memory, one attached to each of the two _link names_ joined by the joint. These are initially placed coincident with the local coordinate systems of the two _link names_, but each may be moved to some other location on the link by the _joint name_ form of the <tt>DATA LINK</tt> statement.
  1. If the _joint name_ form is used, both _link name_ and _joint name_ must have been used in the same previous statement defining that joint. If not, the <tt>DATA LINK</tt> statement is ignored and a message is printed.
  1. When the _joint name_ form is used, global coordinate data are given by the user for the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups. However, this is converted in memory to a (_u_,_v_,_w_) or (_<i>u</i>,<i>v</i>,<i>w</i>) location for that _joint name_ element with respect to the specified _link name_. This data is then considered fixed; if the link is moved, the joint elements move in unison with it.
  1. When the <tt>LINK</tt> form is used, the local coordinate system of the link is moved to another location as specified by the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_data. Any data referenced to the link coordinate system (such as the locations of local joint coordinate systems, any points attached to the link, any geometric shape data from a_<tt>SHAPE</tt> statement, etc.) all move if the local link coordinate system is moved by the <tt>LINK</tt> form of a <tt>DATA LINK</tt> statement.
  1. If more than one <tt>DATA LINK</tt> statement is given for the same _link name_, the later statement takes precedence and earlier data are replaced. No message is printed.
  1. Notice that notes 1) through 6) above make the order in which related <tt>DATA LINK</tt> statements are given very important; related <tt>DATA LINK</tt> statements might not produce the same result if given in different orders.
  1. The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA LINK</tt> statement are length units measured in the global coordinate system.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data must correspond to the rules for the placement of the local joint coordinate systems (refer to the statement defining each particular type of joint). If errors are detected, the corresponding_<tt>DATA LINK</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.
  1. The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local coordinate axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.
  1. The angle formed by points_2_,_1_,_3_need not be a right angle. IMP uses the first point to locate the local origin and uses the second point to define the direction of the local w or z axis; the local_u_or_x_axis is then taken in the half-plane defined by the local_w_or_z_axis and the third point. Any necessary adjustments are made to the third point to produce a local coordinate system with exact right angles.
  1. If the_x<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are not given for the third point, the coordinates of the global origin are used. This may be a convenient shortcut if the user is not concerned about the particular placement of the local u or x axis. In view of notes 11) and 12) above, this does not produce an error unless the local w or z axis passes through the global origin.
  1. Any of the_x<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above example).

## The <tt>DATA XPIN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_3.png' height='400px' />
_Figure 4-3:_
The <tt>DATA XPIN</tt> statement specifies the numeric data which simultaneously locate the two local
coordinate systems attached to the two links on either side of an <tt>XPIN</tt> joint relative to the
absolute (global) frame of reference for the system. The pin axis is initially aligned parallel to
the global X axis.

The <tt>DATA XPIN</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints and
the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system at
the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by an
<tt>XPIN</tt> statement are both defined by a single <tt>DATA XPIN</tt> statement by specifying the global
coordinates of three points (see figure). The first point must lie at the common origins of the two
local coordinate systems. The second and third points are optional but, if given, should lie on the
local positive _v_ and <i>v</i> axes of the coordinate systems attached to the first and second
links named in the <tt>XPIN</tt> statement, respectively.

### Format ###
> DATA XPIN (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>XPIN</tt> joint connecting the two links to which
the local _u_,_v_,_w_ and <i>u</i>,<i>v</i>,<i>w</i> coordinate systems are attached. The
_x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric values for the global coordinates of the three
points defining the initial locations of the two local coordinate systems._

### Examples ###
> DATA XPIN (PIN) = -2.0,2.5,0.0; -2.0,3.5,0.0; -2.0,2.5,1.0

specifies the initial locations of the local coordinate systems attached to the two links on either
side of an <tt>XPIN</tt> joint named _PIN_. The numeric data corresponds approximately to the figure. The
above example might also take any of the following forms:

> DATA XPIN (PIN) = -2,2.5,0; -2,3.5,0; -2,2.5,1

> DATA XPIN (PIN) = -2,2.5, ; -2,3.5, ; -2,2.5,1

> DATA XPIN (PIN) = PT1; -2,3.5,0; -2,2.5,1

> DATA XPIN (PIN) = PT1

### Notes ###
  1. The _joint name_ specified must have been defined by a previous <tt>XPIN</tt> statement. If not, the <tt>DATA XPIN</tt> statement is ignored and a message is printed.
  1. If a <tt>DATA XPIN</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by an <tt>XPIN</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
  1. If more than one <tt>DATA XPIN</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.
  1. The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA XPIN</tt> statement are length units.
  1. Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
  1. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for an_<tt>XPIN</tt> joint (see <tt>XPIN</tt> statement). If errors are detected, the <tt>DATA XPIN</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.
  1. The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however (except, perhaps, for the second and third points); larger distances achieve more accurate placement of axes.
  1. The angles formed by points _2_,_1_,_3_ need not lie in a plane perpendicular to the global X axis. IMP uses the first point to locate the common local origins and the common local _u_,<i>u</i> axes; the local _v_ and <i>v</i> axes are then taken in the half-planes defined by the common local _u_,<i>u</i> axes and the second and third points, respectively. Right angles are formed for the local _v_ and <i>v</i> axes in these half-planes even though they may not pass precisely through the second and third points, respectively.
  1. If the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are not given for the second and/or third points, the local coordinate systems are placed parallel to those of the global system. This may be a convenient shortcut (see final example above), if the user is not concerned about the particular placement of the two local_v_and/or_<i>v</i> axes.
  1. Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).


## The <tt>DATA YPIN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_4.png' height='400px' />
_Figure 4-4:_
The <tt>DATA YPIN</tt> statement specifies the numeric data which simultaneously locate the two local
_u_,_v_,_w_ and <i>u</i>,<i>v</i>,<i>w</i> coordinate systems attached to the two links on either
side of a <tt>YPIN</tt> joint relative to the absolute (global) frame of reference for the system. The pin
axis is initially aligned parallel to the global Y axis.

The <tt>DATA YPIN</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints and
the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system at
the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>YPIN</tt> statement are both defined by a single <tt>DATA YPIN</tt> statement by specifying the global
coordinates of three points (see figure). The first point must lie at the common origins of the two
local _u_,_v_,_w_ and <i>u</i>,<i>v</i>,<i>w</i> coordinate systems. The second and third points are
optional but, if given, must lie on the local positive _w_ and <i>w</i> axes of the coordinate
systems attached to the first and second links named in the <tt>YPIN</tt> statement, respectively.

### Format ###
> DATA YPIN (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>YPIN</tt> joint connecting the two links to which
the local _u_,_v_,_w_ and <i>u</i>,<i>v</i>,<i>w</i> coordinate systems are attached. The
_x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric values for the global coordinates of the three
points defining the initial locations of the two local coordinate systems._

### Examples ###
> DATA YPIN (PIN) = -2.0,2.5,0.0; 0.0,2.5,0.5; -3.0,2.5,1.0

specifies the initial locations of the local coordinate systems attached to the two links on either
side of a <tt>YPIN</tt> joint named PIN. The numeric data corresponds approximately to the figure. The
above example might also take any of the following forms:

> DATA YPIN (PIN) = -2,2.5,0; 0,2.5,.5; -3,2.5,1

> DATA YPIN (PIN) = -2,2.5, ; ,2.5,.5; -3,2.5,1

> DATA YPIN (PIN) = PT1; ,2.5,.5; -3,2.5,1

> DATA YPIN (PIN) = PT1

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>YPIN</tt> statement. If not, the <tt>DATA YPIN</tt> statement is ignored and a message is printed.

# If a <tt>DATA YPIN</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>YPIN</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA YPIN</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.

# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA YPIN</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a_<tt>YPIN</tt> joint (see <tt>YPIN</tt> statement). If errors are detected, the <tt>DATA YPIN</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.

# The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however (except, perhaps, for the second and third points); larger distances achieve more accurate placement of axes.

# The angles formed by points _2_,_1_,_3_ need not lie in a plane perpendicular to the global Y axis. IMP uses the first point to locate the common local origins and the common local _v_,<i>v</i> axes; the local _w_ and <i>w</i> axes are then taken in the half-planes defined by the common local _v_,<i>v</i> axes and the second and third points, respectively. Right angles are formed for the local _w_ and <i>w</i> axes in these half-planes even though they may not pass precisely through the second and third points, respectively.

# If the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are not given for the second and/or third points, the local coordinate systems are placed parallel to those of the global system. This may be a convenient shortcut (see final example above), if the user is not concerned about the particular placement of the local_w_and_<i>w</i> axes.

# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).

## The <tt>DATA ZPIN</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_5.png' height='400px' />
_Figure 4-5:_
The <tt>DATA ZPIN</tt> statement specifies the numeric data which simultaneously locate the two local
coordinate systems attached to the two links on either side of a <tt>ZPIN</tt> joint relative to the
absolute (global) frame of reference for the system. The pin axis is initially aligned parallel to
the global Z axis.

The <tt>DATA ZPIN</tt> statement, taken together with the <tt>DATA</tt> statements for other types of joints and
the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system at
the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>ZPIN</tt> statement are both defined by a single <tt>DATA ZPIN</tt> statement by specifying the global
coordinates of three points (see figure). The first point must lie at the common origins of the two
local coordinate systems. The second and third points must lie on the local positive _u_ and
<i>u</i> axes of the coordinate systems attached to the first and second links named in the <tt>ZPIN</tt>
statement.

### Format ###
> DATA ZPIN (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>ZPIN</tt> joint connecting the two links to which
the local coordinate systems are attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric
values for the global coordinates of the three points defining the initial locations of the two
local coordinate systems._

### Examples ###
> DATA ZPIN (PIN) = -2.0,2.5,0.0; -2.0,3.5,0.0; 0.0,2.5,0.5

specifies the initial locations of the local coordinate systems attached to the two links on either
side of a <tt>ZPIN</tt> joint named PIN. The numeric data corresponds approximately to the figure. The
above example might also take any of the following forms:

> DATA ZPIN (PIN) = -2,2.5,0; -2,3.5,0; 0,2.5,.5

> DATA ZPIN (PIN) = -2,2.5, ; -2,3.5, ; ,2.5,.5

> DATA ZPIN (PIN) = PT1; PT2; 0,2.5,.5

> DATA ZPIN (PIN) = PT1

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>ZPIN</tt> statement. If not, the <tt>DATA ZPIN</tt> statement is ignored and a message is printed.

# If a <tt>DATA ZPIN</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>ZPIN</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA ZPIN</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.

# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA ZPIN</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a_<tt>ZPIN</tt> joint (see <tt>ZPIN</tt> statement). If errors are detected, the <tt>DATA ZPIN</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.

# The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however (except, perhaps, for the second and third points); larger distances achieve more accurate placement of axes.

# The angles formed by points _2_,_1_,_3_ need not lie in a plane perpendicular to the global _Z_ axis. IMP uses the first point to locate the common local origins and the common local _w_,<i>w</i> axes; the local _u_ and <i>u</i> axes are then taken in the half-planes defined by the common local _w_,<i>w</i> axes and the second and third points, respectively. Right angles are formed for the local _u_ and <i>u</i> axes in these half-planes even though they may not pass precisely through the second and third points, respectively.

# If the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are not given for the second and/or third points, the local coordinate systems are placed parallel to those of the global system. This may be a convenient shortcut (see final example above), if the user is not concerned about the particular placement of the two local_u_and_<i>u</i> axes.

# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).

## The <tt>DATA REVOLUTE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_6.png' height='400px' />
_Figure 4-6:_
The <tt>DATA REVOLUTE</tt> statement specifies the numeric data which simultaneously locate the two local
coordinate systems attached to the two links on either side of a <tt>REVOLUTE</tt> joint relative to the
absolute (global) frame of reference for the system.

The <tt>DATA REVOLUTE</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints
and the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system
at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>REVOLUTE</tt> statement are both defined by a single <tt>DATA REVOLUTE</tt> statement by specifying the global
coordinates of four points (see figure). The first point must lie at the common origins of the two
local coordinate systems and the second point must lie on the common local positive _w_,<i>w</i>
axes. The third and fourth points must lie on the local positive _u_ and <i>u</i> axes of the
coordinate systems attached to the first and second links named in the <tt>REVOLUTE</tt> statement,
respectively.

### Format ###
> DATA REVOLUTE (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>; x<sub>4</sub>,y<sub>4</sub>,z<sub>4</sub>

where _joint name_ is the alphanumeric name of the <tt>REVOLUTE</tt> joint connecting the two links to
which the local coordinate systems are attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are
numeric values for the global coordinates of the four points defining the initial locations of the
two local coordinate systems._

### Examples ###
> DATA REVOLUTE (PIN) = -2.0,2.5,0.0; -2.0,3.5,0.0; $
> > 0.0,2.5,0.5; -3.0,2.5,1.0

specifies the initial locations of the local coordinate systems attached to the two links on either
side of a <tt>REVOLUTE</tt> joint named PIN. The numeric data corresponds approximately to the figure. The
above example might also take any of the following forms:


> DATA REVOLUTE (PIN) = -2,2.5,0; -2,3.5,0; 0,2.5,.5; -3,2.5,1

> DATA REVOLUTE (PIN) = -2,2.5, ; -2,3.5, ; ,2.5,.5; -3,2.5,1

> DATA REVOLUTE (PIN) = PT1; PT2; 0,2.5,.5; -3,2.5,1

> DATA REVOLUTE (PIN) = PT1; PT2

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>REVOLUTE</tt> statement. If not the <tt>DATA REVOLUTE</tt> statement is ignored and a message is printed.

# If a <tt>DATA REVOLUTE</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>REVOLUTE</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA REVOLUTE</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.

# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA REVOLUTE</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a revolute joint (see_<tt>REVOLUTE</tt> statement). If errors are detected, the <tt>DATA REVOLUTE</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.

# The four points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however (except, perhaps, for the third and fourth points); larger distances achieve more accurate placement of axes.

# The angles formed by points _2_,_1_,_3_ and by points _2_,_1_,_4_ need not be right angles. IMP uses the first and second points to locate the common local origins and the common local _w_,<i>w</i> axes; the local _u_ and <i>u</i> axes are then taken in the half-planes defined by the common local _w_,<i>w</i> axes and the third and fourth points, respectively. Right angles are formed for the local _u_ and <i>u</i> axes in these half-planes even though they may not pass through the third and fourth points, respectively.

# If the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are not given for the third and/or fourth points, the coordinates of the global origin are used. In view of note 8) above, this does not produce an error unless the pin axis passes through the global origin. This may be a convenient shortcut (see final example above), if the user is not concerned about the particular placement of the local_u_and_<i>u</i> axes.

# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).

## The <tt>DATA XSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_7.png' height='400px' />
_Figure 4-7:_
The <tt>DATA XSLIDE</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of an <tt>XSLIDE</tt> joint relative to the
absolute (global) frame of reference for the system. The sliding axis is initially aligned parallel
to the global X axis.

The <tt>DATA XSLIDE</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints
and the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system
at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by an
<tt>XSLIDE</tt> statement are coincident and are both defined by a single <tt>DATA XSLIDE</tt> statement by
specifying the global coordinates of one point (see figure). The point defines the common origins of
the two local coordinate systems. The local coordinate axes attached to the two links are set
parallel to the global axes.

### Format ###
> DATA XSLIDE (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>

where _joint name_ is the alphanumeric name of the <tt>XSLIDE</tt> joint connecting the two links to
which the local coordinate systems are attached. The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_are numeric values for
the global coordinates of the point defining the initial location of the origin of the two local
coordinate systems._

### Examples ###
> DATA XSLIDE (SLIP) = -1.0,1.0,1.0

specifies the initial locations of the coordinate systems attached to the two links on either side
of a <tt>XSLIDE</tt> joint named <tt>SLIP</tt>. The numeric data corresponds approximately to the figure.

The above example might also take any of the following forms:

> DATA XSLIDE (SLIP) = -1,1,0

> DATA XSLIDE (SLIP) = -1,1

> DATA XSLIDE (SLIP) = PT1

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>XSLIDE</tt> statement. If not, the <tt>DATA XSLIDE</tt> statement is ignored and a message is printed.

# If a <tt>DATA XSLIDE</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by an <tt>XSLIDE</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA XSLIDE</tt> statement is given for the same _joint name_ the later statement takes precedence and earlier data are replaced.

# The dimensions for the _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_numeric data in a_<tt>DATA XSLIDE</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_group of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see last example above).

## The <tt>DATA YSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_8.png' height='400px' />
_Figure 4-8:_
The <tt>DATA YSLIDE</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of a <tt>YSLIDE</tt> joint relative to the
absolute (global) frame of reference for the system. The sliding axis is initially aligned parallel
to the global Y axis.

The <tt>DATA YSLIDE</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints
and the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system
at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>YSLIDE</tt> statement are coincident and are both defined by a single <tt>DATA YSLIDE</tt> statement by
specifying the global coordinates of one point (see figure). The point defines the common origins of
the two local coordinate systems. The local coordinate axes attached to the two links are set
parallel to the global axes.

### Format ###
> DATA YSLIDE (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>

where _joint name_ is the alphanumeric name of the <tt>YSLIDE</tt> joint connecting the two links to
which the local coordinate systems are attached. The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_are numeric values for
the global coordinates of the point defining the initial location of the origin of the two local
coordinate systems._

### Examples ###
> DATA YSLIDE (SLIP) = -1.0,1.0,1.0

specifies the initial locations of the coordinate systems attached to the two links on either side
of a <tt>YSLIDE</tt> joint named <tt>SLIP</tt>. The numeric data corresponds approximately to the figure.

The above example might also take any of the following forms:

> DATA YSLIDE (SLIP) = -1,1,0

> DATA YSLIDE (SLIP) = -1,1

> DATA YSLIDE (SLIP) = PT1

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>YSLIDE</tt> statement. If not, the <tt>DATA YSLIDE</tt> statement is ignored and a message is printed.

# If a <tt>DATA YSLIDE</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>YSLIDE</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA YSLIDE</tt> statement is given for the same _joint name_ the later statement takes precedence and earlier data are replaced.

# The dimensions for the _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_numeric data in a_<tt>DATA YSLIDE</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_group of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see last example above).

## The <tt>DATA ZSLIDE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_9.png' height='400px' />
_Figure 4-9:_
The <tt>DATA ZSLIDE</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of a <tt>ZSLIDE</tt> joint relative to the
absolute (global) frame of reference for the system. The sliding axis is aligned parallel to the
global Z axis.

The <tt>DATA ZSLIDE</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints
and the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system
at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>ZSLIDE</tt> statement are coincident and are both defined by a single <tt>DATA ZSLIDE</tt> statement by
specifying the global coordinates of one point (see figure). The point defines the common origins of
the two local coordinate systems. The local coordinate axes attached to the two links are set
parallel to the global axes.

### Format ###
> DATA ZSLIDE (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>

where _joint name_ is the alphanumeric name of the <tt>ZSLIDE</tt> joint connecting the two links to
which the local coordinate systems are attached. The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_are numeric values for
the global coordinates of the point defining the initial location of the origin of the two local
coordinate systems._

### Examples ###
> DATA ZSLIDE (SLIP) = -1.0,1.0,1.0

specifies the initial locations of the coordinate systems attached to the two links on either side
of a <tt>ZSLIDE</tt> joint named <tt>SLIP</tt>. The numeric data corresponds approximately to the figure.

The above example might also take any of the following forms:
> DATA ZSLIDE (SLIP) = -1,1,0

> DATA ZSLIDE (SLIP) = -1,1

> DATA ZSLIDE (SLIP) = PT1

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>ZSLIDE</tt> statement. If not, the <tt>DATA ZSLIDE</tt> statement is ignored and a message is printed.

# If a <tt>DATA ZSLIDE</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>ZSLIDE</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA ZSLIDE</tt> statement is given for the same _joint name_ the later statement takes precedence and earlier data are replaced.

# The dimensions for the _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_numeric data in a_<tt>DATA ZSLIDE</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>_group of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has been previously given (see last example above).

## The <tt>DATA PRISM</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_10.png' height='400px' />
_Figure 4-10:_
The <tt>DATA PRISM</tt> statement specifies the numeric data which simultaneously locates the two local
coordinate systems attached to the two links on either side of a prismatic joint relative to the
absolute (global) frame of reference for the system.

The <tt>DATA PRISM</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints and
the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system at
the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>PRISM</tt> statement are coincident and are both defined by a single <tt>DATA PRISM</tt> statement by
specifying the global coordinates of three points (see figure). The first point defines the common
origins of the two local coordinate systems. The second point must be located on the common local
positive _w_,<i>w</i> axes. The third point must lie in the half-plane defined by the common local
_w_,<i>w</i> axes and the common local positive _u_,<i>u</i> axes.

### Format ###
> DATA PRISM (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>PRISM</tt> joint connecting the two links to which
the local coordinate systems are attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric
values for the global coordinates of the three points defining the initial locations of the two
local coordinate systems._

### Examples ###
> DATA PRISM (SLIP)= -1.0,1.0,0.0; -1.0,4.0,0.0; 0.0,1.0,-0.5

specifies the initial locations of the coordinate systems attached to the two links on either side
of a <tt>PRISM</tt> joint named <tt>SLIP</tt>. The numeric data correspond approximately to the figure.

The above example might also take any of the following forms:
> DATA PRISM (SLIP) = -1,1,0; -1,4,0; 0,1,-.5

> DATA PRISM (SLIP) = -1,1, ; -1,4, ; ,1,-.5

> DATA PRISM (SLIP) = PT1; PT2; 0,1,-.5

> DATA PRISM (SLIP) = PT1; PT2

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>PRISM</tt> statement. If not, the <tt>DATA PRISM</tt> statement is ignored and a message is printed.

# If a <tt>DATA PRISM</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>PRISM</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA PRISM</tt> statement is given for the same _joint name_ the later statement takes precedence and earlier data are replaced.

# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA PRISM</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a_<tt>PRISM</tt> joint (see <tt>PRISM</tt> statement). If errors are detected, the <tt>DATA PRISM</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.

# The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.

# The angle formed by points _2_,_1_,_3_ need not be a right angle. IMP uses the first point to locate the common local origins extending vectors from there toward the second point; it forms the common local _w_,<i>w</i> axes. The common local positive _u_,<i>u</i> axes are taken in the half-plane defined by the common local _w_,<i>w</i> axes and the third point; a right angle is then formed for the common local _u_,<i>u</i> axes in the half-plane even though they may not pass through the third point.

# If the _x_<sub>3</sub>_,_y<sub>3</sub>_,_z<sub>3</sub>_numeric data are not given for the third point, the coordinates of the global origin are used. In view of note 8) above, this does not produce an error unless the common local_w_,_<i>w</i> axes pass through the global origin. This may be a convenient shortcut (see final example above) if the user is not concerned about the particular placement of the local _u_ and <i>u</i> axes.

# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see last example above).

## The <tt>DATA CYLINDER</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_11.png' height='400px' />
_Figure 4-11:_
The <tt>DATA CYLINDER</tt> statement specifies the numeric data which simultaneously locates the two local coordinate systems attachedto the two links on either side of a <tt>CYLINDER</tt> joint relative tothe absolute (global) frame of reference for the system.

The <tt>DATA CYLINDER</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints and the <tt>DATA LINK</tt> statements,describe the relative locations of the various links of the systemat the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a <tt>CYLINDER</tt> statement are coincident and are both defined by a single <tt>DATA CYLINDER</tt> statement by specifying the global coordinates of three points (see figure). The first point must lie at the common origin of the two localcoordinate systems. The second point must be located on the common local positive _w_,<i>w</i> axes. The third point must lie in the half-plane defined by the common local _w_,<i>w</i> axes and the common local positive _u_,<i>u</i> axes.

### Format ###
> DATA CYLINDER (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>CYLINDER</tt> joint connecting the two links to
which the local coordinate systems are attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are
numeric values for the global coordinates of the three points defining the initial locations of
the two local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> coordinate systems.

### Examples ###
> DATA CYLINDER(CYL)=-1.0,1.0,0.0;-1.0,4.0,0.0;0.0,1.0,-0.5

specifies the initial locations of the two coincident _u_,_v_,_w_ and <i>u</i>,<i>v</i>,<i>w</i>
coordinate systems attached to the two links on either side of a <tt>CYLINDER</tt> joint named CYL. The
numeric data corresponds approximately to the figure.

The above example might also take any of the following forms:
> DATA CYLINDER (CYL) = -1,1,0; -1,4,0; 0,1,-.5

> DATA CYLINDER (CYL) = -1,1, ; -1,4, ; ,1,-.5

> DATA CYLINDER (CYL) = PT1; PT2; 0,1,-.5

> DATA CYLINDER (CYL) = PT1; PT2

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>CYLINDER</tt> statement. If not, the <tt>DATA CYLINDER</tt> statement is ignored and a message is printed.

# If a <tt>DATA CYLINDER</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>CYLINDER</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA CYLINDER</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.

# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA CYLINDER</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a_<tt>CYLINDER</tt> joint (see <tt>CYLINDER</tt> statement). If errors are detected, the <tt>DATA CYLINDER</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.

# The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.

# The angle formed by points _2_,_1_,_3_ need not be a right angle. IMP uses the first point to locate the two coincident local origins; extending a vector toward the second point, it then forms the common local _w_ and <i>w</i> axes. The common local positive _u_ and <i>u</i> axes are then taken in the half-plane defined by the common local _w_ and <i>w</i> axes and the third point; a right angle is formed for the common local _u_ and <i>u</i> axes in this half-plane even though they may not exactly pass through the third point.

# If the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are not given for the third point, the coordinates of the global origin are used. In view of note 8) above, this does not produce an error unless the common local_w_,_<i>w</i> axes pass through the global origin. This may be a convenient shortcut (see final example above) if the user is not concerned about the particular placement of the local _u_ and <i>u</i> axes.

# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).


## The <tt>DATA RIGID</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_2.png' height='400px' />
_Figure 4-2:_
The <tt>DATA RIGID</tt> statement simultaneously specifies the numeric data which locate the two local
coordinate systems attached to the two links on either side of a <tt>RIGID</tt> joint relative to the
absolute (global) frame of reference for the system.

The <tt>DATA RIGID</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints and
the <tt>DATA LINK</tt> statements, describe the relative locations of the various links and joints of the
system at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>RIGID</tt> statement are coincident and are both defined by a single <tt>DATA RIGID</tt> statement by
specifying the global coordinates of three points (see figure). The first point defines the common
origins of the two local coordinate systems. The second point lies on the common local _w_ and
<i>w</i> axes and the third point lies on the common local _u_ and <i>u</i> axes of the coordinate
systems attached to the two links joined.

### Format ###
> DATA RIGID (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>RIGID</tt> joint connecting the two links to which
the local coordinate systems are attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric
values for the global coordinates of the three points defining the initial locations of the two
local coordinate systems._

### Example ###
> DATA RIGID (WELD) = -1.0,2.5,0.0; -1.0,3.5,0.0; -2.0,2.5,1.0

specifies the initial locations of the two coincident local coordinate systems attached to the two
links connected by a <tt>RIGID</tt> joint named _WELD_. The above example might also take any of the
following forms:

> DATA RIGID (WELD) = -1,2.5,0; -1,3.5,0; -2,2.5,1

> DATA RIGID (WELD) = -1,2.5, ; -1,3.5, ; -2,2.5,1

> DATA RIGID (WELD) = PT1; PT2; -2,2.5,1

> DATA RIGID (WELD) = PT1; PT2

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>RIGID</tt> statement. If not, the <tt>DATA RIGID</tt> statement is ignored and a message is printed.

# If a <tt>DATA RIGID</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>RIGID</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.

# If more than one <tt>DATA RIGID</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.

# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA RIGID</tt> statement are length units.

# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.

# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must define two coincident local coordinate systems (see_<tt>RIGID</tt> statement).

# The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.

# The angle formed by points _2_,_1_,_3_ need not be a right angle. IMP uses the first and second point to locate the common local origins and the common local _w_ and <i>w</i> axes; the common local _u_ and <i>u</i> axes are then formed in the half-plane defined by the common local _w_ and <i>w</i> axes and the third point. A right angle is formed for the common local _u_ and <i>u</i> axes in this half-plane even though this direction may not pass through the third point given.

# If the _x_<sub>3</sub>_,_y<sub>3</sub>_,_z<sub>3</sub>_data are not given for the third point, the coordinates of the global origin are used. This may be a convenient shortcut if the user is not concerned with the_u_,_<i>u</i> axis placement (see final example above). In view of note 8) above, this does not produce an error unless the common local _w_,<i>w</i> axes pass through the global origin.

# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).

## The <tt>DATA GEAR</tt> Statement ##
The <tt>DATA GEAR</tt> statement specifies the gear ratio and the center to
center distance for a <tt>GEAR</tt> joint.

### Format ###
> DATA GEAR (joint name) = ratio, distance

where _joint name_ is the alphanumeric name of the <tt>GEAR</tt> joint, _ratio_ is the numeric value of
the gear ratio for the joint, and _distance_ is the numeric value of the center to center distance
(the sum of the pitch radii) for the two mating <tt>GEAR</tt> sectors.

### Example ###
> DATA GEAR (SPUR) = 2.625, 6.25

specifies that the gear ratio of a spur gear joint named <tt>SPUR</tt> is 84:32 = 2.625, and that the sum
of the pitch radii of the mating gear sectors is 4.526 + 1.724 = 6.25 length units.

### Notes ###
# There must be a <tt>DATA GEAR</tt> statement for each joint defined by a <tt>GEAR</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
# The _joint name_ specified must have been defined by a previous <tt>GEAR</tt> statement. If not, the <tt>DATA GEAR</tt> statement is ignored and a message is printed.
# Unlike <tt>DATA</tt> statements describing certain other types of joints (for example, the <tt>DATA ZPIN</tt> statement), the <tt>DATA GEAR</tt> statement does not specify the locations of the two local coordinate systems for the <tt>GEAR</tt> joint; two <tt>DATA LINK</tt> statements must be defined for each _joint name_ defined by a <tt>GEAR</tt> statement. If these do not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA GEAR</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The value of _ratio_ is dimensionless; the value of _distance_ has units of length.
# The value of _ratio_ is the ratio of the number of teeth (or the pitch diameter) of the first gear named in the <tt>GEAR</tt> statement to the number of teeth (or pitch diameter) of the second gear named. A positive value of _ratio_ indicates that both are external gears, while a negative _ratio_ indicates an internal-external gear combination.
# A value of zero may not be used for _ratio_ to represent a gear-rack combination. A zero value for _ratio_ causes the <tt>DATA GEAR</tt> statement to be ignored and a message to be printed.
# The center to center _distance_ is optional; it need not be specified by the user. If it is not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, it will be calculated from data for the local coordinate systems on either side of the joint at that time.
# If the center to center _distance_ is given, it should be consistent with the placement of the two local coordinate systems on either side of the gear joint. If not consistent at the time an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the kinematic shapes of all links will be found first from the locations of the local coordinate systems; the two gear centers will then be set to the specified distance; any discrepancies will be compensated for by movements within the joints of the system when assembly is attempted at the design (initial) position.

## The <tt>DATA BEVEL</tt> Statement ##
The <tt>DATA BEVEL</tt> statement specifies the gear ratio and the size of the two bevel gears defined by a
previous <tt>BEVEL</tt> statement.

### Format ###
> DATA BEVEL (joint name) = ratio, radius

where each _joint name_ is the alphanumeric name of the <tt>BEVEL</tt> joint, _ratio_ is the numeric
value of the gear ratio for the joint, and _radius_ is the pitch circle radius of the second link
named in the <tt>BEVEL</tt> statement.

### Example ###
> DATA BEVEL (BVL) = 2.625, 2.0

specifies that the gear ratio of a <tt>BEVEL</tt> joint named <tt>BVL</tt> is 84/32 = 2.625 and that the back-face
pitch circle radii of the two bevel gears are 5.25 and 2.0 length units, respectively.

### Notes ###
# There must be a <tt>DATA BEVEL</tt> statement for each joint defined by a <tt>BEVEL</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
# The _joint name_ specified must have been defined by a previous <tt>BEVEL</tt> statement. If not, the <tt>DATA BEVEL</tt> statement is ignored and a message is printed.
# Unlike <tt>DATA</tt> statements describing certain other types of joints (for example, the <tt>DATA ZPIN</tt> statement), the <tt>DATA BEVEL</tt> statement does not specify the locations of the two local coordinate systems for the <tt>BEVEL</tt> joint; two <tt>DATA LINK</tt> statements must be defined for each <tt>BEVEL</tt> joint. If these do not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA BEVEL</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The value of _ratio_ is dimensionless; the value of _radius_ has units of length.
# The value of _ratio_ is the ratio of the number of teeth of the first bevel gear named in the <tt>BEVEL</tt> statement to the number of teeth of the second.
# The value of _ratio_ must be a positive number. A zero or negative value for _ratio_ causes the <tt>DATA BEVEL</tt> statement to be ignored and a message to be printed.
# The angle between the two intersecting shafts of a <tt>BEVEL</tt> joint is always 90 ° . The two local coordinate systems defined by the two <tt>DATA LINK</tt> statements are assumed to be at consistent distances from the intersection of the two shafts, that is, the u,v and u’,v’ planes are both chosen to go through the point of contact of the respective pitch circles (see figure with <tt>BEVEL</tt> statement). The _radius_ specified is the pitch circle radius of the second gear named, measured in the u,v plane. It should equal the distance from the shaft intersection to the u,v plane.


## The <tt>DATA RACK</tt> Statement ##
The <tt>DATA RACK</tt> statement specifies the pinion radius for a <tt>RACK</tt> joint.

### Format ###
> DATA RACK (joint name) = radius

where each _joint name_ is the alphanumeric name of the <tt>RACK</tt> joint and _radius_ is the pitch
circle radius of the second link named in the <tt>RACK</tt> statement.

### Example ###
> DATA RACK (MESH) = 2.5
specifies that the pitch circle radius of the pinion in a <tt>RACK</tt> joint named <tt>MESH</tt> is 2.5 length
units.

### Notes ###
# There must be a <tt>DATA RACK</tt> statement for each joint defined by a <tt>RACK</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
# The _joint name_ specified must have been defined by a previous <tt>RACK</tt> statement. If not, the <tt>DATA RACK</tt> statement is ignored and a message is printed.
# Unlike <tt>DATA</tt> statements describing certain other types of joints (for example, the <tt>DATA ZPIN</tt> statement), the <tt>DATA RACK</tt> statement does not specify the locations of the two local coordinate systems for the <tt>RACK</tt> joint; two <tt>DATA LINK</tt> state- ments must also be defined for each <tt>RACK</tt> joint. If these do not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local _u_,_v_,_w_ or <i>u</i>,<i>v</i>,<i>w</i> coordinate system(s) with missing data is (are) initially placed coincident with the x,y,z link frame of reference.
# If more than one <tt>DATA RACK</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The value of _radius_ has units of length. It should be equal to the perpendicular distance from the local <i>u</i>,<i>v</i>,<i>w</i> origin to the local u axis (see figure with the <tt>RACK</tt> statement).
# The value of _radius_ may not be zero. If zero is specified for _radius_, the <tt>DATA RACK</tt> statement is ignored and a message is printed.


## The <tt>DATA SCREW</tt> Statement ##
The <tt>DATA SCREW</tt> statement specifies the lead of a screw joint.

### Format ###
> DATA SCREW (joint name) = value

where _joint name_ is the alphanumeric name of the <tt>SCREW</tt> joint and _value_ is the numeric
value of the lead of the <tt>SCREW</tt> joint thread.

### Example ###
> DATA SCREW (THRD) = -0.750

specifies the lead of a <tt>SCREW</tt> joint named <tt>THRD</tt> as 0.750 length units per revolution with a
left-hand thread.

### Notes ###
# There must be a <tt>DATA SCREW</tt> statement for each joint defined by a <tt>SCREW</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
# The _joint name_ specified must have been defined by a previous <tt>SCREW</tt> statement. If not, the <tt>DATA SCREW</tt> statement is ignored and a message is printed.
# Unlike <tt>DATA</tt> statements describing certain other types of joints (for example, the <tt>DATA ZPIN</tt> statement), the <tt>DATA SCREW</tt> statement does not specify the locations of the two local coordinate systems for the <tt>SCREW</tt> joint; two <tt>DATA LINK</tt> statements must also be specified for each _joint name_ defined by a <tt>SCREW</tt> statement. If these do not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA SCREW</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The dimensions of _value_ are length units of advance of the screw per revolution. A right-hand thread has a positive _value_ and a left-hand thread has a negative _value_.
# The _value_ of the lead may not be zero. A <tt>REVOLUTE</tt> statement should be used instead of a <tt>SCREW</tt> for this case. If zero is specified for _value_, the <tt>DATA SCREW</tt> statement is ignored and a message is printed.


## The <tt>DATA CAM</tt> Statement ##
The <tt>DATA CAM</tt> statement specifies the shape of the pitch curve for a <tt>CAM</tt> joint.

### Format ###
> DATA CAM (joint name) = value name

where _joint name_ is the alphanumeric name of the <tt>CAM</tt> joint and _value name_ is the
alphanumeric name of a previously defined <tt>VALUE</tt> expression set equal to a <tt>TABLE</tt> function giving
data for the pitch curve for the <tt>CAM</tt> joint.

### Example ###
> VALUE (R) = TABLE (PHI): datafile.dat
> DATA CAM (CURV) = R

specifies that the pitch curve radius of a <tt>CAM</tt> joint named <tt>CURV</tt> is specified by a <tt>VALUE</tt>
expression named R which refers to a <tt>TABLE</tt> function referencing a file named “datafile.dat_._

### Notes ###
# There must be a <tt>DATA CAM</tt> statement for each joint defined by a <tt>CAM</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
# The _joint name_ specified must have been defined by a previous <tt>CAM</tt> statement. If not, the <tt>DATA CAM</tt> statement is ignored and a message is printed.
# Unlike <tt>DATA</tt> statements describing certain other types of joints (for example, the <tt>DATA ZPIN</tt> statement), the <tt>DATA CAM</tt> statement does not specify the locations of the two local coordinate systems for the <tt>CAM</tt> joint; two <tt>DATA LINK</tt> state- ments must also be defined for each <tt>CAM</tt> joint. If these do not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA CAM</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The _value name_ must refer to a previously defined <tt>VALUE</tt> expression consisting solely of a <tt>TABLE</tt> function; other kinds of <tt>VALUE</tt> expression cannot be used. If this is not satisfied the <tt>DATA CAM</tt> statement is ignored and a message is printed.
# The argument of the <tt>TABLE</tt> function is arbitrary and is not used. During the simulation, the <tt>TABLE</tt> function is evaluated as if the independent variable is the first joint variable of the <tt>CAM</tt> joint, an angle (in radians). Thus the data file referred to by the <tt>TABLE</tt> function should specify tabular data (see section 2-7.29) for the radius of the pitch curve as a function of angle (in radians) measured relative to the u,v coordinate system (see figure with the <tt>CAM</tt> statement) of the first link named in the <tt>CAM</tt> statement. The tabular data should specify radii for equally spaced angular increments for a full rotation (2 PI = 6.28318 radians).
# The dimensions of the tabular data for the pitch curve radius are in length units.


## The <tt>DATA SLOT</tt> Statement ##
The <tt>DATA SLOT</tt> statement specifies the shape of the slot for a <tt>SLOT</tt> joint.

### Format ###
> DATA SLOT (joint name) = value name

where _joint name_ is the alphanumeric name of the <tt>SLOT</tt> joint and _value name_ is the
alphanumeric name of a previously defined <tt>VALUE</tt> expression set equal to a <tt>TABLE</tt> function giving
data for the centerline curve of the slot.

### Example ###
> VALUE (Y) = TABLE<tt> (</tt>PHI`): datafile.dat
> DATA SLOT (CURV) = V

specifies that the profiled shape of the centerline curve of a <tt>SLOT</tt> joint named <tt>CURV</tt> is
specified by a file named “datafile.dat_and a_<tt>VALUE</tt> expression named V accessing that file via a
<tt>TABLE</tt> function.

### Notes ###
# There must be a <tt>DATA SLOT</tt> statement for each joint defined by  a <tt>SLOT</tt> statement. If these are not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the simulation is halted and a message is printed.
# The _joint name_ specified must have been defined by a previous <tt>SLOT</tt> statement. If not, the <tt>DATA SLOT</tt> statement is ignored and a message is printed.
# Unlike <tt>DATA</tt> statements describing certain other types of joints (for example, the <tt>DATA ZPIN</tt> statement), the <tt>DATA SLOT</tt> statement does not specify the locations of the two local coordinate systems for the <tt>SLOT</tt> joint; two <tt>DATA LINK</tt> statements must also be defined for each <tt>SLOT</tt> joint. If these do not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA SLOT</tt> statement is given for the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The _value name_ must refer to a previously defined <tt>VALUE</tt> expression consisting solely of a <tt>TABLE</tt> function; other kinds of <tt>VALUE</tt> expression cannot be used. If this is not satisfied the <tt>DATA SLOT</tt> statement is ignored and a message is printed.
# The argument of the <tt>TABLE</tt> function is arbitrary and is not used. During the simulation, the <tt>TABLE</tt> function is evaluated as if the independent variable is the first joint variable of the <tt>SLOT</tt> joint, a distance along the u axis (see figure for the <tt>SLOT</tt> joint). Thus the datafile referred to by the <tt>TABLE</tt> function should specify tabular data (see section 2-7.29) for the v distances for the profiled slot centerline as a function of u relative to the u,v coordinate system of the first link named in the <tt>SLOT</tt> statement. The tabular data should specify v(u) values for equally spaced increment of u over the full length of the slot.
# The dimensions for v in the tabular data for the slot profile are length units.


## The <tt>DATA UJOINT</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_12.png' height='400px' />
_Figure 4-12:_
The <tt>DATA UJOINT</tt> statement specifies the numeric data which simultaneously locate the two local
coordinate systems attached to the two links on either side of a <tt>UJOINT</tt> joint relative to the
absolute (global) frame of reference for the system.

The <tt>DATA UJOINT</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints
and the <tt>DATA LINK</tt> statements, describe the of relative locations the various links of the system
at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>UJOINT</tt> statement are both defined by a single <tt>DATA UJOINT</tt> statement by specifying the global
coordinates of three points (see figure). The first point must lie at the common origins of the two
local coordinate systems. The second and third points must lie on the local positive w and w’ axes
of the coordinate systems attached to the first and second links named in the <tt>UJOINT</tt> statement,
respectively.

### Format ###
> DATA UJOINT (joint name) = x<sub>1</sub>,y<sub>1</sub>,z<sub>1</sub>; x<sub>2</sub>,y<sub>2</sub>,z<sub>2</sub>; x<sub>3</sub>,y<sub>3</sub>,z<sub>3</sub>

where _joint name_ is the alphanumeric name of the <tt>UJOINT</tt> connecting the two links to which the
local coordinate systems are attached. The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups are numeric
values for the global coordinates of the three points defining the initial locations of the two
local coordinate systems._

### Examples ###
> DATA UJOINT (UJNT) = -1.0,2.0,0.0; 0.0,2.0,1.0; -1.0,3.0,0.0

specifies the initial locations of the local coordinate systems attached to the two links on either
side of a <tt>UJOINT</tt> named <tt>UJNT</tt>. The numeric data corresponds approximately to the figure.

The above example might also take any of the following forms:
> DATA UJOINT (UJNT) = -1,2,0; 0,2,1; -1,3,0
> DATA UJOINT (UJNT) = -1,2, ; ,2,1; -1,3
> DATA UJOINT (UJNT) = PT1; 0,2,1; -1,3,0
> DATA UJOINT (UJNT) = PT1; PT2; PT3

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>UJOINT</tt> statement. If not, the <tt>DATA UJOINT</tt> statement is ignored and a message is printed.
# If a <tt>DATA UJOINT</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>UJOINT</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA UJOINT</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.
# The dimensions for all _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data in a_<tt>DATA UJOINT</tt> statement are length units.
# Care should be taken in supplying accurate dimensional data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
# The _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data must conform to the rules for the placement of the local coordinate systems for a universal joint (see_<tt>UJOINT</tt> statement). If errors are detected, the <tt>DATA UJOINT</tt> statement is ignored and a message is printed. Certain types of errors may not be detected until an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; these cause the simulation to be halted and a message to be printed at that time.
# The three points for which _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_numeric data are given need not be unit distances apart; the local_u_,_v_,_w_and_<i>u</i>,<i>v</i>,<i>w</i> axes are normalized by IMP to form unit vectors. The points should not be chosen coincident or too close together, however; larger distances achieve more accurate placement of axes.
# Any of the _x_<sub>i</sub>_,_y<sub>i</sub>_,_z<sub>i</sub>_groups of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid_<tt>DATA POINT</tt> statement has previously been given (see above examples).

## The <tt>DATA SPHERE</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_13.png' height='400px' />
_Figure 4-13:_
The <tt>DATA SPHERE</tt> statement specifies the numeric data which simultaneously locate the two local
coordinate systems attached to the two links on either side of a <tt>SPHERE</tt> joint relative to the
absolute (global) frame of reference for the system.

The <tt>DATA SPHERE</tt> statements, taken together with the <tt>DATA</tt> statements for other types of joints
and the <tt>DATA LINK</tt> statements, describe the relative locations of the various links of the system
at the initial (design) position.

The initial locations of the two local coordinate systems attached to the two links joined by a
<tt>SPHERE</tt> statement are both defined by a single <tt>DATA SPHERE</tt> statement by specifying the location
of one point, the center of the <tt>SPHERE</tt> joint. However, IMP chooses the orientations of the local
_u_,_v_,_w_ and <i>u</i>,<i>v</i>,<i>w</i> axes; thus the user has no control of their orientation.
If the user wishes to control the orientations of the local _u_,_v_,_w_ and
<i>u</i>,<i>v</i>,<i>w</i> coordinate systems, a pair of <tt>DATA LINK</tt> statements should be used rather than
a <tt>DATA SPHERE</tt> statement.

### Format ###
> DATA SPHERE (joint name) = x,y,z

where _joint name_ is the alphanumeric name of the <tt>SPHERE</tt> joint connecting the two links to
which the local coordinate systems are attached. The _x,y,z_ group is comprised of numeric values
for the global coordinates of the common local origins, the location of the center of the <tt>SPHERE</tt>
joint.

### Examples ###
> DATA SPHERE (BALL) = -1.0, 1.0, 1.0

specifies the initial locations of the local coordinate systems attached to the two links on either
side of a <tt>SPHERE</tt> joint named <tt>BALL</tt>. The numeric data corresponds approximately to the figure.

The above example might also take either of the following forms:
> DATA SPHERE (BALL) = -1,1,1
> DATA SPHERE (BALL) = PT1

### Notes ###
# The _joint name_ specified must have been defined by a previous <tt>SPHERE</tt> statement. If not, the <tt>DATA SPHERE</tt> statement is ignored and a message is printed.
# If a <tt>DATA SPHERE</tt> statement or the two equivalent <tt>DATA LINK</tt> statements are not specified for each _joint name_ defined by a <tt>SPHERE</tt> statement before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the local coordinate system(s) with missing data is (are) initially placed coincident with the link frame of reference.
# If more than one <tt>DATA SPHERE</tt> statement is given for the same _joint name_, the later statement takes precedence and earlier data are replaced.
# The dimensions for the _x,y,z_ data in a <tt>DATA SPHERE</tt> statement are length units.
# Care should be taken in supplying accurate _x,y,z_ data since any errors result in improper shapes for the links and remain throughout the simulation. Slight errors cause inaccurate answers, while gross errors may cause completely unpredictable results.
# The _x,y,z_ group of numeric data may be replaced by the alphanumeric name of a previously defined point for which a valid <tt>DATA POINT</tt> statement has previously been given (see above example).

## The <tt>DATA POINT</tt> Statement ##
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_14.png' height='400px' />
_Figure 4-14:_
The <tt>DATA POINT</tt> statement specifies the location of a point defined in a previous <tt>POINT</tt> statement.

### Format ###
There are three forms of the <tt>DATA POINT</tt> statement.

The first form is used to specify the location of a point relative to one of the local joint
coordinate systems attached to the link of which the point is a part:

> DATA POINT (point name, joint name) = _u_,_v_,_w_

where _point name_ is the alphanumeric name of the point, _joint name_ is the alphanumeric name
of the joint whose local coordinate system is used for reference, and _u_,_v_,_w_ are the
numeric values of the point's coordinates relative to this local coordinate system.

The second form is identical with the first except that _joint name_ is replaced by the keyword
<tt>LINK</tt>:

> DATA POINT (point name, LINK) = x,y,z

which indicates that the local coordinate system of the link to which the point is attached is used
for specifying of the _x,y,z_ data.

The third form is also identical with the first except that _joint name_ is replaced by the
keyword <tt>ABS</tt>:

> DATA POINT (point name, <tt>ABS</tt>) = X,Y,Z

which indicates that the global coordinate system is used for measurement of the numeric _X,Y,Z_
data.

### Examples ###
> DATA POINT (PT1, JT1) = 2.0,2.0,0.0

specifies the location of a point named PT1 relative to a local coordinate system at a joint named
JT1 as shown in the figure.

Three other valid specifications, which also correspond to the figure, are:
> DATA POINT (PT1, JT2) = -3,2,0
> DATA POINT (PT1, <tt>LINK</tt>) = 0,2,0
> DATA POINT (PT1, <tt>ABS</tt>) = 2,5,0


### Notes ###
# There must be a <tt>DATA POINT</tt> statement for each point defined by a <tt>POINT</tt> statement. If one does not appear before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the point with missing data is placed at the origin of the local link coordinate system.
# The _point name_ specified must have been defined by a previous <tt>POINT</tt> statement. If not, the <tt>DATA POINT</tt> statement is ignored and a message is printed.
# The _joint name_, if specified, must have been defined in a previous statement, and it must be connected to the same link to which the point is attached. If not, the <tt>DATA POINT</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA POINT</tt> statement is given referring to the same _point name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The _u_,_v_,_w_ or _x,y,z_ or _X,Y,Z_ coordinate data have units of length.
# When the <tt>ABS</tt> form of the <tt>DATA POINT</tt> statement is used, the _X,Y,Z_ data may be replaced by the alphanumeric name of a previously defined point for which a valid <tt>DATA POINT</tt> statement has already been given.

## The <tt>DATA GRAVITY</tt> Statement ##
The <tt>DATA GRAVITY</tt> statement specifies the components of the gravitational acceleration vector
relative to the global coordinatesystem. It also specifies that the weights and potential energy
changes of all links which have mass should henceforth be considered in performing the simulation.

### Format ###
> DATA GRAVITY = g<sub>x</sub>,g<sub>y</sub>,g<sub>z</sub>
where _g_<sub>x</sub>,g<sub>y</sub>,g<sub>z</sub>_are the numeric values of the global components of the gravitational
acceleration vector._

### Example ###
> DATA GRAVITY = 0,-386.1,0

specifies that the acceleration of gravity is 386.1 length units per second per second in the global
negative Y direction.

### Notes ###
# The <tt>DATA GRAVITY</tt> statement is optional. However, if it is not included before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given, the effects of gravity, that is, the gravitational forces due to the weights of the links, are neglected in the simulation. No message is printed.
# Even with the <tt>DATA GRAVITY</tt> statement included, the effects of gravity are neglected for any link whose mass is not specified by <tt>SHAPE</tt> and <tt>DATA DENSITY</tt> statements or by a <tt>DATA MASS</tt> statement. No message is printed.
# If more than one <tt>DATA GRAVITY</tt> statement is specified, the later statement takes precedence; earlier data are replaced and a message is printed.
# If a <tt>FIND EQUILIBRIUM</tt> statement (static mode) or a <tt>FIND DYNAMICS</tt> statement (dynamic mode) is encountered before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, a <tt>DATA GRAVITY</tt> statement causes potential energy changes due to gravity to be considered in determining the position or motion of the system. If neither of these statements is encountered (kinematic mode), potential energy changes are not considered in determining the system's position. However, gravitational forces are considered for all modes when performing constraint force analyses.
# The dimensions of the gravity vector are length units per second per second.
# Standard gravity in US Customary units is 386.088 inches per second per second.
# There is no assumption made that the gravitational acceleration vector has a 1.0 g magnitude. The conversion of mass units to weight units is not related to the <tt>DATA GRAVITY</tt> statement, but can be controlled by use of the <tt>UNIT</tt> (<tt>MASS</tt>) statement.


## The <tt>DATA DENSITY</tt> Statement ##
The <tt>DATA DENSITY</tt> statement specifies the mass density for a shape defined by a <tt>SHAPE</tt> statement.
The <tt>DATA DENSITY</tt> statement causes the automatic calculation of the mass, the center of mass, and
the mass moments and products of inertia for that shape and updates the mass properties of the
associated link using the specified material density.

### Format ###
> DATA DENSITY (shape name) = density

where _shape name_ is the alphanumeric name of a solid which has been named in a previous <tt>SHAPE</tt> statement and _density_ is the numeric value of the mass density of that shape's material.
### Example ###
> SOLID READ (ROD) = rod.geo
> SHAPE (SHAFT) = ROD DATA DENSITY (ROD) = 0.286

specifies that the material for the shape named <tt>ROD</tt> of the link named <tt>SHAFT</tt> has mass density of
0.286 mass units per cubic length unit, and that the shape of <tt>ROD</tt> (from file _rod.geo_) is to be
used with this density to find the mass, the center of mass location, and the mass moments and
products of inertia for that part of link <tt>SHAFT</tt>.

### Notes ###
# The <tt>DATA DENSITY</tt> statement is optional; it may, but need not, be used for any shape specified in a <tt>SHAPE</tt> statement.
# A <tt>DATA MASS</tt> and/or set of <tt>DATA DENSITY</tt> statements is necessary for all solid shapes of each link whose mass is to be considered in the simulation. Each link whose mass is not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given is considered to have no kinetic energy and no gravitational potential energy. No message is printed.
# The _shape name_ specified must have appeared in a previous <tt>SHAPE</tt> statement specifying that the _shape name_ is a part of a particular link. If the link has not been named in a <tt>SHAPE</tt> statement, or if the _shape name_ and its geometry have not been defined, before the <tt>DATA DENSITY</tt> statement is given, the <tt>DATA DENSITY</tt> statement is ignored and a message is printed.
# If a solid shape has been defined for a part of a link with a <tt>SHAPE</tt> statement, the <tt>DATA DENSITY</tt> statement should be used rather than the <tt>DATA MASS</tt> or <tt>DATA INERTIA</tt> statements in order to ensure consistency with the defined part shape. If no shape has been defined by a <tt>SHAPE</tt> statement a <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statement should be used instead.
# If both <tt>DATA DENSITY</tt> and <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements are used for the same link or its subordinate solid parts, the <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements should be given first for the portion of the link which has no defined shape. <tt>DATA DENSITY</tt> statements given after this for solid part shapes of the same link then cause the total mass of the link and its distribution to be properly incremented.
# If more than one <tt>DATA DENSITY</tt> statement is given for the same _shape name_, the total mass and mass distribution of the link are incremented multiple times, thus causing an error; no message is printed. Notice, however, that different <tt>DATA DENSITY</tt> statements may be used for the different _shape names_ attached to the same _link name_. The total mass properties of the link will then include the combination of all sub-shapes of the total geometry of the link.
# If more than one <tt>DATA MASS</tt> or <tt>DATA INERTIA</tt> statement is given for the same _link name_, the later data takes precedence and earlier data are replaced. Notice, however, that the increments caused by earlier <tt>DATA DENSITY</tt> statements for _shape names_ on this link are lost.
# The _density_ value has units of mass per cubic length. When using inches, seconds, and pounds force, for example, and density has units of pounds mass per cubic inch, then a <tt>UNIT MASS</tt> = 0.002950l statement must be in effect at the time that the <tt>DATA DENSITY</tt> statement is issued. When using meters, seconds, and newtons, the density is given in kilograms per See the <tt>UNIT MASS</tt> cubic meter and <tt>UNIT</tt> (<tt>MASS</tt>) = 1.0. statement in Chapter 6 for more details.
# If a <tt>FIND EQUILIBRIUM</tt> statement (static mode) or a <tt>FIND DYNAMICS</tt> statement (dynamic mode) and a <tt>DATA GRAVITY</tt> statement are encountered before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, potential energy changes due to gravity are considered in determining the position or motion of the system. If a <tt>FIND EQUILIBRIUM</tt> or <tt>FIND DYNAMICS</tt> statement does not appear (kinematic mode), gravitational potential energy is not considered in determining the system's position. In all modes, however, gravity is considered in constraint force analysis if a <tt>DATA GRAVITY</tt> statement is given.
# If a <tt>FIND DYNAMICS</tt> statement (dynamic mode) is encountered before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, the kinetic energies of all links for which valid <tt>DATA DENSITY</tt> or <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements are specified are considered in determining the motion of the system. In either kinematic or dynamic mode, the kinetic energies of all moving masses are considered in constraint force analysis.


## The <tt>DATA MASS</tt> Statement ##
The <tt>DATA MASS</tt> statement specifies the mass and the location of the center of mass of one link of
the system.

### Format ###
> DATA MASS (link name, joint name) = m; _u_,_v_,_w_

where _link name_ is the alphanumeric name of the link, _m_ is the numeric value of the mass of
the link and _u_,_v_,_w_ are the numeric values of the coordinates of the center of mass of
the link measured relative to the local coordinate system attached to _link name_ at the joint
with the alphanumeric name _joint name_.

### Example ###
> DATA MASS (ROD, UJNT) = 0.5; 3.25,0.0,0.0

specifies that the mass of the link named <tt>ROD</tt> is 0.5 mass units, and that its center of gravity is
located at u=3.25, v=0, and w=0, relative to the local coordinate system attached to <tt>ROD</tt> at the
joint named <tt>UJNT</tt>.

### Notes ###
# The <tt>DATA MASS</tt> and <tt>DATA DENSITY</tt> statements are optional; they may be used repeatedly to specify masses for as many or as few links as desired.
# A separate <tt>DATA MASS</tt> or set of <tt>DATA DENSITY</tt> statements is necessary for each link whose mass is to be considered in the simulation. Each link whose mass is not specified before an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given is considered to have no kinetic energy and no gravitational potential energy. No message is printed.
# The _link name_ specified must have appeared in at least one previous statement defining a link or a joint. If not, the <tt>DATA MASS</tt> statement is ignored and a message is printed.
# The keyword <tt>LINK</tt> can be used in place of a _joint name_; if this is done if signifies that _x,y,z_ data are specified with respect to the coordinate system of _link name_ instead of _u_,_v_,_w_ data.
# Unless the keyword <tt>LINK</tt> is used, the _joint name_ specified must have been defined in a previous statement defining a joint, and it must be a connection for the same _link name_ for which the mass is specified. If not, the <tt>DATA MASS</tt> statement is ignored and a message is printed.
# If both <tt>DATA DENSITY</tt> and <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements are used for the same link or its subordinate solid part shapes, the <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements should be given first for the portion of the link which has no defined shape. <tt>DATA DENSITY</tt> statements given after this for solid part shapes of the same link then cause the total mass of the link and its distribution to be properly incremented.
# If more than one <tt>DATA MASS</tt> or <tt>DATA INERTIA</tt> statement is given for the same _link name_, the later data takes precedence and earlier data are replaced. Notice, however, that the increments caused by any earlier <tt>DATA DENSITY</tt> statements for _shape names_ on this link are lost; no message is printed.
# The _m_ value has units of mass; the _u_,_v_,_w_ or _x,y,z_ coordinates have units of length. When using inches, seconds, and pounds force, _m_ has units of pounds mass; then a <tt>UNIT MASS</tt> = 0.0025901 statement must be in effect at the time the <tt>DATA MASS</tt> statement is issued. When using meters, seconds, and newtons, then _m_ is given in kilograms and <tt>UNIT MASS</tt> = 1.0. See the <tt>UNIT MASS</tt> statement in Chapter 6.
# When a <tt>DATA MASS</tt> statement is given, mass data for a point mass located at the center of gravity of the specified _link name_ are stored; appropriate mass moments and products of inertia relative to the designated _joint name_ local coordinate system are also stored. A subsequent <tt>DATA INERTIA</tt> statement may then be used, if desired, to specify distributed mass moments and products of inertia.
# A <tt>DATA MASS</tt> or <tt>DATA DENSITY</tt> statement may be specified for the fixed link if desired, but has no effect on the simulation.
# If a <tt>FIND EQUILIBRIUM</tt> statement (static mode) or a <tt>FIND DYNAMICS</tt> statement (dynamic mode) and a <tt>DATA GRAVITY</tt> statement are encountered before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, potential energy changes due to gravity are considered in determining the position or motion of the system. If a <tt>FIND EQUILIBRIUM</tt> or <tt>FIND DYNAMICS</tt> statement does not appear (kinematic mode), gravitational potential energy is not considered in determining the system's position. In all modes, however, gravity is considered in constraint force analysis if a <tt>DATA GRAVITY</tt> statement is given.
# If a <tt>FIND DYNAMICS</tt> statement (dynamic mode) is encountered before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, the kinetic energies of all links for which <tt>DATA MASS</tt> or <tt>DATA DENSITY</tt> statements are specified are considered in determining the motion of the system. In either kinematic or dynamic mode, the kinetic energies of all moving masses are considered in constraint force analysis.


## The <tt>DATA INERTIA</tt> Statement ##
The <tt>DATA INERTIA</tt> statement may be used to specify the distributed mass moments and products of
inertia of a link for which a <tt>DATA MASS</tt> statement has been given.

### Format ###
> DATA INERTIA (link name, joint name) = I<sub>xx</sub>,I<sub>yy</sub>,I<sub>zz</sub>,I<sub>xy</sub>,I<sub>xz</sub>,I<sub>yz</sub>

where _link name_ is the alphanumeric name of the link and _Ixx,Iyy,...,Iyz_ are the numeric values of the mass moments and products of inertia measured relative to the local _u_,_v_,_w_ coordinate system attached to _link name_ at the joint with the alphanumeric name _joint name_.

### Example ###
> DATA INERTIA (ROD, UJNT) = 0.002,16.7,16.7,0.0,0.0,0.0

specifies the mass moments and products of inertia of a link named <tt>ROD</tt> relative to the local _u_,_v_,_w_ coordinate system at the joint named <tt>UJNT</tt>.

### Notes ###
# Use of the <tt>DATA INERTIA</tt> statement is optional; it may be used repeatedly to specify distributed inertia properties for as many or as few links as desired.
# If a <tt>DATA INERTIA</tt> statement is used, a <tt>DATA MASS</tt> statement must have been previously specified for the same _link name_. If not, the <tt>DATA INERTIA</tt> statement is ignored and a message is printed.
# The keyword <tt>LINK</tt> can be used for _joint name_; if this is done it signifies that the _I_<sub>xx</sub>,I<sub>yy</sub>,...,I<sub>yz</sub>_data are spec- ified with respect to the_x,y,z_coordinate system of_link name_.
# The_joint name_specified must have been previously defined, and must be a connection for the same_link name_for which the mass moments and products of inertia are specified. If not, the_<tt>DATA INERTIA</tt> statement is ignored and a message is printed.
# The _joint name_ specified need not be the same as the _joint name_ used in the corresponding <tt>DATA MASS</tt> statement, although this is permitted and is often convenient.
# If both <tt>DATA DENSITY</tt> and <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements are used for the same link or its subordinate solid part shapes, the <tt>DATA MASS</tt> and <tt>DATA INERTIA</tt> statements should be given first for the portion of the link which has no defined shape. <tt>DATA DENSITY</tt> statements given after this for solid part shapes of the same link then cause the total mass of the link and its distribution to be properly incremented.
# If more than one <tt>DATA MASS</tt> or <tt>DATA INERTIA</tt> statement is given for the same _link name_, the later data takes precedence and earlier data are replaced. Notice, however, that the increments caused by any earlier <tt>DATA DENSITY</tt> statements for _shape names_ on this link are lost; no message is printed.
# The units for the mass moments and products of inertia are mass length squared (for example, pounds mass inches squared or kilogram meters squared). See the <tt>UNIT MASS</tt> statement in Chapter 6 for further discussion.
# When a <tt>DATA MASS</tt> statement is given, data for a point mass located at the specified center of mass of that link are stored. Appropriate mass moments and products of inertia for a point mass are also stored relative to the designated _joint name_ local coordinate system. A subsequent <tt>DATA INERTIA</tt> statement may then be used to specify distributed mass moments and products of inertia if desired.
# A <tt>DATA INERTIA</tt> statement may be specified for the fixed link if desired, but has no effect on the simulation.


## The <tt>DATA SPRING</tt> Statement ##
There are two uses of the <tt>DATA SPRING</tt> statement. One use is to specify the rate and free length of
a spring defined by a previous <tt>SPRING</tt> statement. The other use is to specify the rates (stiffness)
and free (unloaded) positions of springs acting with the joint variable(s) of a previously defined
joint.

### Format ###
> DATA SPRING (name) = rate,position; rate,position; ...

where _name_ is the alphanumeric name of a previously defined spring or joint. If _name_ was
defined by a previous <tt>SPRING</tt> statement, then only one _rate_ and _position_ are specified; if
_name_ refers to a joint, then a _rate_ and _position_ are specified for each joint variable
in succession. Each _rate_ is the numeric value of a spring rate or joint stiffness and each
_position_ is the numeric length of a spring or value of a joint variable for which the spring or
joint stiffness produces no load.

### Examples ###
> DATA SPRING (PULL) = 100.0, 5.25

specifies that a spring named <tt>PULL</tt> has a rate of 100.0 force units per unit deflection, and a free
length of 5.25 length units.

> DATA SPRING (PIN) = K, -45

specifies that there is torsional stiffness in the joint named <tt>PIN</tt>. The stiffness is defined by a
previous <tt>VALUE</tt> expression with the name <tt>K</tt> (see note 6), and the joint is in an unloaded position
when the joint variable has a value of -45°.

> DATA SPRING (CYL) = NONE, NONE; 1200,2.5

specifies that a cylindric joint named CYL has no rotational stiffness along with the first joint
variable (see note 7), but does have a translational stiffness acting with the second joint variable.
The translational stiffness is 1200 force units per unit deflection, and there is no force
transmitted when the second joint variable (the translation) has a value of 2.5 length units.
### Notes ###
# There must be a <tt>DATA SPRING</tt> statement for each spring defined by a <tt>SPRING</tt> statement. If these do not appear before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, any spring with undefined data is deleted and a message is printed at that time.
# <tt>DATA SPRING</tt> statements need not be given for all joints, but may be used for as many or few as desired.
# The _name_ specified must have been defined by a previous <tt>SPRING</tt> statement or joint definition statement. If not, the <tt>DATA SPRING</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA SPRING</tt> statement is encountered using the same _name_, the later data takes precedence; earlier data are replaced and a message is printed.
# The units for the _rate_ of a tension or compression spring are force per unit length of deflection from the free position. The _rate_ of a torsion spring has units of torque per degree of deflection from the free position. The free _position_ has units of length or degrees.
# The numeric value of any _rate_ or _position_ may be substituted for by the alphanumeric name of a previously defined <tt>VALUE</tt> expression. In such a case, however, the units of a <tt>VALUE</tt> expression for a torsion _rate_ must be torque per radian and the units of a <tt>VALUE</tt> expression for a rotational _position_ must be radians.
# The keyword <tt>NONE</tt> may be used in place of any _rate_ and _position_ for any joint variable for which no stiffness is intended. If the keyword <tt>NONE</tt> is used for a _rate_ or _position_ value, <tt>NONE</tt> is also used for the other value.


## The <tt>DATA DAMPER</tt> Statement ##
There are two uses for the <tt>DATA DAMPER</tt> statement. One use is to specify the damping coefficient of
a viscous damper defined by a <tt>DAMPER</tt> statement. The other use is to specify the coefficients of
viscous damping acting within the joint variable(s) of a previously defined joint.

### Format ###
> DATA DAMPER (name) = coefficient, coefficient, ...

where _name_ is the alphanumeric name of a previously defined damper or joint. If _name_ was
defined by a previous <tt>DAMPER</tt> statement, then only one _coefficient_ is given; if _name_ refers
to a joint, then a _coefficient_ is given for each joint variable in succession. Each
_coefficient_ is the numeric value of a damping coefficient.

### Examples ###
> DATA DAMPER (SLOW) = 4.75

specifies that a viscous damper named <tt>SLOW</tt> has a damping coefficient of 4.75 force seconds per
unit length.

> DATA DAMPER (LOSS) = C

specifies that there is viscous damping in a revolute joint named <tt>LOSS</tt>. The damping coefficient is
defined by a previous <tt>VALUE</tt> expression named <tt>C</tt> (see note 6).

> DATA DAMPER (CYL) = 0.15, NONE

specifies that there is viscous damping of 0.15 force length seconds per radian resisting the motion
of the first joint variable (rotation) of a cylindric joint named CYL, but no damping with the
motion of the second joint variable, the translation (see note 7).

### Notes ###
# There must be a <tt>DATA DAMPER</tt> statement for each damper defined by a <tt>DAMPER</tt> statement. If these do not appear before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, any damper with undefined data is deleted and a message is printed at that time.
# <tt>DATA DAMPER</tt> statements need not be given for all joints, but may be used for as many or as few as desired.
# The _name_ specified must have been defined by a previous <tt>DAMPER</tt> statement or a joint definition statement. If not, the <tt>DATA DAMPER</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA DAMPER</tt> statement is encountered using the same _name_, the later data takes precedence; earlier data are replaced and a message is printed.
# The units for the _coefficient_ of a translational damper are force seconds per unit length; for a torsional damper, the units are force length seconds per radian.
# The numeric value of any _coefficient_ may be substituted for by the alphanumeric name of a previously defined <tt>VALUE</tt> expression.
# The keyword <tt>NONE</tt> may be used in place of any _coefficient_ for a joint variable for which no damping is intended.


## The <tt>DATA FORCE</tt> Statement ##
There are two uses for the <tt>DATA FORCE</tt> statement. One use is to specify the magnitude of an
externally applied force defined by a <tt>FORCE</tt> statement. The other use is to specify the magnitudes
of pairs of equal and opposite forces or torques applied along each of the joint variables of a
previously defined joint.

### Format ###
> DATA FORCE (name) = force, force, ...

where _name_ is the alphanumeric name of a previously defined force or joint. If _name_ was
defined by a previous <tt>FORCE</tt> statement, then only one _force_ is given; if _name_ refers to a
joint, then a _force_ is given for each joint variable in succession. Each _force_ is the
numeric value of an applied force or torque.

### Examples ###
> DATA FORCE (PUSH) = -100

specifies that an externally applied force named <tt>PUSH</tt> has a magnitude of -100 force units.

> DATA FORCE (PULL) = F

specifies that a force named <tt>PULL</tt> has a magnitude defined by a previous <tt>VALUE</tt> expression named
<tt>F</tt> (see note 7).

> DATA FORCE (CYL) = NONE, 15.2

specifies that there is no externally applied torque acting on the rotational joint variable of the
cylindric joint named CYL (see note 8), but that equal and opposite forces of magnitude 15.2 force
units are applied along the translational joint variable.

### Notes ###
# There must be a <tt>DATA FORCE</tt> statement for each force defined by a <tt>FORCE</tt> statement. If these do not appear before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, any force with undefined data is deleted and a message is printed at that time.
# <tt>DATA FORCE</tt> statements need not be given for all joints, but may be used for as many or as few as desired.
# The _name_ specified must have been defined by a previous <tt>FORCE</tt> statement or a joint definition statement. If not, the <tt>DATA FORCE</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA FORCE</tt> statement is encountered using the same _name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The units for a _force_ are force units if the _name_ refers to a <tt>FORCE</tt> statement. If the _name_ refers to a joint, then units of force are used for a translational joint variable _force_ and units of length force are used for a rotational joint variable _force_.
# The sign of the _force_ value must be consistent with the order of the point names specified in the <tt>FORCE</tt> statement. A _force_ value applied within a joint is considered positive if it tends to change the value of the joint variable in the positive sense.
# The numeric value of any _force_ may be substituted for by the alphanumeric name of a previously defined <tt>VALUE</tt> expression.
# The keyword <tt>NONE</tt> may be used in place of any _force_ for a joint variable for which no externally applied force is intended.


## The <tt>DATA TORQUE</tt> Statement ##
There are two uses for the <tt>DATA TORQUE</tt> statement. One use is to specify the magnitude of an
externally applied torque defined by a <tt>TORQUE</tt> statement. The other use is to specify the
magnitudes of pairs of equal and opposite forces or torques applied along each of the joint
variables of a previously defined joint.

### Format ###
> DATA TORQUE (name) = torque, torque, ...

where _name_ is the alphanumeric name of a previously defined torque or joint. If _name_ was
defined by a previous <tt>TORQUE</tt> statement, then only one _torque_ is given; if _name_ refers to a
joint, then a _torque_ is given for each joint variable in succession. Each _torque_ is the
numeric value of an applied torque or force.

### Examples ###
> DATA TORQUE (TWIST) = -100

specifies that an externally applied torque named <tt>TWIST</tt> has a magnitude of -100 torque units.

> DATA TORQUE (TURN) = F

specifies that a torque named <tt>TURN</tt> has a magnitude defined by a previous <tt>VALUE</tt> expression named
<tt>F</tt> (see note 7).

> DATA TORQUE (CYL) = 15.2, NONE

specifies that there are equal and opposite externally applied torques acting on the rotational
joint variable of the cylindric joint named <tt>CYL</tt>, but that no force is applied along the
translational joint variable (see note 8).

### Notes ###
# There must be a <tt>DATA TORQUE</tt> statement for each torque defined by a <tt>TORQUE</tt> statement. If these do not appear before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, any torque with undefined data is deleted and a message is printed at that time.
# <tt>DATA TORQUE</tt> statements need not be given for all joints but may be used for as many or as few as desired.
# The _name_ specified must have been defined by a previous <tt>TORQUE</tt> statement or a joint definition statement. If not, the <tt>DATA TORQUE</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA TORQUE</tt> statement is encountered using the same _name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The units for a _torque_ are length force if the _name_ refers to a <tt>TORQUE</tt> statement. If the _name_ refers to a joint, then units of force are used for a translational joint variable _torque_ and units of length force are used for a rotational joint variable _torque_.
# The sign of the _torque_ value must be consistent with the order of the point names specified in the <tt>TORQUE</tt> statement. A _torque_ value applied within a joint is considered positive if it tends to change the value of the joint variable in the positive sense.
# The numeric value of a _torque_ may be substituted for by the alphanumeric name of a previously defined <tt>VALUE</tt> expression.
# The keyword <tt>NONE</tt> may be used in place of a _torque_ for a joint variable for which no externally applied torque is intended.


## The <tt>DATA CONTACT</tt> Statement ##
The <tt>DATA CONTACT</tt> statement is used to specify the properties of a pair of contacting solids
defined by a <tt>CONTACT</tt> statement.

### Format ###
> DATA CONTACT (contact name) = e<sub>n</sub>, e<sub>t</sub>, e<sub>b</sub>, e<sub>r</sub>, mu

where _contact name_ is the alphanumeric name of a previously defined contact, _e_<sub>n</sub>, e<sub>t</sub>,
and e<sub>b</sub>_are the coefficients of restitution in the normal, tangential, and binormal directions,
respectively,_e<sub>r</sub>_is the torsional coefficient of restitution, and_mu_is the
coefficient of Coulomb friction, all taken with respect to the impacting surfaces of the contact._

### Examples ###
> DATA CONTACT (HIT) = 0.9, -1.0, 0.0, -1.0, 0.25

specifies that a <tt>CONTACT</tt> named <tt>HIT</tt> has coefficients of restitution of 0.9, -1.0, 0.0, and -1.0 in the normal, tangential, binormal, and torsional directions, respectively, and a coefficient of Coulomb friction of 0.25 units.

### Notes ###
# There may be a <tt>DATA CONTACT</tt> statement for each contact defined by a <tt>CONTACT</tt> statement. If these do not appear before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement, any contacts without such data are given default data of e<sub>n</sub>=0.0, e<sub>t</sub>=0.0, e<sub>bi</sub>=-1.0, e<sub>mn</sub>=0.0, and mu=0.0; no message is printed.
# <tt>DATA CONTACT</tt> statements need not be given for all contacts but may be used for as many or as few as desired.
# The _contact name_ specified must have been defined by a previous <tt>CONTACT</tt> statement. If not, the <tt>DATA CONTACT</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA CONTACT</tt> statement is encountered using the same _contact name_, the later statement takes precedence; earlier data are replaced; no message is printed.
# The numeric values of the coefficients of restitution are unity for purely elastic (no loss of relative velocity on rebound) and zero for plastic (total loss of relative velocity with no rebound); the values are positive for a direction reversal and negative for no direction reversal of the relative velocity during impact.
# The coefficient of Coulomb friction _mu_ is always non-negative, but may be zero.
# Which of the five coefficients are used for a given _contact name_ depend on the settings of the _impact models_ specified by the most recent <tt>IMPACT</tt> statement at the time that an <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is encountered.


## The <tt>DATA POSITION</tt> Statement ##
The <tt>DATA POSITION</tt> statement designates a single degree of freedom joint as a position input
(<tt>SGC</tt>) for the system in the kinematic or static mode and specifies the initial position, increment
size, and number of increments for its joint variable during the simulation.

### Format ###
> DATA POSITION (joint name) = position, increment, n steps

where _joint name_ is the alphanumeric name of the <tt>REVOLUTE</tt> or <tt>PRISM</tt> or <tt>XPIN</tt> or <tt>YPIN</tt> or
<tt>ZPIN</tt> or <tt>XSLIDE</tt> or <tt>YSLIDE</tt> or <tt>ZSLIDE</tt> or <tt>GEAR</tt> or <tt>BEVEL</tt> or <tt>RACK</tt> or <tt>SCREW</tt> joint being
designated as an <tt>SGC</tt>, _position_ is the numeric value of the joint variable at the first
position to be simulated, _increment_ is the numeric value of the increment to be made in that
joint variable value for each print, and _n steps_ is the integer number of increments to be made
in that joint variable during the simulation.

### Examples ###
> DATA POSITION (PIN) = -90.0, 15.0, 24

specifies that the previously defined <tt>REVOLUTE</tt> joint named PIN is an <tt>SGC</tt> for the system and is
to be incremented from -90° to 270° in equal steps of 15° each.

> DATA POSITION (SLIP) = 1.75

specifies that the <tt>PRISM</tt> joint named <tt>SLIP</tt> is an <tt>SGC</tt> for the system and its joint variable is
held stationary at a value of 1.75 length units throughout the simulation.

### Notes ###
# The <tt>DATA POSITION</tt> statement may not be used after a <tt>FIND DYNAMICS</tt> statement (dynamic mode). If this is attempted, the <tt>DATA POSITION</tt> statement is ignored and a message is printed.
# The <tt>DATA POSITION</tt> statement is optional; it may be used along with the <tt>DATA MOTION</tt> statement for as few or as many joints as desired up to the number of degrees of freedom of the system.
# If more <tt>DATA POSITION</tt> and/or <tt>DATA MOTION</tt> statements are specified than there are degrees of freedom in the system, no error is detected immediately. During the simulation, however, a diagnostic message will occur unless the _position_ data are all specified (with extreme precision) consistent with a configuration for which the system can be assembled. Difficulty will certainly result upon incrementing to a new position.
# If less <tt>DATA POSITION</tt> and/or <tt>DATA MOTION</tt> statements are specified than the number of degrees of freedom of the system, additional joint variables are selected as free generalized coordinates (<tt>FGC</tt>s) by the IMP system.
# If a <tt>FIND EQUILIBRIUM</tt> statement is encountered before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement (static mode), then any <tt>FGC</tt> positions are varied to move the system to a position of static equilibrium. If not (kinematic mode), then no control is exerted over the values of the <tt>FGC</tt>s; they usually retain their original positions.
# The _joint name_ specified must be defined by a previous statement defining a single degree of freedom joint. If not, the <tt>DATA POSITION</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement is encountered referring to the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# If only a single _position_ of a particular joint variable is intended, the values of _increment_ and _n steps_ need not be specified; when not specified _increment_ and _n steps_ are treated as zero.
# If the value of _increment_ is given as zero, then _n steps_ is also treated as zero.
# The units of _position_ and _increment_ are degrees for a rotational joint or length units for a sliding joint.
# The sign of the _position_ and _increment_ values must be consistent with the sign convention of the joint variable (see statement defining the joint).
# If an <tt>SGC</tt> joint variable value is set to or incremented to a position which cannot be achieved by the system model, this position is ignored and the simulation is continued at the next position; a message is printed.
# When a _position_ is specified for a joint variable by a <tt>DATA POSITION</tt> statement, it is assumed to have zero velocity and zero acceleration until otherwise specified by a <tt>DATA VELOCITY</tt> or <tt>DATA ACCEL</tt> statement.
# The starting position specification need not be the design position, but should not be too far away from it.
# When a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement is used to set a particular joint variable to a specified position, this implies that sufficient force or torque is applied at that joint variable to achieve that position even though no <tt>DATA FORCE</tt> or <tt>DATA TORQUE</tt> statement has been given.


## The <tt>DATA VELOCITY</tt> Statement ##
The <tt>DATA VELOCITY</tt> statement specifies the velocity of a joint variable which was specified as an
<tt>SGC</tt> by a previous <tt>DATA POSITION</tt> statement.

### Format ###
> DATA VELOCITY (joint name) = velocity

where _joint name_ is the alphanumeric name of a joint which was previously designated in a
<tt>DATA POSITION</tt> statement, and _velocity_ is the numeric value of the joint variable velocity for
that joint.

### Example ###
> DATA VELOCITY (PIN) = -188.5

specifies that velocity of the pinned joint named PIN is -188.5 radians per second (1800 rpm) clockwise.

### Notes ###
# A <tt>DATA VELOCITY</tt> statement may not be used after a <tt>FIND EQUILIBRIUM</tt> statement (static mode) or a <tt>FIND DYNAMICS</tt> statement (dynamic mode). If this is attempted, the <tt>DATA VELOCITY</tt> statement is ignored and a message is printed.
# The _joint name_ specified must have been defined as an <tt>SGC</tt> by a previous <tt>DATA POSITION</tt> statement referring to the same _joint name_. If not, the <tt>DATA VELOCITY</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA VELOCITY</tt> statement is encountered referring to the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# Not every <tt>SGC</tt> designated by a <tt>DATA POSITION</tt> statement need be given a velocity. Those not given velocities by <tt>DATA VELOCITY</tt> statements are treated as having zero _velocities_.
# If more than one position of the system is simulated, the _velocity_ specified is the same for all positions even though a <tt>DATA ACCEL</tt> statement may be given.
# The units of _velocity_ are radians per second for a rotational joint or length units per second for a sliding joint.
# The sign of the _velocity_ must be consistent with the sign convention for the joint variable (see statement defining the joint).


## The <tt>DATA ACCEL</tt> Statement ##
The <tt>DATA ACCEL</tt> statement specifies the acceleration of a joint variable which was specified as an
<tt>SGC</tt> by a previous <tt>DATA POSITION</tt> statement.

### Format ###
> DATA ACCEL (joint name) = acceleration

where _joint name_ is the alphanumeric name of a joint which was previously designated in a
<tt>DATA POSITION</tt> statement, and _acceleration_ is the numeric value of the joint variable
acceleration for that joint.

### Example ###
> DATA ACCEL (PIN) = 50.0

specifies that acceleration of the <tt>SGC</tt> revolute joint named <tt>PIN</tt> is 50.0 radians per second per
second.

### Notes ###
# A <tt>DATA ACCEL</tt> statement may not be used after a <tt>FIND EQUILIBRIUM</tt> statement (static mode) or a <tt>FIND DYNAMICS</tt> statement (dynamic mode). If this is attempted, the <tt>DATA ACCEL</tt> statement is ignored and a message is printed.
# The _joint name_ specified must be defined as an <tt>SGC</tt> by a previous <tt>DATA POSITION</tt> statement referring to the same _joint name_. If not, the <tt>DATA ACCEL</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA ACCEL</tt> statement is encountered referring to the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# Not every <tt>SGC</tt> designated by a <tt>DATA POSITION</tt> statement need be given acceleration. Those not given acceleration by <tt>DATA ACCEL</tt> statements are treated as having zero acceleration.
# If more than one position of the system is simulated, the _acceleration_ specified is the same for all positions.
# The units of _acceleration_ are radians per second per second for a rotating joint or length units per second per second for a sliding joint.
# The sign of the _acceleration_ must be consistent with the sign convention for the joint variable joint (see statement defining the joint).


## The <tt>DATA MOTION</tt> Statement ##
The <tt>DATA MOTION</tt> statement designates one or more joint variables as motion input(s),(<tt>SGC</tt>s), for
the system and specifies their motion(s).

### Format ###
> DATA MOTION (joint name) = position, position, ...

where _joint name_ is the alphanumeric name of the joint whose joint variables are to be motion
inputs (<tt>SGC</tt>s). There is one _position_ value specified for each joint variable in order; each
_position_ is a numeric value or the alphanumeric name of a <tt>VALUE</tt> expression specifying the
position of that joint variable.

### Examples ###
> DATA MOTION (PIN) = -90.0

specifies that the previously defined <tt>REVOLUTE</tt> joint named <tt>PIN</tt> is held stationary, with its
joint variable value set to -90° throughout the simulation.

> DATA MOTION (SLIP) = RAMP

specifies that the <tt>PRISM</tt> joint named <tt>SLIP</tt> is an <tt>SGC</tt>; its motion is defined by a previous
<tt>VALUE</tt> expression named <tt>RAMP</tt> (see note 8).

> <tt>DATA MOTION</tt> (CYL) = 30.0, <tt>NONE</tt>

specifies that, in the cylindric joint named CYL, the rotational joint variable is held stationary
at a value of 30.0E; the translational joint variable is not an <tt>SGC</tt> (see note 9).

### Notes ###
# The <tt>DATA MOTION</tt> statement is optional; it may be used along with <tt>DATA POSITION</tt> or <tt>DATA</tt> IC statements for as few or as many joint variables as desired up to the number of degrees of freedom of the system.
# If more <tt>DATA MOTION</tt>, <tt>DATA POSITION</tt>, and/or <tt>DATA</tt> IC statements are specified than allowed by the degree of freedom of the system, no error is detected immediately. During the simulation, however, a diagnostic message will occur unless the _position_ data are all specified (with extreme precision) consistent with a configuration for which the system can be assembled. Difficulty will certainly result upon attempting to increment to a new position.
# If <tt>DATA MOTION</tt>, <tt>DATA POSITION</tt>, and/or <tt>DATA</tt> IC statements are specified for less joint variables than the degrees of freedom of the system, additional joint variables are selected as free generalized coordinates (<tt>FGC</tt>s) by the IMP system.
# The _joint name_ specified must be defined by a previous statement defining a joint. If not, the <tt>DATA MOTION</tt> statement is ignored and a message is printed.
# If more than one <tt>DATA MOTION</tt>, <tt>DATA POSITION</tt>, or <tt>DATA IC</tt> statement is encountered referring to the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The units of each _position_ value depend on the nature of the joint variable; degrees are used for each rotational joint variable (also see note 8) and length units for each translational joint variable.
# The sign of each _position_ value must be consistent with the sign convention for the corresponding joint variable (see joint definition statement).
# The numeric value of any _position_ may be substituted for by the alphanumeric name of a previously defined <tt>VALUE</tt> expression. In such a case, however, the units of a rotational joint variable <tt>VALUE</tt> expression must be radians.
# The keyword <tt>NONE</tt> may be used in place of any _position_ value for a joint variable which is not intended as an <tt>SGC</tt>.
# If a numeric value is used for _position_, the velocity and acceleration of the corresponding joint variable are assumed to be zero. When a <tt>VALUE</tt> expression name is used for _position_, proper derivative values are used to provide the corresponding velocity and acceleration. Note, however, that <tt>VALUE</tt> expressions using the <tt>VELOCITY</tt>, <tt>ACCELERATION</tt>, or <tt>FORCE</tt> functions may return undefined values for the derivatives. Undefined values are treated as zeroes in their use in the <tt>DATA MOTION</tt> statement.
# When a <tt>DATA MOTION</tt> statement is used, this implies that sufficient force or torque is applied at each joint variable to achieve the specified motion even though no <tt>DATA FORCE</tt> or <tt>DATA TORQUE</tt> statement has been given.


## The <tt>DATA IC</tt> Statement ##
The <tt>DATA IC</tt> statement specifies the initial positions and velocities of the joint variables of a
designated joint for the start of a dynamic mode simulation.

### Format ###
> <tt>DATA IC</tt> (joint name)=position,velocity;position,velocity;...

where _joint name_ is the alphanumeric name of the joint whose initial conditions are specified.
Each _position_ and _velocity_ pair are the numeric values for the initial position and velocity
of one joint variable; there is one _position,velocity_ pair of values specified for each joint
variable in order.

### Examples ###
> DATA IC (PIN) = -90, 12.566

specifies that the initial conditions for the pinned joint named <tt>PIN</tt> for a dynamic mode simulation
are to have its joint variable set to -90° with an initial velocity of 12.566 radians per second
(2 Hz).

> DATA IC (SLIP) = POS VEL

specifies that the dynamic mode simulation will begin with initial conditions for the sliding joint
named <tt>SLIP</tt> defined by previous value expressions named <tt>POS</tt> and <tt>VEL</tt> (see note 9).

> DATA IC (CYL) = 30,12.566; NONE, NONE

specifies that, for the cylindric joint named <tt>CYL</tt>, the rotational joint variable has initial
conditions of 30° and 12.566 radians per second, while the translational joint variable has no
initial conditions specified (see note 10).

### Notes ###
# The <tt>DATA IC</tt> statement must be preceded by a <tt>FIND DYNAMICS</tt> statement (dynamic mode); if not, the statement is ignored and a message is printed.
# The <tt>DATA IC</tt> statement is optional; it may be used along with the <tt>DATA MOTION</tt> statement for as few or many joint variables as desired up to the number of degrees of freedom of the system.
# If more <tt>DATA MOTION</tt> and <tt>DATA IC</tt> statements are specified than allowed by the degree of freedom of the system, no error is detected immediately. During the simulation, however, a diagnostic message will occur unless the _position_ data are all specified (with extreme precision) consistent with a configuration for which the system can be assembled. Difficulty will certainly result upon attempting to increment to a new position.
# If <tt>DATA MOTION</tt> and <tt>DATA IC</tt> statements are specified for less joint variables than the degree of freedom of the system, additional joint variables are selected as free generalized coordinates (<tt>FGC</tt>s) by the IMP system. The initial conditions for these additional <tt>FGC</tt>s are determined by IMP; the initial velocities of these additional <tt>FGC</tt>s are assumed zero.
# The _name_ specified must be defined by a previous statement defining a joint. If not, the <tt>DATA</tt> IC statement is ignored and a message is printed.
# If more than one <tt>DATA IC</tt> or <tt>DATA MOTION</tt> statement is encountered referring to the same _joint name_, the later statement takes precedence; earlier data are replaced and a message is printed.
# The units of each _position_ and each _velocity_ value depend upon the nature of each joint variable. For rotational joint variables, the units of _position_ are degrees (also see note 9), and the units of _velocity_ are radians per second; for each translational joint variable, each _position_ has units of length, while each _velocity_ has units of length per second.
# The sign of each _position_ and each _velocity_ value must be consistent with the sign convention for the corresponding joint variable (see joint definition statement).
# The numeric value of any _position_ or any _velocity_ may be substituted for by the alphanumeric name of a previously defined <tt>VALUE</tt> expression. In such a case, however, the units of a rotational joint variable _position_ value must be radians.
# The keyword <tt>NONE</tt> may be used in place of any _position_ and _velocity_ value for a joint variable for which initial conditions are not intended to be specified. When <tt>NONE</tt> is used for either the _position_ or the _velocity_ of a joint variable, the other value for the same joint variable is also treated as <tt>NONE</tt>.