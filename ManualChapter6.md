# Chapter 6: Control Statements #
The various control statements recognized by the IMP interpreter are presented in this chapter. Control statements are used to set the mode of the simulation and to allow the user to guide the actions performed by the IMP system. The first word of each control statement instructs the IMP system to interpret the remainder of the statement according to one of the formats on the following pages:

## The REMARK Statement ##
The REMARK statement is used to embed comments in an IMP simulation model for documentation. It is ignored by the IMP interpreter and has no effect on the simulation.
### Format: ###
REMARK comment
### Examples: ###
REMARK PROTOTYPE SUSPENSION ANALYSIS REMARK J. J. UICKER, JR. $ JUNE 1, 1995
### Notes: ###

# Comments may be imbedded within an IMP model in either of two ways: either as imbedded remarks (see Section 2-2.3), or by use of the REMARK statement.
# The REMARK statement is ignored, but is printed with the output if the PRINT INPUT statement is in effect.
# A REMARK statement may contain continuation lines (see second example above), but must not contain more than 35 words as determined by counting IMP separators.
## The CLEAR Statement ##
The CLEAR statement causes the IMP memory to be cleared and initialized for a new simulation model.
### Format: ###
CLEAR
### Notes: ###

# It is not necessary to use the CLEAR statement at the beginning of the first simulation model; the memory is automatically cleared when IMP is initialized.
# The echo of input data caused by PRINT INPUT or lack of such caused by DELETE PRINT INPUT is not reinitialized; also the type of terminal specified by a DEVICE statement is not reset by the CLEAR statement.
## The TITLE Statement ##
The TITLE statement assigns an alphanumeric title to the system being simulated. This title is used in the heading of printed results.
### Format: ###
TITLE = string where "string" is an arbitrarily selected alphanumeric title of 63 or fewer characters.
### Example: ###
TITLE: PROTOTYPE SUSPENSION SIMULATION
### Notes: ###

# Use of the TITLE statement is optional. If it is not included before the EXECUTE or EXECUTE HOLD statement, however, the default title appears in the banner above the printed results.
# The TITLE statement may be used more than once. If so, only the most recent "string" assigned is in effect at any time. This feature is useful, for example, in distinguishing between similar simulation results with modified data; a new "title" may be assigned after each EXECUTE or EXECUTE HOLD statement.
# Continuation lines (the $ character), end of statement (the $$ character), and imbedded remarks may not be used within a TITLE statement.
## The EXECUTE Statement ##
The EXECUTE statement initiates the actual performance of the simulation and requests that the model be returned to its original configuration upon completion.
### Format: ###
EXECUTE
### Notes: ###

# This statement or the EXECUTE HOLD statement must be used to cause any type of simulation to be performed. All other IMP statements do not cause simulation, but only specify the model and the types of results desired when simulation is initiated.
# This statement may be repeated as often as desired, making model changes by new statements between simulations.
# After a simulation is completed, the system model data is reset to the configuration corresponding to the data at the beginning of the simulation, and TIME is reset to zero.
## The EXECUTE HOLD Statement ##
The EXECUTE HOLD statement initiates the actual performance of a simulation and requests that the model remain in its final configuration when the simulation is completed.
### Format: ###
EXECUTE HOLD
### Notes: ###

# This statement or the EXECUTE statement must be used to cause any type of simulation to be performed. All other IMP statements do not cause simulation, but only specify the model and the types of results desired when simulation is initiated.
# This statement may be repeated as often as desired, making model changes by new statements between simulations.
# After a simulation is completed, the system model data remains at the last valid configuration achieved in the simulation. A message is printed indicating that the "reference position" for any subsequent data has been changed to the new configuration.
# After an EXECUTE HOLD simulation has been completed, the value of TIME is not reset to zero. Therefore, a subsequent EXECUTE or EXECUTE HOLD statement causes the simulation to continue from the end of the previous simulation. The value of TIME is reset to zero, however, at the end of an EXECUTE (without HOLD) simulation or when a RESET statement is issued.
## The RESET Statement ##
The RESET statement can be used after an EXECUTE HOLD statement as another method to reset time to zero.
### Format: ###
RESET
### Notes: ###

# The EXECUTE HOLD statement can be used to cause a simulation to halt and to return control to the user. This allows changing the system model and continuing the simulation from that state by issuing another EXECUTE or EXECUTE HOLD statement. For this reason, TIME is not set back to zero upon completion of an EXECUTE HOLD simulation.
# Sometimes, however, the user might wish to use the EXECUTE HOLD statement in order to leave the system model in a different configuration at the end of simulation, but wishes to continue modeling from there as if no simulation had yet happened. In such a case the EXECUTE HOLD statement has the disadvantage that it does not set TIME back to zero.
# The purpose of the RESET statement is to overcome the difficulty of note 2). If issued after the completion of an EXECUTE HOLD statement, the RESET statement sets TIME to zero.
## The DELETE INPUT (ALL) Statement ##
The DELETE INPUT (ALL) statement is used to delete all SGC and FGC definitions and to cancel kinematic or static mode.
### Format: ###
DELETE INPUT (ALL)
### Notes: ###

# When no FIND EQUILIB or FIND DYNAMICS statement has been given and an EXECUTE or EXECUTE HOLD statement has been performed the simulation model is, by default, locked into kinematic mode. In order to cancel kinematic or static mode, so that a FIND EQUILIB or FIND DYNAMICS statement may be given, it is necessary to use the DELETE INPUT (ALL) statement.
# The DELETE INPUT (ALL) statement deletes the definitions and data of all previous DATA POSITION, DATA VELOCITY, DATA ACCEL, and DATA MOTION statements, so that no SGCs are defined upon completion. It also eliminates any IMP chosen FGCs from any previous EXECUTE or EXECUTE HOLD statements.
# When a DELETE INPUT (ALL) statement is encountered, the simulation mode becomes undefined. The next EXECUTE or EXECUTE HOLD statement is again performed in kinematic mode by default unless another mode is requested.
## The FIND EQUILIB Statement ##
The FIND EQUILIB statement requests that the simulation be performed in static (equilibrium) mode and that, after all SGCs have been set to their assigned positions, any remaining degrees of freedom (FGCs) should be adjusted to achieve a configuration of minimum potential energy (static equilibrium) for the system.
### Format: ###
FIND EQUILIB
### Notes: ###

# This statement must appear before the EXECUTE or EXECUTE HOLD statement if static mode simulation is desired. Otherwise the simulation is performed in kinematic mode (or the previously defined mode).
# A maximum of 25 search steps is taken in seeking an equilibrium configuration. If equilibrium conditions are not satisfied within these 25 steps, the search is halted, the simulation is terminated, and a message is printed.
# If a DATA POSITION or DATA MOTION statement is specified in combination with the FIND EQUILIB statement, an appropriate force or torque is assumed to be applied at that SGC such that the specified position is one of static equilibrium even though no DATA FORCE statement has been given.
# If it is possible to move the system (or any part of it) in such a way that the potential energy is not changed, then the system is in a position of neutral equilibrium. In such a case, IMP searches for a position with no net unbalanced forces or torques at any of the FGCs. Any such position found is an equilibrium position and allows the simulation to continue. However, in such a case, much less information is available to guide the search and it is often impossible to find an equilibrium position to the accuracy required within the 25 search steps allowed.
# The FIND EQUILIB statement may not be used if a DATA VELOCITY or DATA ACCEL statement has been specified since the simulation is then in kinematic mode. If this is attempted, the FIND EQUILIB statement is ignored and a message is printed. To switch to static mode, the kinematic mode must first be canceled by use of the DELETE INPUT (ALL) statement; the FIND EQUILIB statement may then be given and any previous SGC position data may again be specified by DATA POSITION or DATA MOTION statements.
# The FIND EQUILIB statement may not be used if a FIND DYNAMICS statement has been specified since the simulation is then in dynamic mode. If this is attempted, the FIND EQUILIB statement is ignored and a message is printed. To switch to static mode in this case, the dynamic mode must first be canceled by use of the DELETE DYNAMICS statement; the FIND EQUILIB statement may then be given and SGC position data may again be specified by DATA POSITION or DATA MOTION statements.
# All DAMPER and DATA DAMPER statements have no effect when the simulation is in static mode; however, they are not in error and no message is printed.
## The DELETE EQUILIB Statement ##
The DELETE EQUILIB statement can be used to cancel the static mode and to delete all SGC definitions and associated data.
### Format: ###
DELETE EQUILIB
### Notes: ###

# This statement must be preceded by a FIND EQUILIB statement; if not, the statement is ignored and a message is printed.
# This statement also deletes the definitions and data of all previous DATA POSITION and DATA MOTION statements, so that no SGCs are defined upon completion.
# When a DELETE EQUILIB statement is encountered the simulation mode becomes undefined. The next EXECUTE or EXECUTE HOLD statement is performed in kinematic mode by default unless another mode is requested.
## The FIND DYNAMICS Statement ##
The FIND DYNAMICS statement requests that any subsequent simulation be performed in dynamic (time response) mode. Upon starting the simulation, all specified DATA IC data are applied and the specified SGCs are driven according to the DATA MOTION statements; the DATA FORCE and DATA TORQUE data are applied; and the dynamic equations of motion are formulated and integrated to determine the motion of the system.
### Format: ###
FIND DYNAMICS
### Notes: ###

# This statement must appear before the EXECUTE or EXECUTE HOLD statement if a dynamic mode simulation is desired. Otherwise the simulation is performed in kinematic mode (or the previously defined mode).
# The FIND DYNAMICS statement may not be used after a DATA POSITION statement or a FIND EQUILIB statement has been given since the simulation is then in either kinematic or static mode. If this is attempted, the FIND DYNAMICS statement is ignored and a message is printed. The previous mode may be canceled by use of the DELETE INPUT (ALL) or DELETE EQUILIB statement, and the FIND DYNAMICS statement may then be given.
# A DATA TIME statement must also be specified before the EXECUTE or EXECUTE HOLD statement if a FIND DYNAMICS statement has been given. If not, the simulation is terminated and a message is printed.
# An appropriate force or torque is assumed applied at each joint to achieve any specified initial conditions even though no DATA FORCE statement has explicitly been given.
# If the masses of some of the moving links have been ignored, and if it is possible to move the system (the FGCs) in such a way that only the massless links move, then time integration is impossible since the mass matrix is singular in such a model. If this in encountered, even instantaneously during the integration, the simulation is terminated and a message is printed.
# If it is possible to move some of the FGCs in such a way that the potential energy is not changed, then the stiffness matrix is singular and integration results should be viewed with suspicion. If this is encountered, even instantaneously during the integration, a warning message is printed but the simulation is continued.
## The DATA TIME Statement ##
The DATA TIME statement designates the final value of time through which a simulation is to be performed. It also specifies the minimum time increment for the step size and the time increment with which results are to be printed, listed or stored.
### Format: ###
DATA TIME = final time, min increment, print increment where "final time" is a positive numeric value specifying the time limit up to which the simulation should proceed. The "min increment" is a positive numeric value specifying the minimum time increment for a single time step, and "print increment" is a positive numeric value specifying the time increment between outputs of the requested simulation results.
### Example: ###
DATA TIME = 3.5, 0.005, 0.10 specifies that a simulation is to be carried out until time reaches 3.5 seconds, with a minimum time increment of 0.005 seconds, and with results being output after each 0.10 seconds.
### Notes: ###

# A DATA TIME statement must be specified before an EXECUTE or EXECUTE HOLD statement whenever the simulation is in dynamic mode. If not, the simulation is interrupted and a message is printed. If in kinematic or static mode, an appropriate DATA TIME statement will be set and message printed.
# If more than one DATA TIME statement is encountered, the later statement takes precedence and earlier data are replaced.
# The values of "final time", "min increment", and "print increment" have units of seconds.
# The values of "final time", "min increment", and "print increment" may not be negative; if one or more is, the statement is ignored and a message is printed.
# The values of "min increment" and "print increment" may not be zero; if either is, the statement is ignored and a message is printed.
## The ZERO (FORCE) Statement ##
The ZERO (FORCE) statement defines the force tolerances to be used in adjusting the time steps used in time integration for dynamic mode simulations.
### Format: ###
ZERO (FORCE) = force error, percent error where "force error" is the numeric value of the force tolerance to be treated as acceptable in any single time step and "percent error" is the same force tolerance expressed in percent of current force. The time integration step size is adjusted dynamically so that both of these criteria are achieved at each time step during dynamic mode integration.
### Example: ###
ZERO (FORCE) = 0.1, 1 specifies that, at each time step in a dynamic mode simulation, as the dynamic forces and torques at the SGCs are calculated, the time step will be set so that the inaccuracies in the dynamic forces and torques are not greater than 0.1 pounds or 1 percent of their current values.
### Notes: ###

# In most IMP simulations, the ZERO (FORCE) statement need not be used at all. If a ZERO (FORCE) statement is not entered before an EXECUTE or EXECUTE HOLD statement is encountered, and if the simulation is in dynamic mode, then default values of 0.1 "force error" and 1 "percent error", respectively, are used.
# The time steps used in dynamic mode time integration are continually adjusted to keep integration errors to less than the specified "force error" and "percent error" levels for each individual time step. However, it must be remembered that most time steps will have much less than this amount of error and that error does not propagate to the next time step except in unusual cases. The "force error" specified should not be specified smaller than necessary for the total force accuracy required by the application.
# If more than one ZERO (FORCE) statement is encountered, the later statement takes precedence; earlier data are replaced and a message is printed.
# The values of "force error" and "percent error" may not be zero or negative; if they are, the statement is ignored and a message is printed.
# The "force error" value is used to check both forces and torques, and has dimensions of force or force length.
## The DELETE DYNAMICS Statement ##
The DELETE DYNAMICS statement is used to cancel the dynamic mode and to delete the DATA TIME statement, all SGC definitions, and associated data.
### Format: ###
DELETE DYNAMICS
### Notes: ###

# This statement must be preceded by a FIND DYNAMICS statement; if not, the statement is ignored and a message is printed.
# This statement also deletes the definitions and data of all previous DATA MOTION and DATA TIME statements so that, upon completion, no SGCs are defined.
# When a DELETE DYNAMICS statement is encountered, the simulation mode becomes undefined. The next EXECUTE or EXECUTE HOLD statement is performed in kinematic mode by default unless another mode is requested.
## The END Statement ##
The END statement indicates the end of an IMP simulation, and returns control from IMP to the operating system of the host computer.
### Format: ###
END
### Notes: ###

# This statement must be given at the end of every IMP simulation. It is the only way to exit from the IMP program.
## The PRINT INPUT Statement ##
The PRINT INPUT statement requests that subsequent IMP statements be printed with the output as they are read.
### Format: ###
PRINT INPUT
### Notes: ###

# When the IMP program is first initiated, the IMP statements are not automatically printed as they are entered.
# The PRINT INPUT statement has its primary use when it precedes or is included in the file for a RECALL INPUT statement. In this context it causes the statements read from the file to be printed with the output data.
# The PRINT INPUT statement is not printed with the output; however, subsequent statements are printed.
# The PRINT INPUT statement may be used to resume printing of IMP input statements at any point after a DELETE PRINT (INPUT) statement.
# A PRINT INPUT statement should not follow a STORE INPUT statement until a DELETE STORE (INPUT) statement has been given, since IMP cannot print with the output and in the STORE file simultaneously. If this is attempted, the statement is ignored and a message is printed.
## The DELETE PRINT (INPUT) Statement ##
The DELETE PRINT (INPUT) statement requests that subsequent IMP statements no longer be printed with the output as they are read.
### Format: ###
DELETE PRINT (INPUT)
### Notes: ###

# The DELETE PRINT (INPUT) statement is printed with the output; however, subsequent statements are not printed.
# The PRINT INPUT statement may be used to resume printing of IMP input statements at any point after a DELETE PRINT (INPUT) statement.
## The STORE INPUT Statement ##
The STORE INPUT statement requests that subsequent IMP statements be stored in a file as they are read.
### Format: ###
STORE INPUT = filename where "filename" specifies the name of the file in which the input statements are to be stored.
### Notes: ###

# The purpose of the STORE INPUT statement is to store the input statements of an IMP model in a specified file such that they may be reread by a future IMP program by use of the RECALL INPUT statement.
# The STORE INPUT statement halts the printing of IMP input statements with the output since IMP cannot print with the output and in the STORE file simultaneously. In this sense, it has the same effect as the DELETE PRINT (INPUT) statement.
# Subsequent IMP input statements are stored until a DELETE STORE INPUT, an EXECUTE, an EXECUTE HOLD, a RETURN, an END, or a CLEAR statement is encountered. In this sense, each of these statements has the same effect as a DELETE STORE (INPUT) statement.
# The STORE INPUT statement itself is not stored; however, subsequent statements are stored.
# It is the user's responsibility to insure that the "filename" specified refers to a new or reusable file, and that older useful information in that file is not lost. If a "filename" is not supplied on the initial STORE INPUT statement, and if execution is interactive, then the user is prompted to enter a "filename".
# If a previous STORE INPUT statement has been discontinued by a DELETE STORE (INPUT), an EXECUTE, an EXECUTE HOLD, a RETURN, or a CLEAR statement, and it is desirable to store further IMP input statements as a continuation of the previous file, then another STORE INPUT statement may be issued without specifying a "filename". The same "filename" will then be continued. However, in such a case, if the same "filename" is specified again in the later STORE INPUT statement, the file will be rewound and written over from the beginning.
## The DELETE STORE (INPUT) Statement ##
The DELETE STORE (INPUT) statement requests that subsequent IMP statements no longer be stored on file as they are encountered.
### Format: ###
DELETE STORE (INPUT)
### Notes: ###

# If a STORE INPUT statement has been previously specified, the IMP input statements are being stored on a file as they are read. The DELETE STORE (INPUT) statement discontinues this process.
# If a STORE INPUT statement has been previously specified, the DELETE STORE (INPUT) statement is stored on the file as well. This DELETE STORE (INPUT) statement, however, is backspaced over and overwritten with a RETURN statement. If these IMP statements are reread from the file by a RECALL INPUT statement in a future IMP program, each RETURN statement in the file causes reading to revert to the standard input device.
## The RETURN Statement ##
When this statement is read from a file by use of the RECALL INPUT statement, it requests IMP to revert to the standard input device for reading of further IMP input statements.
### Format: ###
RETURN
### Notes: ###

# When the file being read by a RECALL INPUT statement has been created by a STORE INPUT statement in a previous IMP program, the file has a RETURN statement as its last statement (assuming that the previous program terminated normally). If the user has prepared a file of IMP input statements to be read by use of the RECALL INPUT statement, the last line of this file must also contain a RETURN statement.
# The IMP input statements stored on the file should not include a CLEAR, a STORE INPUT, a RECALL INPUT, an EXECUTE, or an EXECUTE HOLD statement.
## The RECALL INPUT Statement ##
The RECALL INPUT statement requests that IMP input statements be read from a previously prepared file.
### Format: ###
RECALL INPUT = filename where "filename" specifies the name of the prepared file.
### Notes: ###

# When a RECALL INPUT statement is encountered, the reading of subsequent IMP input statements is attempted from the file rather than the standard input device. Reading continues from this file until a RETURN statement is encountered. The RETURN statement causes reading to revert to the standard input device. The file should end with a RETURN statement whether prepared by a previous IMP program (see STORE INPUT statement) or prepared separately by the user.
# The IMP input statements stored in the file should not include the CLEAR, the STORE INPUT, the RECALL INPUT, the EXECUTE, or the EXECUTE HOLD statements.
# If, for the first RECALL INPUT statement encountered while executing interactively and no filename is specified, IMP prompts the user for a filename. On subsequent RECALL INPUT statements with no filename specified, IMP continues reading after the last RETURN statement encountered in the file used in the previous RECALL INPUT statement. If RECALL INPUT = "filename" is entered again using the same or a new "filename", then IMP starts at the top of the named file.
# If the specified "filename" does not exist or cannot be used the RECALL INPUT statement is ignored; a message is printed.
## The UNIT (MASS) Statement ##
The UNIT (MASS) statement defines the factor which is used to convert the chosen mass units to those consistent with the force, length, and time units being used.
### Format: ###
UNIT (MASS) = value where "value" is the numeric value for a unit mass expressed in the user's force, length, and time units.
### Examples: ###
UNIT (MASS) = 0.0025901 specifies that the user wishes to enter mass data in units of pounds mass and that one pound mass is equivalent to 0.0025901 pounds force seconds squared per inch. UNIT (MASS) = 1.0 specifies that the mass data will be entered in kilograms and that one kilogram is equal to one Newton seconds squared per meter. UNIT (MASS) = 0.031081 specifies that mass data will be expressed in slugs and that one slug is equal to 0.03181 pound seconds squared per foot. This assumes that all length data are given in feet.
### Notes: ###

# All calculations in IMP assume that data are entered in a single consistent set of units. The units of angles are always in degrees, though their time derivatives are in radians per second. Time is always expressed in seconds. The user is free to choose any length and force units desired as long as they are used consistently throughout. The only internal unit dependence in IMP is in using mass units which are convenient for the user and also are consistent with those used for force, length, and time. Providing this is the purpose of the UNIT (MASS) statement.
# The "value" is only used in reading data from the DATA DENSITY, DATA MASS, and DATA INERTIA statements and in converting mass units to consistent internal units of force seconds squared per length. Since this conversion takes place as DATA DENSITY, DATA MASS, and DATA INERTIA statements are entered, any UNIT (MASS) statement must be entered before any DATA DENSITY, DATA MASS and DATA INERTIA statements are entered.
# If no UNIT (MASS) statement is used, then the default value of 0.0025901 is assumed. Thus, under default conditions, the user is assumed to be using US Customary units (pounds force, pounds mass, inches, and seconds).
# If more than one UNIT (MASS) statement is encountered, the later statement takes precedence and the earlier conversion factor is replaced. Previous DATA DENSITY, DATA MASS, and DATA INERTIA data are not recalculated, however.
# The "value" must be greater than zero. If not a message is printed and the UNIT (MASS) statement is ignored.
## The PRINT ON Statement ##
The PRINT ON statement requests that subsequent information printed on the terminal also be recorded in a file for later hardcopy printing.
### Format: ###
PRINT ON = filename where "filename" specifies the name of the file to be used for later printing.
### Example: ###
PRINT ON = ANALYS.LST
### Notes: ###

# When a PRINT ON statement is encountered, the "filename" is stored and opened to receive information. From this point forward, all information printed on the terminal is also duplicated in that file for later off-line printing. Duplication of printed information in this file continues until the end of the IMP job or until explicitly stopped by a PRINT OFF statement.
# If no "filename" is encountered on the first PRINT ON statement while executing interactively, IMP prompts the user for a "filename". If executing in background mode, the default "filename" of "prt.dat" is used.
# After a previous PRINT ON statement has been interrupted by a PRINT OFF statement, printing can be continued again by another PRINT ON statement without a "filename". If a PRINT ON statement is encountered without a "filename", the "filename" from the previous PRINT ON statement is continued from where it was left.
# If a "filename" is given and is distinct from the "filename" of a previous PRINT ON statement, the former file is ended and subsequent information begins on the later named file. If the same "filename" is explicitly named in more than one PRINT ON statement, the later PRINT ON statement causes the same file to be rewound and started again, thus causing previous information to be overwritten and lost.
# If the specified "filename" is invalid or cannot be used, the PRINT ON statement is ignored and a message is printed.
## The PRINT OFF Statement ##
The PRINT OFF Statement requests discontinuation of a previous PRINT ON statement.
### Format: ###
PRINT OFF
### Notes: ###

# If a previous PRINT ON statement has been issued and is still active, all printed information is being written in a file. The PRINT OFF statement discontinues writing in this file.
# The PRINT OFF statement discontinues printing in the file, but does not cause the "filename" to be forgotten or closed. Therefore, if a subsequent PRINT ON statement is issued without a "filename", printing continues at the current end of the file and no information is overwritten. If a subsequent PRINT ON statement is issued containing the same "filename", the file is rewound and previous information is overwritten and lost. If a subsequent PRINT ON statement contains a new "filename", the previous file is closed and the new information is printed on the later named file.
## The PAUSE ON Statement ##
The PAUSE ON statement requests that, during subsequent simulations, IMP pause at the completion of each time increment, each tabular listing, each graph (plot), and each schematic figure drawn to allow the user time to study the results before continuing.
### Format: ###
PAUSE ON
### Notes: ###

# The PAUSE ON statement causes no immediate effect at the time it is issued. The actual pause(s) occur(s) during the simulation invoked by a subsequent EXECUTE or EXECUTE HOLD statement.
# The PAUSE ON statement is totally ignored in background execution; PAUSE ON functions solely in interactive mode.
# Once the PAUSE ON statement has been issued, it remains active throughout the IMP session or until discontinued by a PAUSE OFF statement.
# If a PAUSE ON request is not active, tabular listings, graphs (plots), and animation drawings proceed in succession at the rate allowed by the host computer. This may cause results to be erased or scrolled off the screen before the user has had time to read or copy them.
# When an IMP session begins, the default setting for the flag is PAUSE OFF.
# If a PAUSE ON statement is encountered when the PAUSE flag is already set to ON, the statement is ignored.
## The PAUSE OFF Statement ##
The PAUSE OFF statement requests that IMP discontinue any previous PAUSE ON statement.
### Format: ###
PAUSE OFF
### Notes: ###

# When an IMP session begins, the default setting for the PAUSE flag is PAUSE OFF.
# The PAUSE OFF statement is totally ignored in background execution; it functions solely for interactive purposes.
# Once the PAUSE OFF statement has been set, it remains active throughout the IMP session or until discontinued by a PAUSE ON statement.
# If a PAUSE ON request is not active, tabular listings, graphs (plots), and animation drawings proceed in succession at the rate allowed by the host computer. This may cause results to be erased or scrolled off the screen before the user has had time to read or copy them.
# If a PAUSE OFF statement is encountered when the PAUSE flag is already set to OFF, the statement is ignored.
## The ERASE ON Statement ##
The ERASE ON statement requests that, during subsequent simulations, the screen be erased and a new page started at the completion of each tabular listing, each graph (plot), and each schematic figure drawn during animation.
### Format: ###
ERASE ON
### Notes: ###

# The ERASE ON statement causes no immediate effect at the time it is issued. The actual screen erasure(s) occur during the simulation invoked by a subsequent EXECUTE or EXECUTE HOLD statement.
# The screen erasures caused by the ERASE ON statement can be bothersome to the user in not allowing time for previous results to be studied before erasure. This can be controlled by the PAUSE ON statement.
# Once the ERASE ON statement has been issued, it remains active throughout the IMP session or until discontinued by an ERASE OFF statement.
# When an IMP session begins, the default setting for the ERASE flag is ERASE OFF.
# If an ERASE ON statement is encountered when the ERASE flag is already set to ON, the statement is ignored.

## The ERASE OFF Statement ##
The ERASE OFF statement requests discontinuation of a previous ERASE ON statement.
### Format: ###
ERASE OFF
### Notes: ###

# When an IMP session beings, the default setting for the ERASE flag is ERASE OFF.
# Once the ERASE OFF statement has been issued, it remains active throughout the IMP session or until discontinued by an ERASE ON statement.
# If an ERASE OFF statement is encountered when the ERASE flag is already set to OFF the statement is ignored.
## The IDENTIFY Statement ##
The IDENTIFY statement requests that IMP print (immediately) the names of all entities of a given type which currently exist in the system model.
### Format: ###
IDENTIFY type, type, ... where each "type" is one of the following keywords: VALUES LINKS CONTACTS JOINTS AXES POINTS SPRINGS DAMPERS FORCES TORQUES INPUTS IC ALL LOOPS ZEROES
### Example: ###
IDENTIFY: JOINTS, INPUTS, LOOPS, ZEROES requests an immediate listing of the names of all joints, all SGS's, the links and joints which form the kinematic loops, and the current settings for all IMP tolerances.
### Notes: ###

# The primary use of the IDENTIFY statement is to refresh the user's memory of the current state of the system model. It is intended for interactive use, and is of little help in background execution.
# Each "type" must be one of the keywords listed above. If not, the unknown "type" is ignored.
# Each "type" must be separated from others by a valid separator, usually a space or a comma.
# No more than 35 "types" may be specified in a single IDENTIFY statement.
# Since IMP only recognizes keyword distinctions up to four characters, it is noted that either the singular or the plural forms may be used for all of the above keywords except AXES, IC, or ALL.
# If "type" is one of the keywords: VALUES, LINKS, CONTACTS, JOINTS, AXES, POINTS, SPRINGS, DAMPERS, FORCES, TORQUES, INPUTS, or IC, then the names of all currently defined entities of that type are listed.
# If "type" is the keyword LINKS then the names of all links are listed. The names of all SOLIDS attached to each of those links are listed as well.
# If "type" is the keyword INPUT then the names of all joints with currently active DATA POSITION or DATA MOTION specifications, i.e., all SGCs, are listed.
# If "type" is the keyword ZEROES, then the current settings of all IMP tolerances (ZERO statements) are listed. 1
# If "type" ALL is requested, then the names of all VALUES, LINKS, CONTACTS, JOINTS, AXES, POINTS, SPRINGS, DAMPERS, FORCES, TORQUES, INPUTS, and IC's are listed. LOOPS and ZEROES are not listed, however, unless requested specifically.
## The ZERO (DATA) Statement ##
The ZERO (DATA) statement defines the tolerance used in checking for discrepancies in numerical input data.
### Format: ###
ZERO (DATA) = value where "value" is the numeric value of the tolerance used in data checking.
### Example: ###
ZERO (DATA) = 0.001 specifies that subsequent input data should be checked for discrepancies of greater than 0.001 degrees or length units.
### Notes: ###

# If no ZERO (DATA) statement is given, input data is checked using default tolerances of 0.0001 degrees and 0.0001 length units.
# The "value" given replaces both the angular and the distance tolerances. Therefore, "value" has dimensions of both degrees and length units.
# If more than one ZERO (DATA) statement is given, the later statement takes precedence and earlier data are replaced.
# The effect of setting this tolerance too loosely is that diagnostic messages may be missed for data errors which may have been discovered by a stricter tolerance.
# The effect of setting this tolerance too tight is that the precision required in input data to avoid diagnostics might be more than that required for adequate simulation.
## The ZERO (POSITION) Statement ##
The ZERO (POSITION) statement defines the tolerance used in checking for geometric position errors, and specifies the maximum number of steps allowed in seeking geometric closure of the system at each position simulated.
### Format: ###
ZERO (POSITION) = value, nsteps where "value" is the numeric value of the tolerance used in checking for geometric position errors, and "nsteps" is a positive integer specifying the maximum number of numerical iterations allowed.
### Example: ###
ZERO (POSITION) = 0.0005 specifies that geometric closure be checked at each position simulated using a tolerance of 0.0005 degrees or length units.
### Notes: ###

# If no ZERO (POSITION) statement is given, geometric closure is checked against default tolerances of 0.0001 degrees and 0.0001 length units; a maximum of 20 numerical iterations is allowed.
# The "value" given replaces both the angular and distance tolerances. Therefore, "value" has dimensions of both degrees and length units; "nsteps", of course, is dimensionless.
# If more than one ZERO (POSITION) statement is given, the later statement takes precedence and earlier data are replaced.
# As the system is incremented to each new position, IMP performs an iterative assembly procedure to find proper values for each of the joint variables. The iteration procedure converges and is considered finished when all of the joint variable corrections are smaller than "value".
# The effect of setting this tolerance too loosely is that round-off errors may accumulate to large values in calculations such as the evaluation of dynamic forces. As a general rule, "value" should not be larger than 0.001 and a smaller "value" is preferable.
# The effect of setting this tolerance too tight is that the computer may not be able to achieve the precision necessary for solution. This results in a message that says "the mechanism can not be assembled in 20 iterations". If this message occurs (without a message saying that the iteration process diverged) then "value" is too strict for solution to be possible within the precision of the computer for the input data given.
# A typical problem converges to very tight tolerances in four or less iterations. No problem has ever been found which requires ten or more iterations to reach a solution. Thus, no reason is seen to ever set "nsteps" to a value above 1
#
# If "nsteps" is not given, or is zero or negative, then it is ignored and the previous value remains.
## The ZERO (EQUILIB) Statement ##
The ZERO (EQUILIB) statement defines the tolerance used in determining whether a position of static equilibrium has been achieved within desired accuracy limits, and specifies the maximum number of search steps allowed in seeking equilibrium.
### Format: ###
ZERO (EQUILIB) = value, nsteps where "value" is the numeric value of the tolerance used in checking whether the free generalized coordinate (FGC) positions have achieved a position of static equilibrium for the system, and "nsteps" is a positive integer specifying the maximum number of search steps allowed.
### Example: ###
ZERO (EQUILIB) = 0.0001, 40 specifies that the equilibrium search has converged when the free generalized coordinate (FGC) position values have been determined within 0.0001 degrees or length units, and that up to 40 search steps are allowed.
### Notes: ###

# If no ZERO (EQUILIB) statement is given, the FGC search steps are checked against default tolerances of 0.001 degrees or length units, and 25 search steps are allowed.
# The "value" given replaces both the angular and distance tolerances. Therefore, "value" has dimensions of both degrees and length units; "nsteps", of course, is dimensionless.
# If more than one ZERO (EQUILIB) statement is given, the later statement takes precedence and earlier data are replaced.
# As the FGC position variables are incremented toward equilibrium, the change in each FGC position variable is checked; equilibrium is considered achieved when all FGC position changes are less than "value".
# The effect of setting "value" too loosely is that small unbalanced forces may remain at the FGC variables. As a general rule, this tolerance should be tight enough that "value" multiplied by the largest spring rate in the model yields an acceptably small error in force units.
# The effect of setting "value" too strictly is that the equilibrium search may fail to converge in the "nsteps" allowed. As a general rule, "value" should not be set tighter than the tolerance set by the ZERO (POSITION) statement.
# This tolerance has no effect unless a FIND EQUILIB statement is given before the EXECUTE or EXECUTE HOLD statement.
# If "nsteps" is not given, or is zero or negative, then it is ignored and the previous value remains.
## The ZERO (SYSTEM) Statement ##
The ZERO (SYSTEM) statement defines a tolerance used in determining the number of degrees of freedom of the system.
### Format: ###
ZERO (SYSTEM) = value where "value" is a numeric value to be used for the tolerance.
### Example: ###
ZERO (SYSTEM) = 0.000001
### Notes: ###

# If no ZERO (SYSTEM) statement is given, a default tolerance of 0.0000001 is used.
# As the constraint equations of the system geometry are solved during the iterative geometric assembly procedure, this tolerance is used to determine whether each new equation is linearly independent of the previous equations and can be used to solve for an additional dependent joint variable position value. Any joint variable which cannot be found in this way (not dependent) and is not specified by the user (SGC) is assumed to be a free generalized coordinate (FGC).
# If more than one ZERO (SYSTEM) statement is encountered, the later statement takes precedence and earlier data are replaced.
# As a general rule, this tolerance should be kept at least one order of magnitude stricter than the ZERO (POSITION) tolerance. If too loose, additional degrees of freedom may be erroneously identified for the system. Very tight values (e.g. 1.0E-9) are often desirable and should not be considered too tight unless too few degrees of freedom are identified.
## The ZERO (INERTIA) Statement ##
The ZERO (INERTIA) statement defines the tolerance used in determining singularity of the mass (inertia) matrix of the dynamic equations of motion.
### Format: ###
ZERO (INERTIA) = value where "value" is the numeric value of the tolerance used while inverting the mass matrix.
### Example: ###
ZERO (INERTIA) = 0.001
### Notes: ###

# If no ZERO (INERTIA) statement is given, a default tolerance of 0.00001 is used.
# If more than one ZERO (INERTIA) statement is encountered, the later statement takes precedence and earlier data are replaced.
## The ZERO (SPRING) Statement ##
The ZERO (SPRING) statement defines the tolerance used in determining singularity of the stiffness matrix of the dynamic equations of motion.
### Format: ###
ZERO (SPRING) = value where "value" is the numeric value of the tolerance used in testing for singularity of the stiffness matrix.
### Example: ###
ZERO (SPRING) = 0.001
### Notes: ###

# If no ZERO (SPRING) statement is given, a default tolerance of 0.00001 is used.
# If more than one ZERO (SPRING) statement is encountered, the later statement takes precedence and earlier data are replaced.
# As a general rule, this tolerance should not be looser than the reciprocal of the largest spring rate of the system. If the tolerance is too loose, then a message may be printed.
## The ZERO (INDETERM) Statement ##
The ZERO (INDETERM) statement defines the tolerance used in determining the static indeterminacy of a constraint force component.
### Format: ###
ZERO (INDETERM) = value where "value" is the numeric value of the tolerance used in testing for static indeterminacy of a component of a constraint force.
### Example: ###
ZERO (SPRING) = 0.001
### Notes: ###

# If no ZERO (INDETERM) statement is given, a default tolerance of 0.0001 is used.
# If more than one ZERO (INDETERM) statement is encountered, the later statement takes precedence and earlier data are replaced.
# If this tolerance is too tight, then improper numeric values (usually, but not always zeroes) may be printed for constraint force components which should be shown as statically indeterminate. If this tolerance is too loose, then values of some constraint force components may be shown as indeterminate (‘????’) even when proper numeric values should be found.
## The ZERO (ZERO) Statement ##
The ZERO (ZERO) statement defines a tolerance which is used for testing whether various quantities are essentially zero in situations where no other specific tolerance has been defined.
### Format: ###
ZERO (ZERO) = value where "value" is the numeric value of the tolerance.
### Example: ###
ZERO (ZERO) = 0.00001
### Notes: ###

# If no ZERO (ZERO) statement is given, a default tolerance of 0.000001 is used.
# If more than one ZERO (ZERO) statement is encountered, the later statement takes precedence and earlier data are replaced.
# This tolerance should always be kept very small, at least as small as other tolerances.