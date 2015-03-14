# Chapter 7: DELETE Statements #
The various DELETE statements recognized by the IMP interpreter are presented in this chapter. DELETE statements are used to delete previously defined features or components and all other features, components, or data dependent on them from the system model. Each DELETE statement begins with the keyword DELETE followed by a separator; the second word of the statement is also a keyword and directs IMP to interpret the remainder of the statement according to one of the following formats:

## The DELETE TITLE Statement ##
The DELETE TITLE statement requests the deletion of the title assigned to the model by a previous TITLE statement.
### Format: ###
DELETE TITLE
### Notes: ###

# It is not necessary to delete the previously defined title before a new title is defined; see note (2) with the TITLE statement.
## The DELETE VALUE Statement ##
The DELETE VALUE statement requests the deletion of one or more specified VALUE statements from the IMP memory.
### Format: ###
DELETE VALUE (name, name, ... ) where each "name" is the alphanumeric "name" defined by a previous VALUE statement.
### Example: ###
DELETE VALUE (FUNC X FofX) requests that the previous VALUE statements defining values named FUNC, X, and FofX be deleted from the IMP system memory.
### Notes: ###

# Each "name" must be separated from others by valid separators, usually commas or blanks.
# No more than 33 "names" may be specified in a single DELETE VALUE statement.
# Each "name" must be defined by a previous VALUE statement. If not, the undefined "name" is ignored and a message is printed.
# Other VALUE statements which depend on this VALUE "name" for their definitions are not deleted; their values become undefined until a new VALUE statement is given defining a VALUE with the same "name".
# The keyword ALL may be used as a "name" and requests that all previously defined VALUE names be deleted.
## The DELETE SOLID Statement ##
The DELETE SOLID statement requests the deletion of specified geometric solids from the links of the system model.
### Format: ###
DELETE SOLID (name, name, ... ) where each "name" is the alphanumeric "name" of a solid to be deleted.
### Example: ###
DELETE SOLID (KNOB SHAFT) requests that the solids named KNOB and SHAFT be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE SOLID statement.
# Each "name" must be defined by a file referenced in a previous SOLID READ statement. If not, the undefined "name" is ignored and a message is printed.
# The keyword ALL may be used as a "name" and requests that all previously defined solids be deleted.
# Deleting one or more solids from a link does not cause recalculation of the mass properties of that link. Therefore, that link's mass properties become poorly defined and should be reestablished by new DATA MASS and DATA INERTIA statements and/or by new SHAPE and DATA DENSITY statements.
## The DELETE CONTACT Statement ##
The DELETE CONTACT statement requests the deletion of the specified contact association between solids of different links by which they are monitored for possible collision.
### Format: ###
DELETE CONTACT (name, name, ... ) where each "name" is the alphanumeric "name" of a previously defined contact to be deleted.
### Example: ###
DELETE CONTACT (HIT BOUNCE) requests that the contacts named HIT and BOUNCE be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE CONTACT statement.
# Each "name" must be defined by a file referenced in a previous CONTACT statement. If not, the undefined "name" is ignored and a message is printed.
# The keyword ALL may be used as a "name" and requests that all previously defined contacts be deleted.
## The DELETE LINK Statement ##
The DELETE LINK statement requests the deletion of specified links and all information dependent on them from the system model.
### Format: ###
DELETE LINK (name, name, ... ) where each "name" is the alphanumeric "name" of a link to be deleted.
### Example: ###
DELETE LINK (BAR LK2 BASE) requests that the links named BAR, LK2, and BASE and all information dependent on them be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE LINK statement.
# Each "name" must be defined by a previous LINK statement or a statement defining a joint. If not, the undefined "name" is ignored and a message is printed.
# Extreme caution should be exercised in the use of the DELETE LINK statement since almost all other items are, at least remotely, dependent on the links and, therefore, may also be deleted.
# The joints attached to a link are treated as dependent on the link and are deleted with the link.
# If the stationary link of the system is deleted, its "name" (or the default "name", BASE) is still retained from the previous GROUND statement. A new GROUND statement must be given or another link must be defined having this "name" before an EXECUTE or EXECUTE HOLD statement is given.
# The "name" of a deleted link is not deleted from the various PRINT or other request statements. This may be done sepaDELETE Statements rately, for example, with the DELETE PRINT statement.
# The keyword ALL may be used as a "name" and requests that all previously defined links be deleted.
## The DELETE JOINT Statement ##
The DELETE JOINT statement requests the deletion of specified joints and all information dependent on them from the system model.
### Format: ###
DELETE JOINT (name, name, ... ) where each "name" is the alphanumeric name of a joint to be deleted.
### Example: ###
DELETE JOINT (PIN1 BALL) requests that the joints named PIN1 and BALL and all information dependent on them be deleted from the system model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE JOINT statement.
# Each "name" must be defined by a previous joint definition statement. If not, the undefined "name" is ignored and a message is printed.
# Extreme caution should be exercised in the use of the DELETE JOINT statement since many other items are defined at least remotely dependent on the joints and, therefore, may also be deleted.
# The links attached by a joint are not treated as dependent on the joint and are not deleted with the joint. Once all joints on a link are deleted, however, the link should also be deleted by a DELETE LINK statement. If not, this will be done automatically when an EXECUTE or EXECUTE HOLD statement is given.
# The "name" of a deleted joint is not deleted from the various PRINT or other request statements. This may be done with the DELETE PRINT statement, however.
# The keyword ALL may be used as a "name", and requests that all previously defined joints be deleted.
## The DELETE POINT Statement ##
The DELETE POINT statement requests the deletion of specified points and all information dependent on them from the system model.
### Format: ###
DELETE POINT (name, name, ... ) where each "name" is the alphanumeric name of a point to be deleted.
### Example: ###
DELETE POINT (A PT2 Q) requests that the points named A, PT2, and Q and all information dependent on them be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE POINT statement.
# Each "name" must be defined by a previous POINT statement. If not, the undefined "name" is ignored and a message is printed.
# Caution should be exercised in the use of the DELETE POINT statement since other items such as springs, forces, torques, or dampers may be dependent on them and, therefore, may also be deleted.
# The "name" of a deleted point is not deleted from PRINT or other request statements. This may be done separately with the DELETE PRINT statement, however.
# The keyword ALL may be used as a "name", and requests that all previously defined points be deleted.
## The DELETE GRAVITY Statement ##
The DELETE GRAVITY statement requests the deletion of the gravity vector from the system model.
### Format: ###
DELETE GRAVITY
### Notes: ###

# This statement eliminates the effects of a previous DATA GRAVITY statement, but not the dynamic effects of the inertia of the moving links. A DELETE MASS statement may be used for that purpose.
# It is not necessary to delete the gravity vector in order to specify new data for it; see note (3) of the DATA GRAVITY statement.
## The DELETE MASS Statement ##
The DELETE MASS statement requests the deletion of the data defining the mass, the center of mass location, and the mass moments and products of inertia of specified links from the system model.
### Format: ###
DELETE MASS (name, name, ... ) where each "name" is the alphanumeric name of a link for which the mass data are to be deleted.
### Example: ###
DELETE MASS (ROD BAR) requests that the mass data for the links named ROD and BAR be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE MASS statement.
# Each "name" must refer to a link which was given mass data by a previous DATA MASS or DATA DENSITY statement. If not, the improper "name" is ignored and a message is printed.
# Care must be taken when "name" refers to a link which was given mass by a previous DATA DENSITY statement since this also eliminates the mass properties of other shapes of the same link which may have been defined by other DATA DENSITY statements.
# The keyword ALL may be used as a "name", and requests that all previously defined mass data be deleted from the system model.
# The DELETE MASS statement eliminates the components of static force due to gravity as well as the dynamic forces resulting from the inertia of the deleted masses. These effects can be achieved individually by deleting the gravity vector or the input motions.
# It is not necessary to delete the mass properties of a link in order to redefine their data; see the DATA DENSITY statement, note 7), the DATA MASS statement, note 7), and the DATA INERTIA statement, note 7).
## The DELETE SPRING Statement ##
The DELETE SPRING statement requests the deletion of specified springs and associated data from the system model.
### Format: ###
DELETE SPRING (name, name, ... ) where each "name" is the alphanumeric name of a spring or a joint which contains a spring which is to be deleted.
### Example: ###
DELETE SPRING (PIN PULL) requests that the spring rate within the revolute joint named PIN and the spring named PULL be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE SPRING statement.
# Each "name" must have appeared in a previous DATA SPRING statement; if not, the improper "name" is ignored and a message is printed.
# The keyword ALL may be used as a "name", and requests that all previously defined springs and all spring rates acting with joint variables be deleted.
# The "name" of a deleted spring is not deleted from the various PRINT or other request statements. This may be done separately with the DELETE PRINT statement, however.
# It is not necessary to delete a spring in order to redefine its data; see the DATA SPRING statement, note 4).
# If "name" refers to a joint, then the spring rates associated with all joint variables of that joint are deleted.
## The DELETE DAMPER Statement ##
The DELETE DAMPER statement requests the deletion of specified dampers and associated data from the system model.
### Format: ###
DELETE DAMPER (name, name, ... ) where each "name" is the alphanumeric name of a damper or a joint which contains a damper which is to be deleted.
### Example: ###
DELETE DAMPER (PIN SLOW) requests that the damping rate within the revolute joint named PIN and the damper named SLOW be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE DAMPER statement.
# Each "name" must have appeared in a previous DATA DAMPER statement; if not, the improper "name" is ignored and a message is printed.
# The keyword ALL may be used as a "name", and requests that all previously defined dampers and all damping rates acting with joint variables be deleted.
# The "name" of a deleted damper is not deleted from the various PRINT or other request statements. This may be done separately with the DELETE PRINT statement, however.
# It is not necessary to delete a damper in order to respecify its data; see the DATA DAMPER statement, note 4).
# If "name" refers to a joint, then the damping rates associated with all joint variables of that joint are deleted.
## The DELETE FORCE Statement ##
The DELETE FORCE statement requests the deletion of specified applied forces and associated data from the system model.
### Format: ###
DELETE FORCE (name, name, ... ) where each "name" is the alphanumeric name of an applied force or a joint which contains an applied force which is to be deleted.
### Example: ###
DELETE FORCE (SLIP PULL) requests that the force applied within the prismatic joint named SLIP and the applied force named PULL be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE FORCE statement.
# Each "name" must have appeared in a previous DATA FORCE or DATA TORQUE statement; if not, the improper "name" is ignored and a message is printed.
# The keyword ALL may be used as a "name", and requests that all previously defined applied forces and torques and all forces and torques applied within joint variables be deleted.
# It is not necessary to delete an applied force or torque in order to respecify its data; see the DATA FORCE statement, note 4), and the DATA TORQUE statement, note 4).
# If "name" refers to a joint, then all applied forces and torques associated with the joint variables of that joint are deleted.
## The DELETE TORQUE Statement ##
The DELETE TORQUE statement requests the deletion of specified applied torques and associated data from the system model.
### Format: ###
DELETE TORQUE (name, name, ... ) where each "name" is the alphanumeric name of an applied torque or a joint which contains an applied torque which is to be deleted.
### Example: ###
DELETE TORQUE (PIN TURN) requests that the torque applied within the revolute joint named PIN and the applied torque named TURN be deleted from the model.
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE TORQUE statement.
# Each "name" must have appeared in a previous DATA FORCE or DATA TORQUE statement not, the improper "name" is ignored and a message is printed.
# The keyword ALL may be used as a "name", and requests that all previously defined applied forces and torques and all forces and torques applied within joint variables be deleted.
# It is not necessary to delete an applied force or torque in order to respecify its data; see the DATA FORCE statement, note 4), and the DATA TORQUE statement, note 4).
# If "name" refers to a joint, then all applied forces and torques associated with the joint variables of that joint are deleted.
## The DELETE INPUT Statement ##
The DELETE INPUT statement requests the deletion for specified joints of any data defined by previous DATA POSITION, DATA VELOCITY, DATA ACCEL, and DATA MOTION statements, and deletion of the designation of the associated joint variables as specified generalized coordinates (SGCs).
### Format: ###
DELETE INPUT (name, name, ... ) where each "name" is the alphanumeric name of a joint for which a previous DATA MOTION or DATA POSITION, DATA VELOCITY, and/or DATA ACCEL statements have designated an input motion.
### Example: ###
DELETE INPUT (PIN SLIP) requests that the previous DATA MOTION or DATA POSITION, DATA VELOCITY, and DATA ACCEL statements for the joints named PIN and SLIP be deleted and that they no longer be designated as specified generalized coordinates (SGCs).
### Notes: ###

# No more than 33 "names" may be specified in a single DELETE INPUT statement.
# Each "name" must have appeared in a previous DATA POSITION or DATA MOTION statement; if not, the improper "name" is ignored and a message is printed.
# It is not necessary to delete an SGC in order to respecify its data; see the DATA POSITION statement, note 7), and the DATA MOTION statement, note 5).
# The DATA VELOCITY and DATA ACCEL statements for a particular joint cannot be deleted separately; the DELETE INPUT statement must be used, and pertinent data respecified.
# The keyword ALL may be used as a "name", and requests the deletion of all SGC data. However, this has the additional side effect of deleting the current mode of the simulation if kinematic; see DELETE INPUT (ALL).
## The DELETE MOTION Statement ##
The DELETE MOTION statement requests the deletion of the motion input information for specified joints and the deletion of the designation of those joints as specified generalized coordinates (SGCs).
### Format: ###
DELETE MOTION (name, name, ... ) where each "name" is the alphanumeric name of a joint for which a previous DATA MOTION statement has designated an input motion now to be deleted.
### Example: ###
DELETE MOTION (PIN, SLIP) requests that the previous DATA MOTION statements for the joints named PIN and SLIP be deleted, and that they no longer be designated as specified generalized coordinates (SGCs).
### Notes: ###

# No more than 33 "names" may be specified in a single DATA MOTION statement.
# Each "name" must have appeared in a previous DATA MOTION or DATA POSITION statement; if not, the improper "name" is ignored and a message is printed.
# It is not necessary to delete an input motion in order to respecify its data; see the DATA MOTION statement, note 5), and the DATA POSITION statement, note 7).
# When the specified joint has multiple joint variables, input motions are deleted for all joint variables of that joint.
# The keyword ALL may be used as a "name", and requests that all previously defined input motions be deleted from the model.
## The DELETE IC Statement ##
The DELETE IC statement requests the deletion of the dynamic initial conditions for specified joints of the system.
### Format: ###
DELETE IC (name, name, ... ) where each "name" is the alphanumeric name of a joint for which the initial conditions are to be deleted.
### Example: ###
DELETE IC (PIN SLIP) requests that the previously defined initial conditions for the joints named PIN and SLIP be deleted.
### Notes: ###

# No more than 33 "names" may be specified in a single DATA IC statement.
# Each "name" must have appeared in a previous DATA IC statement; if not, the improper "name" is ignored and a message is printed.
# It is not necessary to delete an initial condition in order to respecify its data; see the DATA IC statement, note 6).
# When the specified joint has multiple joint variables, initial conditions are deleted for all joint variables of that joint.
# The keyword ALL may be used as a "name", and requests that all previously defined initial conditions be deleted.
## The DELETE PRINT Statement ##
The DELETE PRINT statement is used to delete requests made by previous PRINT statements.
### Format: ###
DELETE PRINT (kind, kind, ... ) where each "kind" is one of the keywords: HEADING, VALUE, POSITION, VELOCITY, ACCEL, FORCE, FREQUENCY, or DYNAMICS.
### Example: ###
DELETE PRINT (FORCE ACCEL) requests that previous requests made by PRINT FORCE and PRINT ACCEL statements be deleted.
### Notes: ###

# Each "kind" must correspond to a previous PRINT statement using the same keyword; if not, the improper "kind" is ignored and a message is printed.
# Each "kind" requests the deletion of all previous PRINT statements of that "kind" with their entire lists of names. A reduced list of names may only be achieved by deleting the entire PRINT statement and respecifying it.
# The keyword ALL may be used as a "kind", and requests the deletion of all previous PRINT statements, irrespective of their "kind".
## The DELETE LIST Statement ##
The DELETE LIST statement is used to delete requests made by previous LIST statements.
### Format: ###
DELETE LIST (kind, kind, ... ) where each "kind" is one of the keywords: VALUE, POSITION, VELOCITY, ACCEL, FORCE, or DYNAMICS.
### Example: ###
DELETE LIST (FORCE ACCEL) requests that all previous requests made by LIST FORCE and LIST ACCEL statements be deleted.
### Notes: ###

# Each "kind" must correspond to a previous LIST statement using the same keyword; if not, the improper "kind" is ignored and a message is printed.
# Each "kind" requests the deletion of all previous LIST statements of that "kind" with their entire lists of names. A reduced list of names may only be achieved by deleting the entire LIST statement and respecifying it.
# The keyword ALL may be used as a "kind", and requests the deletion of all previous LIST statements, irrespective of their "kind".
## The DELETE STORE Statement ##
The DELETE STORE statement is used to delete requests made by previous STORE statements.
### Format: ###
DELETE STORE (kind, kind, ... ) where each "kind" is one of the keywords: HEADING, VALUE, POSITION, VELOCITY, ACCEL, FORCE, or DYNAMICS.
### Example: ###
DELETE STORE (FORCE, ACCEL) requests that all previous requests made by STORE FORCE and STORE ACCEL statements be deleted.
### Notes: ###

# Each "kind" must correspond to a previous STORE statement using the same keyword; if not, the improper "kind" is ignored and a message is printed.
# Each "kind" requests the deletion of all previous STORE statements of that "kind" with their entire lists of names. A reduced list of names may only be achieved by deleting the entire STORE statement and respecifying it.
# The keyword ALL may be used as a "kind", and requests the deletion of all previous STORE statements, irrespective of their "kind".