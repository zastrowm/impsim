# Chapter 8: Graphics Statements #
In order to use any of the graphics capabilities in the IMP program it is assumed that the user is running IMP interactively from a system which has graphics capabilities known to the IMP system. If these conditions are not met, that is, if IMP is executed in background mode, if the user has not specified graphics capability, or if IMP does not contain support for the present graphic device, then it is not possible to obtain graphic output from IMP. When an interactive IMP task is initiated (see Section 2-1), the terminal screen is erased and a banner is printed. Immediately after this the user is asked if the IMP task should be run with graphic or alphanumeric output. If the prompt is answered with the response "ALPHA" then no graphic output is attempted for the session; if the response "GRAPHIC" is given then the statements in this chapter cause graphic output on the terminal screen. This choice can be reversed by later use of a DEVICE statement. This chapter presents the various graphics statements recognized by the IMP interpreter. Graphics statements may be used both to draw a schematic diagram of the system model and/or to request graphs of simulation results. The first word of each graphics statement instructs the IMP system to interpret the remainder of the statement according to one of the following formats:

## The DEVICE Statement ##
The DEVICE statement specifies whether a graphic or an alphanumeric output device is to be used.
### Format: ###
DEVICE = kind where "kind" is one of the keywords: ALPHA or GRAPHIC
### Example: ###
DEVICE = graphic specifies that subsequent graphics statements are intended for output on a graphic display terminal.
### Notes: ###

# This statement should precede the use of any other IMP graphics statements. If not IMP assumes an ALPHA device type and no graphic output is obtained during the session.
# If "kind" is the keyword ALPHA the output device is assumed to be non-graphic capable and no graphic output is obtained directly even though graphic statements are entered.
# GRAPHIC is a valid "kind" when using an Intel-based (IBM PC) or compatible system, or when using a Unix or Linux system with X-windows support. See your system manager if you have further questions.
# If IMP execution is not interactive then "kind" is treated as ALPHA in spite of the keyword specified.
# If the "kind" of device is set to ALPHA or if IMP is executing in non-interactive background mode or if no IMP graphics statements are encountered then no graphic output is produced on the output display.
## The PLOT VALUE Statement ##
The PLOT VALUE statement requests that the values and time derivatives of specified VALUE expressions be plotted versus time for all positions simulated.
### Format: ###
PLOT VALUE (name, name, ... ) where each "name" is the alphanumeric name of a VALUE expression whose value and derivatives are to be plotted.
### Example: ###
PLOT VALUE (F1, F2, WAVE, DX) requests that previously defined VALUE expressions named F1, F2, WAVE, and DX and their time derivatives be plotted for all positions simulated.
### Notes: ###

# Each "name" must be defined by a VALUE statement before the EXECUTE or EXECUTE HOLD statement is given; if not, each undefined VALUE "name" is ignored and a message is printed at each position simulated.
# No more than 33 "names" may be specified in a single PLOT VALUE statement.
# If more than one PLOT VALUE statement is encountered the lists of "names" are concatenated including repeats if a "name" is given more than once.
# The keyword ALL may be used as a "name", and requests that all named VALUE statements be included among those plotted.
# The values of all specified "names" and their first and second time derivatives are saved until the end of the simulation; they are then sorted and plotted in the order named.
## The PLOT POSITION Statement ##
The PLOT POSITION statement requests that the positions of specified joints, points, springs, and dampers be plotted versus time for all positions simulated.
### Format: ###
PLOT POSITION (name, name, ... ) where each "name" is the alphanumeric name of a joint, point, spring, or damper whose position is to be plotted.
### Example: ###
PLOT POSITION (PIN, PT1, BALL, PT5, SLIP) requests that the positions of the joint variables of the joints named PIN and BALL, the global position coordinates of the points named PT1 and PT5, and the position of the damper named SLIP be plotted for all positions simulated.
### Notes: ###

# Each "name" must be defined before the EXECUTE or EXECUTE HOLD statement by a POINT statement, a SPRING statement, a DAMPER statement, or a joint definition statement. If not, the undefined "name" is ignored and a message is printed at each position simulated.
# No more than 33 "names" may be specified in a single PLOT POSITION statement.
# If more than one PLOT POSITION statement is encountered, the lists of "names" are concatenated including repeats if a "name" is given more than once.
# The keyword ALL may be used as a "name", and requests that the positions of all joints, points, springs, and dampers be included among those plotted.
# The position data for all specified "names" are saved until the end of the simulation; they are then sorted and plotted in the order named.
# The dimensions of the position data plotted are degrees or length units as appropriate.
# If "name" refers to a joint, the relative positions of the joint variables are plotted. The signs of the joint variable positions plotted are consistent with the joint variable definitions (see the appropriate joint definition statement).
# If "name" refers to a point, the global coordinates of that point are plotted.
# If "name" refers to a spring or damper, its absolute length is plotted.
## The PLOT VELOCITY Statement ##
The PLOT VELOCITY statement requests that the velocities of specified joints, points, springs, and dampers be plotted versus time for all positions simulated.
### Format: ###
PLOT VELOCITY (name, name, ... ) where each "name" is the alphanumeric name of a joint, point, spring, or damper whose velocity is to be plotted.
### Example: ###
PLOT VELOCITY (PIN, PT1, BALL, PT5, SLIP) requests that the velocities of the joint variables of the joints named PIN and BALL, the absolute velocities of the points named PT1 and PT5, and the relative velocity across the damper named SLIP be plotted for all positions simulated.
### Notes: ###

# Each "name" must be defined before the EXECUTE or EXECUTE HOLD statement by a POINT statement, a SPRING statement, a DAMPER statement, or a joint definition statement. If not, the undefined "name" is ignored and a message is printed at each position simulated.
# No more than 33 "names" may be specified in a single PLOT VELOCITY statement.
# If more than one PLOT VELOCITY statement is encountered, the lists of "names" are concatenated including repeats if a "name" is listed more than once.
# The keyword ALL may be used as a "name", and requests that the velocities of all joints, points, springs, and dampers be included among those plotted.
# The velocity data for all specified "names" are saved until the end of the simulation; they are then sorted and plotted in the order named.
# The dimensions of the velocity data plotted are radians per second or length units per second as appropriate.
# If "name" refers to a joint, the relative velocities of the joint variables are plotted. The signs of the joint variable velocities plotted are consistent with the joint variable definitions (see the appropriate joint definition statement).
# If "name" refers to a point, the global components of the absolute velocity vector for that point are plotted.
# If "name" refers to a spring or damper, the magnitude of the relative velocity along the spring or damper is plotted.
## The PLOT ACCEL Statement ##
The PLOT ACCEL statement requests that the accelerations of specified joints, points, springs, and dampers be plotted versus time for all positions simulated.
### Format: ###
PLOT ACCEL (name, name, ... ) where each "name" is the alphanumeric name of a joint, point, spring, or damper whose acceleration is to be plotted.
### Example: ###
PLOT ACCEL (PIN, PT1, BALL, PT5, SLIP) requests that the accelerations of the joint variables of the joints named PIN and BALL, the absolute accelerations of the points named PT1 and PT5, and the relative acceleration across the damper named SLIP be plotted.
### Notes: ###

# Each "name" must be defined before the EXECUTE or EXECUTE HOLD statement by a POINT statement, a SPRING statement, a DAMPER statement, or a joint definition statement. If not, the undefined "name" is ignored and a message is printed at each position simulated.
# No more than 33 "names" may be specified in a single PLOT ACCEL statement.
# If more than one PLOT ACCEL statement is encountered, the lists of "names" are concatenated including repeats if a "name" is listed more than once.
# The keyword ALL may be used as a "name" and requests that the accelerations of all joints, points, springs, and dampers be included among those plotted.
# The acceleration data for all specified "names" are saved until the end of the simulation; they are then sorted and plotted in the order named.
# The dimensions of the acceleration data plotted are radians per second per second or length units per second per second as appropriate.
# If "name" refers to a joint, the relative accelerations of the joint variables of that joint are plotted. The signs of the joint variable accelerations plotted are consistent with the joint variable definitions (see the appropriate joint definition statement).
# If "name" refers to a point, the global components of the absolute acceleration vector for that point are plotted.
# If "name" refers to a spring or damper, the magnitude of the relative acceleration along that spring or damper is plotted.
## The PLOT FORCE Statement ##
The PLOT FORCE statement requests that the constraint forces and torques acting within specified joints, springs, and dampers be plotted versus time for all positions simulated.
### Format: ###
PLOT FORCE (name, name, ... ) where each "name" is the alphanumeric name of a joint, spring, or damper for which the constraint force and torque components are to be plotted.
### Example: ###
PLOT FORCE (PIN, PULL, SLOW) requests that the constraint force and torque components within the joint named PIN and the forces transmitted through the spring named PULL and the damper named SLOW be plotted for all positions simulated.
### Notes: ###

# Each "name" must be defined before the EXECUTE or EXECUTE HOLD statement by a SPRING statement, a DAMPER statement, or a joint definition statement. If not, the undefined "name" is ignored and a message is printed at each position simulated.
# No more than 33 "names" may be specified in a single PLOT FORCE statement.
# If more than one PLOT FORCE statement is encountered, the lists of "names" are concatenated including repeats if a "name" is listed more than once.
# The keyword ALL may be used as a "name", and requests that the constraint force components in all joints, springs, and dampers be included among those plotted.
# The force data for all specified "names" are saved until the end of the simulation; they are then sorted and plotted in the order given.
# The constraint force and torque components plotted include all static and dynamic effects consistent with the model and the operating conditions. For example, if DATA GRAVITY and DATA MASS or DATA DENSITY statements have been given, the static forces due to the weights of the links are included; if DATA MOTION statements are also given, then dynamic forces are also included.
# Force data are plotted in force units and torque data are plotted in units of length force.
# The constraint force and torque components plotted must be interpreted according to the statements which define the joint and its data. If, for example, the constraint forces and torques are requested for the joint defined by the statement: ZPIN (LK1, LK2) = PIN then the force and torque components plotted are those exerted by LK1 onto LK
# Three components of force and three components of torque are plotted; they are the components along and about the axes of the local coordinate system attached to link LK2 at the joint named PIN.
# The force components within a joint are considered positive when in the same direction as the positive local coordinate axes. The torque components are considered positive when counter-clockwise as seen from the positive ends of the local coordinate axes. 1
# A single force is plotted for a spring or damper; it is positive if the spring or damper is in tension.
## The PLOT DYNAMICS Statement ##
The PLOT DYNAMICS statement requests that the small oscillation transfer functions for the vibratory response of specified joints or points of the system to a specified vibratory input force or motion be plotted over a specified frequency range at the end of the simulation.
### Format: ###
PLOT DYNAMICS (w0,wf,winc; input,namein,nin) = kind,name; $ kind,name; ... where "w0", "wf", and "winc" specify the numeric values of the low frequency, the high frequency, and the initial frequency increment for the plots, respectively; "input" specifies the kind of vibratory input and may be either the keyword FORCE or the keyword MOTION; "namein" is the alphanumeric name of the force or joint where the vibratory input excitation is applied; "nin" is an integer zero for a FORCE "input", or is the integer number of the joint variable within joint "namein" for a MOTION "input". Each "kind,name" pair specifies a transfer function to be plotted; "kind" may be any one of the keywords POSITION, VELOCITY, or ACCEL, and "name" specifies the alphanumeric name of the joint or point whose transfer function is desired.
### Examples: ###
PLOT DYNAMICS (10,1000,2; FORCE PULL 0) = POSITION PT1 specifies that the transfer function for the POSITION response of the point named PT1 to a unit vibratory FORCE input named PULL is to be plotted over the frequency range from 10 to 1000 radians per second with an initial increment of 2 radians per second. PLOT DYNAMICS (0.5,200,0.02; MOTION CYL 2) = VELOCITY PIN $ ACCEL PT5 requests that two transfer functions be plotted over the frequency range from 0.5 to 200 radians per second with an initial increment of 0.02 radians per second showing responses to a unit MOTION input in the second joint variable, the translation of the cylindric joint named CYL. The first plot will represent the relative VELOCITY response of the revolute joint named PIN; the second plot will represent the absolute ACCEL response of the point named PT
#
### Notes: ###

# The requested transfer functions are not plotted immediately, but at the completion of the next simulation, after the next EXECUTE or EXECUTE HOLD statement.
# Since most systems simulated are non-linear, the transfer functions change with the configuration of the system. The desired configuration can be achieved by judicious use of the EXECUTE HOLD statement.
# The values of "w0", "wf", and "winc" must be greater than zero; if not, the PLOT request is ignored and a message is printed.
# The value of "wf" must be greater than the value of "w0"; if not, the PLOT request is ignored and a message is printed.
# The initial increment between the points plotted is made by adding "winc" to "w0"; after that, the frequency increments are taken logarithmically.
# If "input" is not one of the keywords FORCE or MOTION, then the PLOT request is ignored and a message is printed.
# If "input" is the keyword FORCE, then "namein" must be defined by a FORCE statement or a joint definition statement before the EXECUTE or EXECUTE HOLD statement. If "input" is the keyword MOTION, then "namein" must be defined by a joint definition statement before the EXECUTE or EXECUTE HOLD statement. If not, the request is ignored and a message is printed.
# If "input" is the keyword FORCE, then "namein" may not appear in a DATA POSITION or DATA MOTION statement. If "input" is the keyword MOTION, then "namein" must be specified as an SGC by a DATA POSITION or DATA MOTION statement before the EXECUTE or EXECUTE HOLD statement. Otherwise, the PLOT request is ignored and a message is printed.
# If "namein" refers to a force name, then "nin" must be zero; if "namein" refers to a joint name, then "nin" must be a positive integer less than or equal to the number of joint variables of that joint. Otherwise, the PLOT request is ignored and a message is printed. 1
# Each "kind" must be one of the keywords POSITION, VELOCITY, or ACCEL; otherwise, the PLOT request is ignored and a message is printed. 1
# Each "name" must refer to a name defined by a POINT statement or a joint definition statement before the EXECUTE or EXECUTE HOLD statement. If not, the undefined "kind,name" pair is ignored and a message is printed. 1
# No more than 14 "kind,name" pairs may be specified in a single PLOT DYNAMICS statement. 1
# More than one PLOT DYNAMICS statement may be used if desired. 1
# The transfer functions plotted correspond to the small amplitude vibration response of the system with all specified generalized coordinates (SGCs) held stationary, except perhaps for "namein". 1
# If the system has no free generalized coordinates (FGCs), it has no freedom for vibratory response and transfer functions are not defined. If this is encountered, the PLOT request is ignored, and a message is printed. 1
# The units used for frequency are radians per second (Hz).
## The DELETE PLOT Statement ##
The DELETE PLOT statement is used to delete requests made by previous PLOT statements.
### Format: ###
DELETE PLOT (kind, kind, ... ) where each "kind" is one of the keywords: VALUE, POSITION, VELOCITY, ACCEL, FORCE, or DYNAMICS.
### Example: ###
DELETE PLOT (FORCE, ACCEL) requests that all previous requests made by PLOT FORCE and PLOT ACCEL statements be deleted.
### Notes: ###

# Each "kind" must correspond to one or more previous PLOT statements using the same keyword; if not, the improper "kind" is ignored and a message is printed.
# Each "kind" requests the deletion of all previous PLOT statements of that "kind" with their entire lists of names. A reduced list of names may only be achieved by deleting the entire PLOT statement and respecifying it.
# The keyword ALL may be used as a "kind", and requests the deletion of all previous PLOT statements, irrespective of their "kind".
## The DRAW Statement ##
The DRAW statement causes a drawing of visible portions of the system model to be drawn on the currently active graphics device. The contents of the picture are controlled by other IMP graphics statements.
### Format: ###
DRAW specifies that the drawing should be drawn immediately.
### Notes: ###

# The system is viewed as directed by the most recent DATA VIEW, RECALL VIEW, SLIDE, TURN, DATA DRAW, and/or ZOOM statement(s). If no such statements have been specified, the view is taken from infinitely far away on the positive global Z axis, looking at the global origin, with the global Y axis appearing vertical. The drawing is not centered, or scaled to fit the screen, however. Centering and scaling may be accomplished with the DATA VIEW statement.
# The contents of the drawing may be controlled by the SHOW, ERASE, and AXES statements.
# The DRAW statement may be repeated as many times as desired; a new drawing is produced each time.
# When a DRAW statement is used, the system is drawn in its current position. Another position of the system may be drawn by use of the EXECUTE HOLD statement followed by another DRAW statement. However, only one picture is drawn for each DRAW statement. Multiple positions can be drawn (superimposed) by use of the ANIMATE statement.
# Use of the DRAW statement cancels any previous request for an animated drawing sequence requested by an ANIMATE statement.
## The ANIMATE Statement ##
The ANIMATE statement causes a drawing of visible portions of the system model to be drawn on the currently active graphic device, and to be superimposed on other drawings at each position reached during subsequent simulations requested by the EXECUTE or EXECUTE HOLD statement(s).
### Format: ###
ANIMATE specifies that, during future simulations requested by the EXECUTE or EXECUTE HOLD statement, drawings of the system should be drawn repetitively as its geometry changes.
### Notes: ###

# The system is viewed as directed by the most recent DATA VIEW, RECALL VIEW, SLIDE, TURN, DATA DRAW, or ZOOM statement(s). If no such statements have been specified, the view is taken from infinitely far away on the positive global Z axis, looking at the global origin, with the global Y axis appearing vertical. The picture is not centered, or scaled to fit the screen, however. Centering and scaling may be accomplished with the DATA VIEW statement.
# The contents of the drawing drawn may be controlled by the SHOW, ERASE, and AXES statements.
# When the ANIMATE statement is entered, in contrast to the DRAW statement, no picture is drawn immediately. The ANIMATE statement requests that pictures should be drawn at each position reached during future simulations caused by EXECUTE or EXECUTE HOLD statement(s).
# After an ANIMATE statement has been entered, animated sequences of drawings occur for every EXECUTE or EXECUTE HOLD statement until a DRAW statement is entered. A DRAW statement cancels any previous ANIMATE request.
## The DATA VIEW Statement ##
The DATA VIEW statement defines the orientation of the observer relative to the system in viewing the drawing to be produced by a subsequent DRAW or ANIMATE statement.
### Format: ###
There are two forms of the DATA VIEW statement. The first is: DATA VIEW = xe,ye,ze; xv,yv,zv
where "xe,ye,ze" are numeric values of the global coordinates of the viewer's eye and "xv,yv,zv" are numeric values of the global components of a vector which should appear vertically upward in the drawing to be made. The second form of the DATA VIEW statement is: DATA VIEW = name where "name" is an alphanumeric keyword defining data for certain commonly used views. The valid names and their definitions are given in the following table:
### Examples: ###
DATA VIEW = 0.0, 0.0, 10.0; 0.0, 1.0, 0.0 specifies that the next picture is to be drawn looking in from the positive global Z axis, with the positive global Y axis appearing vertically upward and the positive global X axis horizontal to the right. This example may also take any of the following equivalent forms: DATA VIEW = 0, 0, 10; 0, 1, 0 "name" Global X-axis Global Y-axis Global Z-axis FRONT to right upward outward BACK to left upward inward TOP to right outward downward BOTTOM to right inward upward LEFT outward upward to left RIGHT inward upward to right ISOMETRIC down to right upward down to left DATA VIEW = , , 10; , 1 DATA VIEW = FRONT
### Notes: ###

# If no DATA VIEW statement is given, then DATA VIEW = FRONT is assumed as a default. However, the picture is not centered or scaled to fit the screen in this case.
# The DATA VIEW statement must precede the DRAW or ANIMATE statement to which it refers.
# If more than one DATA VIEW statement is given, the last statement takes precedence and earlier data are replaced.
# All numeric "x,y,z" data refer to the same global reference frame used for defining the system model.
# All numeric "x,y,z" data have units of length.
# The angle formed between the two vectors need not be a right angle. If not, the viewing plane is assumed to be perpendicular to the "xe,ye,ze" vector and the "xv,yv,zv" data are adjusted accordingly. The two vectors must not be parallel or an error will result.
# If a new DEVICE statement follows the DATA VIEW statement, the effect of the DATA VIEW statement is lost.

## The DATA DRAW Statement: ##
The DATA DRAW statement defines the distance of the viewer from the drawing and, therefore, the amount of perspective to be used in pictures drawn by subsequent DRAW or ANIMATE statements.

### Format: ###
DATA DRAW = distance where "distance" is the numeric value of the distance from the eye of the observer to the center of the pictured portion of the model.
### Example: ###
DATA DRAW = 100 specifies that the observer is looking from 100 length units out from the center of the field of view of the drawing.
### Notes: ###

# If no DATA DRAW statement is given the DRAW or ANIMATE statement produces a picture viewed from infinitely far away; that is, an orthographic projection.
# The DATA DRAW statement must precede the DRAW or ANIMATE statement to which it refers.
# If more than one DATA DRAW statement is given, the later statement takes precedence and earlier data are replaced.
# The "distance" value has the same units of length used in defining the system model.
# If the "distance" value is given as zero, it is assumed that it should be treated as an infinite "distance", thus leading to an orthographic projection.
## The SHOW Statement ##
The SHOW statement requests that certain named entities in the system model be made visible and specifies their color in future drawings produced by the DRAW or ANIMATE statement.
### Format: ###
SHOW (color) = name, name, ... where each "name" is the alphanumeric name of a previously defined link, spring, damper, force, or torque to be made visible in future pictures and "color" specifies one of the keywords BLACk, RED, ORANge, YELLow, GREEn, AQUA, BLUE, VIOLet, or WHITe as the color to be used for the named items.
### Example: ###
SHOW (RED) = LK1, F requests that the link named LK1 and the force named F be visible and colored red in future pictures.
### Notes: ###

# A SHOW statement must precede the DRAW or ANIMATE statement to which it refers. It remains in effect for each "name" until explicitly changed by a subsequent ERASE statement.
# Each "name" of a spring, damper, force, or torque will cause the appearance of the appropriate schematic symbol in future drawings. These items are initially treated as visible (WHITE) until explicitly named in a SHOW or ERASE statement.
# If "name" refers to a link, the shape drawn depends on whether an external file defining a geometric shape was specified in a SOLID statement for that link. If so, that shape and its color are first set by the contents of the file.
# If "name" refers to a link but the shape is not defined by a SOLID statement with an external file, the shape drawn depends on the points defined on the link. Each POINT statement is assumed to imply a series of straight line segments drawn in the order of the several point names defined in that POINT statement. If two or more point names are not defined in a single POINT statement, no shape is drawn.
# The SHOW statement, by itself, does not cause the drawing of a picture, but only defines the color of visible entities for future DRAW or ANIMATE statements.
# The keyword ALL may be used as a "name" and requests that all links, springs, dampers, forces, and torques be made visible.
# The keyword LOOP followed by an integer (e.g., LOOP 3) may be used as a "name" and requests that the kinematic loop of that number be shown in subsequent drawings as a set of dashed line arrows of the specified color. The loop numbers range from one to the total number of joints less the number of links plus one. If no number is specified or if the number is outside of this range, then all kinematic loops are set to the specified color.
# The "color" specified must be one of the keywords BLACk, RED, ORANge, YELLow, GREEn, AQUA, BLUE, VIOLet, or WHITe; if not the color WHITe is assumed as the default.
# Specifying the "color" of a named item as BLACk is equivalent to naming that item in an ERASE statement.
## The ERASE Statement ##
The ERASE statement requests that certain named entities in the system model be made invisible, that is, changed to color BLACK in future drawings produced by DRAW or ANIMATE statements. ERASE can also be used to clear the graphics output device and initialize for a new picture.
### Format: ###
ERASE (name, name, ...) where each "name" is the alphanumeric name of a previously defined link spring, damper, force, or torque to be made invisible in future pictures.
### Example: ###
ERASE (LK1, F) requests that the link named LK1 and the force named F not be visible in future drawings.
### Notes: ###

# If no "names" are given in an ERASE statement then the graphic output device is cleared.
# An ERASE statement must precede the DRAW or ANIMATE statement to which it refers. It remains in effect for each "name" until explicitly changed by a subsequent SHOW statement.
# The ERASE statement does not delete the entities named from the system model, but only eliminates their appearance in drawings.
# Each link, spring, damper, force, or torque is initially treated as visible (WHITE) until named in a SHOW or ERASE statement.
# The ERASE statement does not cause modification of previous drawings; it only defines changes for future drawings.
# The keyword ALL may be used as a "name" and requests that all links, springs, dampers, forces, and torques be made invisible.
# The keyword LOOP followed by an integer (e.g., LOOP 3) may be used as a "name" and requests that the kinematic loop of that number be made invisible in future pictures. See Note (7) of the SHOW statement.
## The AXES Statement ##
The AXES statement causes the local coordinate axes for specified joints to be shown in future schematic drawings.
### Format: ###
AXES (length) = name, name, ... where "length" is a numeric value specifying the length of the axes and each "name" is the alphanumeric name of a joint for which the local coordinate axes are to be drawn.
### Example: ###
AXES (0.5) = JT2 JT5 specifies that axes of 0.5 length unit should be drawn for each of the local coordinate axes of joints JT2 and JT
#
### Notes: ###

# An AXES statement must precede the DRAW or ANIMATE statement to which it refers. It remains in effect for each "name" until changed by a subsequent AXES statement.
# No more than 33 "names" may be specified in a single AXES statement.
# Each "name" must refer to a previously defined joint. If not, the invalid "name" is ignored; an error message is printed.
# The keyword ALL may be used as a "name" and requests that all currently defined joints be included among those for which local axes are to be drawn.
# If no "names" are given explicitly, the keyword ALL is assumed.
# The units for "length" are the same length units used in defining the system model.
# If "length" is not given explicitly, its occurrence must still be indicated by valid separators. A length of zero is used in this case.
# If "length" is zero, no coordinate axes are drawn by subsequent DRAW or ANIMATE statements for the named joints.
## The ZOOM Statement ##
The ZOOM statement requests that the picture produced by a subsequent DRAW or ANIMATE statement be magnified or reduced in scale.
### Format: ###
ZOOM (power) = xc,yc,zc
where "power" is the numeric value of the magnification or reduction factor relative to the previous picture.
### Example: ###
ZOOM (2.5) requests that a new schematic picture be drawn. It is to be 2.5 times the scale of the previous picture and is to show the area around the origin of the previous picture.
### Notes: ###

# If the value of "power" is entered as a positive number then the magnification or reduction is taken around the center of the previous picture.
# If, while operating interactively, a negative value is entered for "power" the user is requested to enter a screen location via the graphic input device to define the center of the magnified or reduced view.
# If, while operating interactively, a value of "power" of zero is entered or if the value of "power" is missing then the user is requested to enter two screen locations via the graphic input device. These two locations define diagonally opposite corners of the new picture and thus define the "power".
## The SLIDE Statement ##
The SLIDE statement requests that future pictures be translated by a given distance relative to the graphic display screen.
### Format: ###
SLIDE (axis) = distance where "axis" can be any of the keywords: X, Y, or Z, indicating a translation along the horizontal, vertical, or outward normal axis, respectively, of the graphic display device, and where "distance" is the numeric value of the distance by which the picture should be translated relative to its current position.
### Example: ###
SLIDE (X) = 3.5 specifies that the center of the current picture is to be displaced 3.5 length units to the right, and new margins established, before subsequent drawings are made.
### Notes: ###

# Only a single translation, along a specified axis, can be accomplished by a single SLIDE statement. More complex reorientations can be achieved by successive SLIDE and TURN statements.
# The units for "distance" are length units of translation of the picture center; translations are positive when the picture center is to be moved in the positive sense of the "axis". Units are those of the system model, not those of the graphics screen.
## The TURN Statement ##
The TURN statement requests that future pictures be rotated with respect to the graphic display screen and viewed from a new orientation.
### Format: ###
TURN (axis) = angle where "axis" can be any of the keywords: X, Y, or Z, indicating a rotation about the horizontal, vertical, or normal axis of the graphic display screen, respectively, and where "angle" is the numeric value, in degrees, of the counter-clockwise angle by which the picture should be rotated from its current orientation.
### Example: ###
TURN (Z) = 90 specifies that future pictures are to be rotated in the view frame, about the center of the picture, by 90 degrees counterclockwise.
### Notes: ###

# Only a single rotation, about a specified "axis", can be accomplished by a single TURN statement. More complex reorientations can be achieved by successive TURN and SLIDE statements.
# All rotations take place about the center of the graphic display screen.
## The STORE VIEW Statement ##
The STORE VIEW statement requests that the parameters defining the current viewing orientation and scale be stored on a file for later use.
### Format: ###
STORE VIEW
### Notes: ###

# The STORE VIEW statement does not alter the current viewing parameters, but merely saves them for future use.
# The visibility of various links, axes, etc. is not stored by the STORE VIEW statement, only the view orientation, scale, and centering parameters.
# The first time that a STORE VIEW or RECALL VIEW statement is issued, IMP prompts the user to interactively input the filename to be used to store the viewing parameters. This may be a new filename, or the name of a file used in other IMP jobs. It is treated as a direct access file and cannot be edited, printed, or otherwise used except by this or another IMP job.
# After attaching the proper filename, IMP interactively prompts the user to enter a "view number" and a "title" for the current view. Any unused view number between one and fifteen may be used. If unsure, the user may reply with a "view number" of zero to see a catalog of currently used view numbers and titles already stored in the file. The seven standard "view titles" (FRONT, BACK, TOP, BOTTOM, LEFT, RIGHT, and ISOMETRIC) should not be specified.
## The RECALL VIEW Statement ##
The RECALL VIEW statement requests that the current view orientation and scaling parameters be replaced by a former set which have been previously saved on file by a STORE VIEW statement.
### Format: ###
RECALL VIEW
### Notes: ###

# The visibility of various links, axes, etc. is not changed by the RECALL VIEW statement, only the view orientation, scaling, and centering parameters.
# The first time that a STORE VIEW or RECALL VIEW statement is issued, IMP prompts the user to interactively input the filename to be used to store the viewing parameters. This may be the name of a file used in other IMP jobs. It is treated as a direct access file and cannot be edited, printed, or otherwise used except by this or another IMP job.
# After attaching to the proper filename, IMP interactively prompts the user to enter a "view number" for the desired view. Any stored "view number" between one and fifteen may be used. If unsure, the user may reply with a "view number" of zero to see a catalog of currently used "view numbers" and "titles" already stored in the file. The seven standard views (FRONT, BACK, TOP, BOTTOM, LEFT, RIGHT, and ISOMETRIC) usually available from the DATA VIEW statement can also be obtained with the RECALL VIEW statement by supplying a "view number" between -1 and -7, respectively.
## The DELETE VIEW Statement ##
The DELETE VIEW statement requests the deletion from the stored view file of one of the sets of viewing parameters previously stored by a STORE VIEW statement.
### Format: ###
DELETE VIEW
### Notes: ###

# The first time that a STORE VIEW or RECALL VIEW statement is issued, IMP prompts the user to interactively input the filename to be used for the viewing parameters. This may be a new filename, or the name of a file used in other IMP jobs. It is treated as a direct access file and cannot be edited, printed, or otherwise used except by this or another IMP job.
# After attaching to the proper filename, IMP interactively prompts the user to enter a "view number" for the view to be deleted. Any stored "view number" between one and fifteen may be used. If unsure, the user may reply with a "view number" of zero to see a catalog of currently used "view numbers" and "titles" already stored in the file. The seven standard views (FRONT, BACK, TOP, BOTTOM, LEFT, RIGHT, and ISOMETRIC) having "view numbers" between -1 and -7, respectively, may not be deleted.