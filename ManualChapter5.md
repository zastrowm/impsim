# Chapter 5: Request Statements #
The various request statements recognized by the IMP interpreter are presented in this chapter. Request statements are used to define the types of analyses to be performed and the particular quantities which are desired in the output. The first word of each request statement is one of the keywords <tt>PRINT</tt>, <tt>LIST</tt>, or <tt>STORE</tt>, and instructs the IMP system to interpret the remainder of the statement according to one of the formats on the following pages.

## The <tt>PRINT VALUE</tt> Statement ##
The <tt>PRINT VALUE</tt> statement requests that the values and time derivatives of specified <tt>VALUE</tt> expressions be printed for each position simulated.

### Format ###
> PRINT VALUE (name, name, ... )

where each _name_ is the alphanumeric name of a <tt>VALUE</tt> expression whose value and derivatives are to be printed.

### Example ###
> PRINT VALUE (F1, F2, WAVE, DX)

requests that previously defined <tt>VALUE</tt> expressions named <tt>F1</tt>, <tt>F2</tt>, <tt>WAVE</tt>, and <tt>DX</tt> and their time derivatives be printed at each position simulated.

### Notes ###
# Each _name_ must be defined in a <tt>VALUE</tt> statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; if not, each undefined <tt>VALUE</tt> _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>PRINT VALUE</tt> statement.
# If more than one <tt>PRINT VALUE</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that all <tt>VALUE</tt> names be included among those printed.
# The numeric value and the first and second time derivatives are printed for each _name_ as each position of the system is simulated; they are printed in the order given.
# For any _name_ whose value or derivatives cannot be calculated at a certain position, the undefined information is printed as "????"


## The <tt>LIST VALUE</tt> Statement ##
The <tt>LIST VALUE</tt> statement requests that the values and time derivatives of specified <tt>VALUE</tt> expressions be tabularly listed for all positions simulated.

### Format ###
> LIST VALUE (name, name, ... )

where each _name_ is the alphanumeric name of a <tt>VALUE</tt> expression whose value and derivatives are to be tabularly listed.

### Example ###
> LIST VALUE (F1, F2, WAVE, DX)

requests that previously defined <tt>VALUE</tt> expressions named <tt>F1</tt>, <tt>F2</tt>, <tt>WAVE</tt>, and <tt>DX</tt> and their time derivatives are to be tabularly listed for all positions simulated.

### Notes ###
# Each _name_ must be defined in a <tt>VALUE</tt> statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; if not, each undefined <tt>VALUE</tt> _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>LIST VALUE</tt> statement.
# If more than one <tt>LIST VALUE</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that all <tt>VALUE</tt> statements be included among those tabularly listed.
# The numeric values and first and second time derivatives for all _names_ are saved until the end of the simulation; they are then sorted and tabularly listed for all positions in the order given.
# For any _name_ whose value or derivatives cannot be calculated at a certain position, the undefined information is listed as "????".


## The <tt>STORE VALUE</tt> Statement ##
The <tt>STORE VALUE</tt> statement requests that the values and time derivatives of specified <tt>VALUE</tt> expressions be stored in a file for all positions simulated.

### Format ###
> STORE VALUE (name, name, ... )

where each _name_ is the alphanumeric name of a <tt>VALUE</tt> expression whose value and derivatives are to be stored.

### Example ###
> STORE VALUE (F1, F2, WAVE, DX)

requests that previously defined <tt>VALUE</tt> expressions named <tt>F1</tt>, <tt>F2</tt>, <tt>WAVE</tt>, and <tt>DX</tt> and their time derivatives are to be stored on a file for all positions simulated.

### Notes ###
# Each _name_ must be defined by a <tt>VALUE</tt> statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is given; if not, each undefined <tt>VALUE</tt> _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>STORE VALUE</tt> statement.
# If more than one <tt>STORE VALUE</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that all <tt>VALUE</tt> statements be included among those stored.
# For any _name_ whose value or derivatives cannot be calculated at a certain position, the value "0.000002" is stored.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests are output. Subsequent <tt>STORE</tt> requests are output to the same file.


## The <tt>PRINT HEADING</tt> Statement ##
The <tt>PRINT HEADING</tt> statement requests that the values of the generalized coordinates (SGCs and FGCs) be printed as each position issimulated.

### Format ###
> PRINT HEADING

### Notes ###
# When <tt>PRINT HEADING</tt> has been specified, the values of the SGCs are printed as they are incremented to each new position. Once the system has been successfully assembled at the new position and the degrees of freedom of the system have been determined, the values of any FGCs chosen by IMP are also printed.
# For each SGC or FGC, the values of position, velocity, and acceleration are printed.


## The <tt>STORE HEADING</tt> Statement ##
The <tt>STORE HEADING</tt> statement requests that the values of the generalized coordinates (SGCs and FGCs) be stored on a file for all positions simulated.

### Format ###
> STORE HEADING

### Notes ###
# When <tt>STORE HEADING</tt> has been specified, the values of the SGCs are stored as they are incremented to each new position. Once the system has been successfully assembled at the new position and the degrees of freedom of the system have been determined, the values of any FGCs chosen by IMP are also stored.
# For each SGC or FGC, the values of position, velocity, and acceleration are stored.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests are output. Subsequent <tt>STORE</tt> requests are output to the same file.


## The <tt>PRINT POSITION</tt> Statement ##
The <tt>PRINT POSITION</tt> statement requests that the positions of specified joints, points, springs, dampers, and links be printed for each position simulated.

### Format ###
> PRINT POSITION (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose position is to be printed.

### Example ###
> PRINT POSITION (PIN, PT1, BALL, PT5, SLIP)

requests that the positions of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute position coordinates of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the position of the damper named <tt>SLIP</tt> be printed for each position simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>PRINT POSITION</tt> statement.
# If more than one <tt>PRINT POSITION</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the positions of all joints, points, springs, and dampers, but not links, be included among those printed.
# The position data for each _name_ are printed as each position of the system is simulated; they are printed in the order given.
# The dimensions of the position data printed are degrees or length units as appropriate.
# If _name_ refers to a joint, both the relative position of the joint variable(s) and the global coordinates of the origin of the first local coordinate system at that joint are printed. The signs of the joint variable positions printed are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global coordinates of that point are printed.
# If _name_ refers to a spring or damper, the absolute length and the global components of the vector between the two endpoints are printed. The signs of the vector components are taken from the first endpoint toward the second.
# If _name_ refers to a link, the (4x4) transformation matrix T for the local coordinate system of that link relative to the global frame of reference is printed.
> |X|           |x|
> |Y|       = T |y|
> |Z|           |z|
> |1|global     |1|local


## The <tt>LIST POSITION</tt> Statement ##
The <tt>LIST POSITION</tt> statement requests that the positions of specified joints, points, springs, dampers and links be tabularly listed for all positions simulated.

### Format ###
> LIST POSITION (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose position is to be tabularly listed.

### Example ###
> LIST POSITION (PIN, PT1, BALL, PT5, SLIP)

requests that the positions of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute position coordinates of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the position of the damper named <tt>SLIP</tt> be tabularly listed for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>LIST POSITION</tt> statement.
# If more than one <tt>LIST POSITION</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the positions of all joints, points, springs, and dampers, but not links be included among those tabularly listed.
# The position data for all _names_ are saved until the end of the simulation; they are then sorted and listed for all positions in the order given.
# The dimensions of the position data listed are degrees or length units as appropriate.
# If _name_ refers to a joint, the relative positions of the joint variables are tabularly listed. The signs of the joint variable positions listed are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global coordinates of that point are tabularly listed.
# If _name_ refers to a spring or damper, the absolute length is tabularly listed.
# If _name_ refers to a link, the (4x4) transformation matrix T for the local coordinate systems of that link relative to the global frame of reference is listed.
> |X|           |x|
> |Y|       = T |y|
> |Z|           |z|
> |1|global     |1|local


## The <tt>STORE POSITION</tt> Statement ##
The <tt>STORE POSITION</tt> statement requests that the positions of specified joints, points, springs, dampers, and links be stored on a file for all positions simulated.

### Format ###
> STORE POSITION (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose position is to be stored.

### Example ###
> STORE POSITION (PIN, PT1, BALL, PT5, SLIP)

requests that the positions of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute position coordinates of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the position of the damper named<tt>SLIP</tt> be stored on a file for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>STORE POSITION</tt> statement.
# If more than one <tt>STORE POSITION</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the positions of all joints, points, springs, and dampers, but not links, be included among those stored.
# The dimensions of the position data stored are degrees or length units as appropriate.
# If _name_ refers to a joint, the relative positions of the joint variables are stored. The signs of the joint variable positions stored are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global coordinates of that point are stored.
# If _name_ refers to a spring or damper, the global components of the vector between the two endpoints are stored. The signs of the vector components are taken from the first endpoint toward the second.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests are output. Subsequent <tt>STORE</tt> requests are output to the same file.
# If _name_ refers to a link, the (4x4) transformation matrix T for the local coordinate systems of that link relative to the global frame of reference is stored.
> |X|           |x|
> |Y|       = T |y|
> |Z|           |z|
> |1|global     |1|local


## The <tt>PRINT VELOCITY</tt> Statement ##
The <tt>PRINT VELOCITY</tt> statement requests that the velocities of specified joints, points, springs, dampers, and links be printed for each position simulated.

### Format ###
> PRINT VELOCITY (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose velocity is to be printed.

### Example ###
> PRINT VELOCITY (PIN, PT1, BALL, PT5, SLIP)

requests that the velocities of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute velocities of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the relative velocity across the damper named <tt>SLIP</tt> be printed for each position simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>PRINT VELOCITY</tt> statement.
# If more than one <tt>PRINT VELOCITY</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the velocities of all joints, points, springs, and dampers, but not links, be included among those printed.
# The velocity data for each _name_ are printed as each position of the system is simulated; they are printed in the order given.
# The dimensions of the velocity data printed are radians per second or length units per second as appropriate.
# If _name_ refers to a joint, the relative velocities of the joint variables are printed. The signs of the joint variable velocities printed are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global components of the absolute velocity vector for that point are printed.
# If _name_ refers to a spring or damper, the magnitude of the relative velocity along that spring or damper is printed.
# If _name_ refers to a link, the global components of the angular velocity of that link are printed. Also printed are the global components of the absolute velocity of a point attached to that link and instantaneously located at the global origin.


## The <tt>LIST VELOCITY</tt> Statement ##
The <tt>LIST VELOCITY</tt> statement requests that the velocities of specified joints, points, springs, dampers, and links be tabularly listed for all positions simulated.

### Format ###
> LIST VELOCITY (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose velocity is to be tabularly listed.

### Example ###
> LIST VELOCITY (PIN, PT1, BALL, PT5, SLIP)

requests that the velocities of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute velocities of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the relative velocity across the damper named <tt>SLIP</tt> be tabularly listed for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>LIST VELOCITY</tt> statement.
# If more than one <tt>LIST VELOCITY</tt> statement is encountered, the lists of _names_ are concatenated, including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the velocities of all joints, points, springs, and dampers, but not links, be included among those tabularly listed.
# The velocity data for all _names_ are saved until the end of the simulation; they are then sorted and listed for all positions in the order given.
# The dimensions of the velocity data listed are radians per second or length units per second as appropriate.
# If _name_ refers to a joint, the relative velocities of the joint variables are tabularly listed. The signs of the joint variable velocities listed are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global components of the absolute velocity vector for that point are tabularly listed.
# If _name_ refers to a spring or damper, the magnitude of the relative velocity along the spring or damper is tabularly listed.
# If _name_ refers to a link, the global components of the angular velocity of that link are listed. Also listed are the global components of the absolute velocity of a point attached to that link and instantaneously located at the global origin.


## The <tt>STORE VELOCITY</tt> Statement ##
The <tt>STORE VELOCITY</tt> statement requests that the velocities of specified joints, points, springs, dampers, and links be stored on a file for all positions simulated.

### Format ###
> STORE VELOCITY (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose velocity is to be stored.

### Example ###
> STORE VELOCITY (PIN, PT1, BALL, PT5, SLIP)

requests that the velocities of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute velocities of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the relative velocity across the damper named <tt>SLIP</tt> be stored on a file for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>STORE VELOCITY</tt> statement.
# If more than one <tt>STORE VELOCITY</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the velocities of all joints, points, springs, and dampers, but not links, be included among those stored.
# The dimensions of the velocity data stored are radians per second or length units per second as appropriate.
# If _name_ refers to a joint, the relative velocities of the joint variables are stored. The signs of the joint variable velocities stored are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global components of the absolute velocity vector for that point are stored.
# If _name_ refers to a spring or damper, the magnitude of the relative velocity along the spring or damper is stored.
# If _name_ refers to a link, the global components of the angular velocity of that link are stored. Also stored are the global components of the absolute velocity of a point attached to that link and instantaneously located at the global origin.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests, are output. Subsequent <tt>STORE</tt> requests are output to the same file.


## The <tt>PRINT ACCEL</tt> Statement ##
The <tt>PRINT ACCEL</tt> statement requests that the accelerations of specified joints, points, springs, dampers, and links be printed for each position simulated.

### Format ###
> PRINT ACCEL (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose acceleration is to be printed.

### Example ###
> PRINT ACCEL (PIN, PT1, BALL, PT5, SLIP)

requests that the accelerations of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute accelerations of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the relative acceleration across the damper named <tt>SLIP</tt> be printed for each position simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>PRINT ACCEL</tt> statement.
# If more than one <tt>PRINT ACCEL</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a "name is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the accelerations of all joints, points, springs, and dampers but not links be included among those printed.
# The acceleration data for each _name_ are printed as each position of the system is simulated; they are printed in the order given.
# The dimensions of the acceleration data printed are radians per second per second or length units per second per second as appropriate.
# If _name_ refers to a joint, the relative accelerations of the joint variables are printed. The signs of the joint variable accelerations printed are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global components of the absolute acceleration vector for that point are printed.
# If _name_ refers to a spring or damper, the magnitude of the relative acceleration along that spring or damper is printed.
# If _name_ refers to a link, the global components of the angular acceleration of that link are printed. Also printed are the global components of the absolute tangential acceleration of a point attached to that link and instantaneously located at the global origin.


## The <tt>LIST ACCEL</tt> Statement ##
The <tt>LIST ACCEL</tt> statement requests that the accelerations of specified joints, points, springs, dampers, and links be tabularly listed for all positions simulated.

### Format ###
> LIST ACCEL (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose acceleration is to be tabularly listed.

### Example ###
> LIST ACCEL (PIN, PT1, BALL, PT5, SLIP)

requests that the accelerations of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute accelerations of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the relative acceleration across the damper named <tt>SLIP</tt> be tabularly listed for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>LIST ACCEL</tt> statement.
# If more than one <tt>LIST ACCEL</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the accelerations of all joints, points, springs, and dampers, but not links be included among those tabularly listed.
# The acceleration data for all _names_ are saved until the end of the simulation; they are then sorted and listed for all positions in the order given.
# The dimensions of the acceleration data listed are radians per second per second or length units per second per second as appropriate.
# If _name_ refers to a joint, the relative accelerations of the joint variables are tabularly listed. The signs of the joint variable accelerations listed are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global components of the absolute acceleration vector for that point are tabularly listed.
# If _name_ refers to a spring or damper, the magnitude of the relative acceleration along that spring or damper is tabularly listed.
# If _name_ refers to a link, the global components of the angular acceleration of that link are listed. Also listed are the global components of the absolute tangential acceleration of a point attached to that link and instantaneously located at the global origin.


## The <tt>STORE ACCEL</tt> Statement ##
The <tt>STORE ACCEL</tt> statement requests that the accelerations of specified joints, points, springs, dampers, and links be stored on a file for all positions simulated.

### Format ###
> STORE ACCEL (name, name, ... )

where each _name_ is the alphanumeric name of a joint, point, spring, damper, or link whose acceleration is to be stored.

### Example ###
> STORE ACCEL (PIN, PT1, BALL, PT5, SLIP)

requests that the accelerations of the joint variables of the joints named <tt>PIN</tt> and <tt>BALL</tt>, the absolute accelerations of the points named <tt>PT1</tt> and <tt>PT5</tt>, and the relative acceleration across the damper named <tt>SLIP</tt> be stored on a file for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>POINT</tt> statement, a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, a <tt>LINK</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>STORE ACCEL</tt> statement.
# If more than one <tt>STORE ACCEL</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the accelerations of all joints, points, springs, and dampers but not links be included among those stored.
# The dimensions of the acceleration data stored are radians per second per second or length units per second per second as appropriate.
# If _name_ refers to a joint, the relative accelerations of the joint variables are stored. The signs of the joint variable accelerations stored are consistent with the joint variable definitions (see appropriate joint definition statement).
# If _name_ refers to a point, the global components of the absolute acceleration vector for that point are stored.
# If _name_ refers to a spring or damper, the magnitude of the relative acceleration along that spring or damper is stored.
# If _name_ refers to a link, the global components of the angular acceleration of that link are stored. Also stored are the global components of the absolute tangential acceleration of a point attached to that link and instantaneously located at the global origin.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests are output. Subsequent <tt>STORE</tt> requests are output to the same file.


## The <tt>PRINT FORCE</tt> Statement ##
The <tt>PRINT FORCE</tt> statement requests that the constraint forces and torques acting within specified joints, springs, and dampers be printed for all positions simulated.

### Format ###
> PRINT FORCE (name, name, ... )

where each _name_ is the alphanumeric name of a joint, spring, or damper for which the constraint force and torque components are to be printed.

### Example ###
> PRINT FORCE (PIN, PULL, SLOW)

requests that the constraint force and torque components within the joint named <tt>PIN</tt> and the forces transmitted through the spring named <tt>PULL</tt> and the damper named <tt>SLOW</tt> be printed for each position simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>PRINT FORCE</tt> statement.
# If more than one <tt>PRINT FORCE</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the constraint forces in all joints, springs, and dampers be included among those printed.
# The force data for each _name_ are printed as each position of the system is simulated; they are printed in the order given.
# The constraint force and torque components printed include all static and dynamic effects consistent with the current model and the instantaneous operating conditions at the time of printing. For example, if <tt>DATA GRAVITY</tt> and <tt>DATA MASS</tt> statements have been given, the static forces due to the weights of the links are included; if <tt>DATA MOTION</tt> statements are also given, the dynamic forces are also included.
# Force data are printed in force units and torque data are printed in units of length force.
# The constraint force and torque components printed must be interpreted according to the statements which defined the joint and its data. If, for example, the constraint forces and torques are requested for a joint defined by the statement <pre>ZPIN (LK1, LK2) = PIN</pre> then the force and torque components printed are those exerted by link <tt>LK</tt>1 onto link <tt>LK</tt>2. Three components of force and three components of torque are printed; they are the components along and about the axes of the local coordinate system attached to link <tt>LK</tt>2 at the joint <tt>PIN</tt>.
# The force components within a joint are considered positive when in the same direction as the positive local coordinate axes. The torque components are considered positive when counterclockwise as seen from the positive ends of the local coordinate axes.
# A single force is printed for a spring or damper; it is positive if the spring or damper is in tension.
# Any statically indeterminate force or torque component is printed as "????" and is treated as zero. Such statically indeterminate components are not necessarily zero (for example, if the system is assembled under preload), but are not possible to evaluate in a rigid body simulation.


## The <tt>LIST FORCE</tt> Statement ##
The <tt>LIST FORCE</tt> statement requests that the constraint forces and torques acting within specified joints, springs, and dampers be tabularly listed for all positions simulated.

### Format ###
> LIST FORCE (name, name, ... )

where each _name_ is the alphanumeric name of a joint, spring, or damper for which the constraint force and torque components are to be tabularly listed.

### Example ###
> LIST FORCE (PIN, PULL, SLOW)

requests that the constraint force and torque components within the joint named <tt>PIN</tt> and the forces transmitted through the spring named <tt>PULL</tt> and the damper named <tt>SLOW</tt> be tabularly listed for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>LIST FORCE</tt> statement.
# If more than one <tt>LIST FORCE</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the constraint forces in all joints, springs, and dampers be included among those tabularly listed.
# The force data for all _names_ are saved until the end of the simulation; they are then sorted and listed for all positions in the order given.
# The constraint force and torque components listed include all static and dynamic effects consistent with the current model and the instantaneous operating conditions at the time of listing. For example, if <tt>DATA GRAVITY</tt> and <tt>DATA MASS</tt> statements have been given, the static forces due to the weights of the links are included; if <tt>DATA MOTION</tt> statements are also given, the dynamic forces are also included.
# Force data are listed in force units and torque data are listed in units of length force.
# The constraint force and torque components listed must be interpreted according to the statements which defined the joint and its data. If, for example, the constraint forces and torques are requested for a joint defined by the statement <pre>ZPIN (LK1, LK2) = PIN</pre> then the force and torque components listed are those exerted by link <tt>LK</tt>1 onto link <tt>LK</tt>2. Three components of force and three components of torque are listed; they are the components along and about the axes of the local coordinate system attached to link <tt>LK</tt>2 at the joint <tt>PIN</tt>.
# The force components within a joint are considered positive when in the same direction as the positive local coordinate The torque components are considered positive when axes. counterclockwise as seen from the positive ends of the local coordinate axes.
# A single force is listed for a spring or damper; it is positive if the spring or damper is in tension.
# Any statically indeterminate force or torque component is listed as "????" and is treated as zero. Such statically indeterminate components are not necessarily zero (for example, if the system is assembled under preload), but are not possible to evaluate in a rigid body simulation.


## The <tt>STORE FORCE</tt> Statement ##
The <tt>STORE FORCE</tt> statement requests that the constraint forces and torques acting within specified joints, springs, and dampers be stored on a file for all positions simulated.

### Format ###
> STORE FORCE (name, name, ... )

where each _name_ is the alphanumeric name of a joint, spring, or damper for which the constraint force and torque components are to be stored.

### Example ###
> STORE FORCE (PIN, PULL, SLOW)

requests that the constraint force and torque components within the joint named <tt>PIN</tt> and the forces transmitted through the spring named <tt>PULL</tt> and the damper named <tt>SLOW</tt> be stored on a file for all positions simulated.

### Notes ###
# Each _name_ must be defined before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement by a <tt>SPRING</tt> statement, a <tt>DAMPER</tt> statement, or a joint definition statement. If not, the undefined _name_ is ignored and a message is printed at each position simulated.
# Each _name_ must be separated from others by a valid separator.
# No more than 33 _names_ may be specified in a single <tt>STORE FORCE</tt> statement.
# If more than one <tt>STORE FORCE</tt> statement is encountered, the lists of _names_ are concatenated including repeats if a _name_ is given more than once.
# The keyword <tt>ALL</tt> may be used as a _name_, and requests that the constraint forces in all joints, springs, and dampers be included among those stored.
# The force data for each _name_ are stored as each position of the system is simulated; they are stored in the order given.
# The constraint force and torque components stored include all static and dynamic effects consistent with the current model and the instantaneous operating conditions at the time of storage. For example, if <tt>DATA GRAVITY</tt> and <tt>DATA MASS</tt> statements have been given, the static forces due to the weights of the links are included; if <tt>DATA MOTION</tt> statements are also given, the dynamic forces are also included.
# Force data are stored in force units and torque data are stored in units of length force.
# The constraint force and torque components stored must be interpreted according to the statements which defined the joint and its data. If, for example, the constraint forces and torques are requested for a joint defined by the statement <pre>ZPIN (LK1, LK2) = PIN</pre> then the force and torque components stored are those exerted by link <tt>LK</tt>1 onto link <tt>LK</tt>2. Three components of force and three components of torque are stored; they are the components along and about the axes of the local coordinate system attached to link <tt>LK</tt>2 at the joint <tt>PIN</tt>.
# The force components within a joint are considered positive when in the same direction as the positive local coordinate axes. The torque components are considered positive when counterclockwise as seen from the positive ends of the local coordinate axes.
# A single force is stored for a spring or damper; it is positive if the spring or damper is in tension.
# Any statically indeterminate force or torque component is stored as "0.000002" and is treated as zero. Such statically indeterminate components are not necessarily zero (for example, if the system is assembled under preload), but are not possible to evaluate in a rigid body simulation.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests are output. Subsequent <tt>STORE</tt> requests are output to the same file.


## The <tt>PRINT FREQUENCY</tt> Statement ##
The <tt>PRINT FREQUENCY</tt> statement requests that the instantaneous natural frequencies and associated damping ratios of the system be printed for each position simulated.

### Format ###
> PRINT FREQUENCY

### Notes ###
# The frequencies and damping ratios printed correspond to the small amplitude oscillations of the system with all specified generalized coordinates (SGCs) held stationary.
# If the system has no free generalized coordinates (FGCs), it has no rigid body freedoms for oscillation and has no natural frequencies. If this is encountered, the request is ignored and a message is printed at each position simulated.
# Since most mechanical systems simulated are nonlinear, the natural frequencies and damping ratios change with the configuration of the system. They are recalculated and printed at each position simulated.
# If the system is in a stable configuration and not over-damped, there are as many natural frequencies as FGCs. These are printed in units of radians per second and the associated damping ratios (dimensionless) are also printed.
# When one or more of the normal modes of vibration of the system is over-damped, the instantaneous response of the system includes an exponential decay. In this case, the appropriate time constant is printed with units of inverse seconds.
# If the system is in an unstable configuration, its instantaneous response is non-oscillatory and includes an exponential growth rate. Such cases are treated by printing a negative time constant with units of inverse seconds.


## The <tt>PRINT DYNAMICS</tt> Statement ##
The <tt>PRINT DYNAMICS</tt> statement requests that the small oscillation transfer functions for the vibratory response of specified joints or points of the system to a specified vibratory input force or motion be printed at the end of the simulation.

### Format ###
> PRINT DYNAMICS (input, namein, nin) = kind,name; kind,name; ...

where _input_ specifies the kind of vibratory input and may be either the keyword <tt>FORCE</tt> or the keyword <tt>MOTION</tt>; _namein_ is the alphanumeric name of the force or joint where the vibratory input excitation is considered applied; _nin_ is an integer zero when _namein_ refers to a force or torque or is the integer number of the joint variable within the joint when _namein_ refers to a joint. Each _kind,name_ pair specifies a transfer function to be printed; _kind_ may be any one of the keywords <tt>POSITION</tt>, <tt>VELOCITY</tt>, or <tt>ACCEL</tt>, and _name_ specifies the alphanumeric name of the joint or point whose transfer function is to be printed.

### Examples ###
> PRINT DYNAMICS (FORCE, PULL, 0) = POSITION,PT1

requests that the transfer function for the position response of the point named <tt>PT1</tt> to a unit vibratory force input named <tt>PULL</tt> be printed.

> PRINT DYNAMICS (MOTION, CYL, 2) = VELOCITY,PIN; ACCEL,PT5

requests that two transfer functions be printed showing responses to a unit motion input in the second joint variable (the translation) of the cylindric joint named <tt>CYL</tt>. The first response printed should be the relative velocity response of the joint named <tt>PIN</tt>; the second should be the absolute acceleration response of the point named <tt>PT5</tt>.

### Notes ###
# The requested transfer functions are not printed immediately, but at the completion of the next simulation, after the next <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement is issued.
# Since most systems simulated are nonlinear, the transfer functions change with the configuration of the system. The desired configuration can be achieved by judicious use of the <tt>EXECUTE HOLD</tt> statement.
# The transfer functions are printed as formulae using the LaPlace operator variable, S. They can be considered complex functions of frequency by substituting the product of frequency and the unit imaginary number for the variable for S.
# If _input_ is not one of the keywords <tt>FORCE</tt> or <tt>MOTION</tt>, then the request is ignored and a message is printed.
# If _input_ is the keyword <tt>FORCE</tt> then _namein_ must be defined by a <tt>FORCE</tt> statement or a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If _input_ is the keyword <tt>MOTION</tt> then _namein_ must be defined by a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If not, the request is ignored and a message is printed.
# If _input_ is the keyword <tt>FORCE</tt> then _namein_ may not be used in a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement. If _input_ is the keyword <tt>MOTION</tt> then _namein_ must be specified by as an SGC by a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. Otherwise, the request is ignored and a message is printed.
# If _namein_ refers to a force name, then _nin_ may be zero; if _namein_ refers to a joint name, then _nin_ must be a positive integer less than or equal to the number of joint variables of that joint. Otherwise, the request is ignored and a message is printed.
# Each _kind_ must be one of the keywords <tt>POSITION</tt>, <tt>VELOCITY</tt>, or <tt>ACCEL</tt>; otherwise the request is ignored and a message is printed.
# Each _name_ must refer to a name defined by a <tt>POINT</tt> statement or a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If not, the undefined _kind,name_ pair is ignored and a message is printed.
# No more than 15 _kind,name_ pairs may be specified in a single <tt>PRINT DYNAMICS</tt> statement.
# More than one <tt>PRINT DYNAMICS</tt> statement may be used if desired.
# The transfer functions printed correspond to the small amplitude vibration response of the system with any specified generalized coordinates (SGCs) held stationary, except perhaps for joint _namein_.
# If the system has no free generalized coordinates (FGCs), it has no freedom for vibratory response and transfer functions are not defined. If this is encountered, the request is ignored and a message is printed.


## The <tt>LIST DYNAMICS</tt> Statement ##
The <tt>LIST DYNAMICS</tt> statement requests that the small oscillation transfer functions for the vibratory response of specified joints or points of the system to a specified vibratory input force or motion be listed for a specified frequency range at the end of the simulation.

### Format ###
> LIST DYNAMICS(w0,wf,winc/input,namein,nin)=kind,name;...

where _w0_, _wf_, and _winc_ specify the numeric values of the low frequency, the high frequency, and the initial frequency increment, respectively, for the listing; _input_ specifies the kind of vibratory input and may be either the keyword <tt>FORCE</tt> or the keyword <tt>MOTION</tt>; _namein_ is the alphanumeric name of the force or joint where the vibratory input excitation is applied; _nin_ is an integer zero when _namein_ refers to a force or torque, or is the integer number of the joint variable within the joint when _namein_ refers to a joint. Each _kind,name_ pair specifies a transfer function to be listed; _kind_ may be one of the keywords <tt>POSITION</tt>, <tt>VELOCITY</tt>, or <tt>ACCEL</tt>, and _name_ specifies the alphanumeric name of a joint or point whose transfer function is to be listed.

### Examples ###
> LIST DYNAMICS (10,1000,2 / FORCE,PULL,0) = POSITION, PT1

specifies that the transfer function for the position response of the point named <tt>PT1</tt> to a unit vibratory force input named <tt>PULL</tt> is to be listed over the frequency range from 10 to 1000 radians per second with an initial increment of 2 radians per second.

> LIST DYNAMICS(0.5,200,0.02/MOTION,CYL,2)=VELOCITY,PIN;ACCEL,PT5

requests that two transfer functions be listed over the frequency range from 0.5 to 200 radians per second with an initial increment of 0.02 radians per second showing responses to a unit motion
input in the second joint variable (the translation) of the cylindric joint named <tt>CYL</tt>. The first represents the relative velocity response of the joint named <tt>PIN</tt>; the second represents the absolute acceleration response of the point named <tt>PT5</tt>.

### Notes ###
# The requested transfer functions are not listed immediately, but at the completion of the next simulation, after the next <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement.
# Since most systems simulated are nonlinear, the transfer functions change with the configuration of the system. The desired configuration can be achieved by judicious use of the <tt>EXECUTE HOLD</tt> statement.
# The values of _w_<sub>0</sub>_,_w<sub>f</sub>_, and_winc_must be greater than zero; if not, the request is ignored and a message is printed.
# The value of_wf_must be greater than the value of_w0_; if not, the request is ignored and a message is printed.
# The initial frequency increment in the listing is made by adding_winc_to_w0_; after that the frequency increments are taken logarithmically.
# If_input_is not one of the keywords_<tt>FORCE</tt> or <tt>MOTION</tt>, then the request is ignored and a message is printed.
# If _input_ is the keyword <tt>FORCE</tt> then _namein_ must be defined by a <tt>FORCE</tt> statement or a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If _input_ is the keyword <tt>MOTION</tt> then _namein_ must be defined by a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If not, the request is ignored and a message is printed.
# If _input_ is the keyword <tt>FORCE</tt> then _namein_ may not be used in a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement. If _input_ is the keyword <tt>MOTION</tt> then _namein_ must be specified as an SGC by a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. Otherwise, the request is ignored and a message is printed.
# If _namein_ refers to a force name then _nin_ must be zero; if _namein_ refers to a joint name then _nin_ must be a positive integer less than or equal to the number of joint variables of that joint. Otherwise, the request is ignored and a message is printed.
# Each _kind_ must be one of the keywords <tt>POSITION</tt>, <tt>VELOCITY</tt>, or <tt>ACCEL</tt>; otherwise the request is ignored and a message is printed.
# Each _name_ must refer to a name defined by a <tt>POINT</tt> statement or a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If not, the undefined _kind,name_ pair is ignored and a message is printed.
# No more than 14 _kind,name_ pairs may be specified in a single <tt>LIST DYNAMICS</tt> statement.
# More than one <tt>LIST DYNAMICS</tt> statement may be used if desired.
# The transfer functions listed correspond to the small amplitude vibration response of the system with any specified generalized coordinates (SGCs) held stationary, except perhaps for _namein_.
# If the system has no free generalized coordinates (FGCs), it has no freedom for vibratory response and transfer functions are not defined. If this is encountered, the request is ignored and a message is printed.
# The units for frequency are radians per second.


## The <tt>STORE DYNAMICS</tt> Statement ##
The <tt>STORE DYNAMICS</tt> statement requests that the small oscillation transfer functions for the vibratory response of specified joints or points of the system to a specified vibratory input force or motion be stored on a file at the end of the simulation.

### Format ###
> STORE DYNAMICS(input,namein,nin)=kind,name;kind,name;...

where _input_ specifies the kind of vibratory input and may be either the keyword <tt>FORCE</tt> or the keyword <tt>MOTION</tt>; _namein_ is the alphanumeric name of the force or joint where the vibratory input excitation is applied; _nin_ is an integer zero for a <tt>FORCE</tt> _input_, or is the integer number of the joint variable within joint _namein_ for <tt>MOTION</tt> input. Each _kind,name_ pair specifies a transfer function to be stored; _kind_ may be any one of the keywords <tt>POSITION</tt>, <tt>VELOCITY</tt>, or <tt>ACCEL</tt> and _name_ specifies the alphanumeric name of the joint or point whose transfer function is to be stored.

### Examples ###
> STORE DYNAMICS (FORCE, PULL, 0) = POSITION, PT1

specifies that the transfer function for the position response of the point named <tt>PT1</tt> to a unit vibratory force input named <tt>PULL</tt> is to be stored on a file.

> STORE DYNAMICS(MOTION,CYL,2)=VELOCITY,PIN;ACCEL,PT5

requests that two transfer functions be stored on a file showing responses to a unit motion input in the second joint variable (the translation) of the cylindric joint named <tt>CYL</tt>. The first should be the relative velocity response of the joint variable of the joint named <tt>PIN</tt>; the second should be the absolute acceleration response of the point named <tt>PT5</tt>.

### Notes ###
# The requested transfer functions are not stored immediately, but at the completion of the next simulation, after the next <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement.
# Since most systems simulated are nonlinear their transfer functions change with the configuration of the system. The desired configuration can be achieved by judicious use of the <tt>EXECUTE HOLD</tt> statement.
# If _input_ is not one of the keywords <tt>FORCE</tt> or <tt>MOTION</tt> then the request is ignored and a message is printed.
# If _input_ is the keyword <tt>FORCE</tt> then _namein_ must be defined by a <tt>FORCE</tt> statement or a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If _input_ is the keyword <tt>MOTION</tt> then _namein_ must be defined by a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If not the request is ignored and a message is printed.
# If _input_ is the keyword <tt>FORCE</tt> then _namein_ may not be used in a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement. If _input_ is the keyword <tt>MOTION</tt>, then _namein_ must be specified as an SGC by a <tt>DATA POSITION</tt> or <tt>DATA MOTION</tt> statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. Otherwise, the request is ignored and a message is printed.
# If _namein_ refers to a force name then _nin_ must be zero; if _namein_ refers to a joint name then _nin_ must be a positive integer less than or equal to the number of joint variables of that joint. Otherwise the request is ignored and a message is printed.
# Each _kind_ must be one of the keywords <tt>POSITION</tt>, <tt>VELOCITY</tt>, or <tt>ACCEL</tt>; otherwise the request is ignored and a message is printed.
# Each _name_ must refer to a name defined by a <tt>POINT</tt> statement or a joint definition statement before the <tt>EXECUTE</tt> or <tt>EXECUTE HOLD</tt> statement. If not, the undefined _kind,name_ pair is ignored and a message is printed.
# No more than 15 _kind,name_ pairs may be specified in a single <tt>STORE DYNAMICS</tt> statement.
# More than one <tt>STORE DYNAMICS</tt> statement may be used if desired.
# The transfer functions stored correspond to the small amplitude vibration response of the system with any specified generalized coordinates (SGCs) held stationary, except perhaps for joint _namein_.
# If the system has no free generalized coordinates (FGCs), it has no freedom for vibratory response and transfer functions are not defined. If this is encountered, the request is ignored and a message is printed.
# Immediately following the first <tt>STORE</tt> request, the user is prompted to supply a file name in which all <tt>STORE</tt> requests are output. Subsequent <tt>STORE</tt> requests are output to the same file.