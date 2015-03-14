# Chapter 1: The IMP System #

The Integrated Mechanisms Program (IMP) is a computer-aided design and analysis system which
provides a precise, easily used, low cost capability for the simulation of mechanical systems.

The IMP system is intended for the simulation of two- or three-dimensional rigid link mechanical
systems having single or multiple degrees of freedom. The simulation can include pinned, sliding,
screw, spur gear, bevel gear, rack and pinion, cam, slotted, cylindric, universal, ball and socket,
and planar joints in any open- or closed-loop combination. Linear or non-linear springs and viscous
dampers may also be included, either within joints or acting between specified points on the moving
links. Mass and gravity effects can be simulated. Collisions between moving links can be monitored
and the resulting impacts simulated. The system can be driven either by applied forces or input
motions, which can be specified functions of time or system geometry. A system of this type is shown
in the figure on the next page.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch1_1.png' height='400px' />
_Example of a modeled system._

The IMP system is capable of simulation in any of three different modes: kinematic (geometric),
static (equilibrium), or dynamic (time response) mode. In any of these modes IMP will calculate
requested positions, velocities, accelerations, static and dynamic constraint forces, natural
frequencies, damping ratios, and small oscillation transfer functions (principal vibration modes) of
the system simulated.

Before delving into a discussion of the IMP problem-oriented language, the main purpose of this
manual, it is felt that some discussion of the IMP system, its analytical foundations, and the
philosophy behind its development, is important. With this background, hopefully, the user will be
better able to understand its use and to take better advantage of its capabilities. The remainder of
this chapter is devoted to supplying this background.


## The Design Process ##
When the need for a mechanical design presents itself, the designer is faced with two alternative
approaches, either synthesizing or designing a system which meets the requirements.

"_Synthesizing_", in general, implies the application of a known method of solution which explicitly
determines the complete and proper dimensions and specifications of a system to fit the
requirements. While this may be a laudable objective, those synthesis procedures which exist today
which offer complete solution are limited to an extremely small class of problems. Until the scope
of such methods can be significantly extended, it is questionable whether their use justifies the
development cost of a programmed system such as IMP.

The "_design_" of a system, on the other hand, is characterized by "_human iteration_". It makes use
of whatever scientific techniques are applicable. When they are not available, however, the designer
is faced with making his or her own decisions, based on personal judgment and experience, and then
analyzing and testing to determine success.

The IMP system, built upon the design or human iteration philosophy, is therefore intended as a tool
for the designer. It includes a variety of analytical capabilities which can eliminate many routine
tasks and provide computational power far beyond human limitations. The system is not intended,
however, to produce a design. It is assumed that the designer wishes to retain all decision-making
capabilities but will relegate the computational drudgery, as much as possible, to the IMP system.


## System Objectives ##
Once the importance of the man-computer partnership in the design process is recognized, it dictates
many of the characteristics which the IMP system should have. The compromises which were made in the
development of IMP have been based on the philosophy of extending its simulation power, flexibility,
and ease of use, without restricting the designer's freedom of choice. Some discussion of these
objectives and the conflicts between them is important to the user's understanding of IMP.

In the development of IMP, the highest priority has been placed on achieving the maximum scope of
the analyses which can be performed. These presently include the calculation of position, velocity,
acceleration, static and dynamic constraint forces, impacts and momentum changes, natural
frequencies, damping ratios, and small oscillation transfer functions (principal vibration modes).
All of these can be found in either the kinematic (geometric), static (equilibrium), or dynamic
(time response) modes. Although this range of capabilities spans many of the more difficult areas
encountered in the design of rigid body systems, work is continuing to extend the system to new
capabilities.

A closely allied and very important objective has been to achieve maximum breadth in the variety of
systems which can be simulated. The system simulated may be planar or spatial, single- or
multi-freedom, open- or closed-loop. In fact, as a pleasant surprise, it was found after development
that IMP can also be used to analyze structures for their geometric configuration and statically
determinate forces.

The main compromises which had to be made in the development of the IMP system come from the next
objective, that of problem independence. It is felt that the many man-years devoted to the
development of IMP can only be justified through its continued use on a variety of problems.
Therefore every effort has been made to avoid specializing IMP to a particular type of problem.
This objective sometimes causes inconvenience to a particular user. If, for example, a user becomes
unhappy that acceleration information is not given in _g_'s, he or she should remember that other
users' backgrounds lead them to prefer length units per second per second. The alternative is to
write and support a separate program for each application.

A major objective has been that the IMP system be easy to use, since potential users are envisioned
to have little or no computer programming experience. The key to achieving this goal has been the
development of the IMP problem oriented language explained in the remaining chapters of this manual.
With this language, designers can describe their systems and request analyses in terms familiar to
themselves; they need not be familiar with programming languages such as FORTRAN or C.

Hand in hand with ease of use comes the objective that the system be well documented. That is the
purpose of this manual.

Another major objective in the development of IMP has been to achieve, insofar as possible,
host-computer independence. This does not affect the user who has access to the IMP system; however,
without it, IMP might not have been available to him or her on the "right" computer system. With
minor sacrifice in efficiency, the IMP system itself has been written, with a few small exceptions,
in ANSI standard C and it can be quickly implemented on most digital computers. To date IMP has been
implemented on Cray systems, on HP, SUN, and Silicon Graphics Unix systems, on Linux systems, and on
DOS, Windows, Windows 95, Windows 98, Windows 2000, Windows NT, and Windows XP computer systems.

It has also been kept in mind that a good computer-aided design system must be efficient, that is,
it must provide maximum capability at minimum cost. The IMP system is not claimed to be as efficient
as one written for a more specific task. However, efficiency has been a key goal when it can be
achieved without major restrictions on higher priority objectives. Another design objective for a
good system is that it be open-ended and adaptable to fit individual users' needs. This objective
more than any other (so far) has been sacrificed in order to achieve ease of use without requiring
sophisticated programming skills of the user. Internally the IMP system has many capabilities which
cannot as yet be exploited by the user because of the limitations imposed by the IMP problem
oriented language.

The final objective in the development of IMP has been that it be capable of growth, expansion, and
modification. JML is now, and expects to continue to extend the capabilities of IMP. JML is most
interested in obtaining users' suggestions.


## Analytical Techniques ##
One approach to the development of a generalized computer-aided simulation system such as IMP is to
catalog into one system an ever-growing library of solution algorithms for each type of problem
which might be encountered. Requiring the user to specify enough information that his or her problem
can be identified, the system can then be programmed to branch to the appropriate algorithm. This
approach, however, offers no advantages over the development of a separate program for each problem.

A unified approach, on the other hand, implies the development of a single algorithm whereby the
system can recognize, manipulate, and analyze mechanical systems of widely differing structure. In
IMP all problems are analyzed by a single unified procedure based on the algebra of transformation
matrices. The purpose of this section is to briefly describe this generalized procedure, and to
supply references for those users interested in more detail. The main references for the entire
analytical formulation are the doctoral dissertation of P. N. Sheth [[1](ManualChapter1#Footnotes.md)] and the associated
publication.[[2](ManualChapter1#Footnotes.md),[3](3.md)]

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch1_2.png' height='400px' />
_Figure 1-2_ Example of a modeled system.

### Topological Analysis ###
The first phase of a systematic study of a mechanical system must be the topological analysis of the
system description provided by the user. Topological analysis includes the recognition of the number
of links, the number and types of joints, the pattern in which the links and joints are arranged,
the number and form of any kinematic loops, and other such characteristics which are solely
determined by the connectivity of the system.

The elements to be included in the system model are defined by the IMP user through the definition
statements of the IMP language; these are described in [Chapter 3](ManualChapter3.md). As statements are encountered,
several preliminary checks are made and, if the newly defined component is consistent with previous
information, it is added to the model. Space is also reserved at this time for numerical data for
the component and its relationships with other components of the system model are stored.

An essential task in the topological analysis of a mechanical system is the determination of any
kinematic loops. All kinematic analysis techniques, in one way or another, depend upon the
recognition of such loops for the formulation of constraint equations. IMP uses an algorithm based
on graph theory [[4](ManualChapter1#Footnotes.md)] to automate the identification of loops.

If for example, at this stage, IMP discovers that the fixed link is not defined, it concludes that
the problem is improperly posed, prints a diagnostic message, and terminates the simulation.


### Data Collection ###
The next step in the simulation of the system is the collection and reduction of numeric data
supplied by the user to describe the particular system to be simulated. This is done by the use of
the DATA statements explained in [Chapter 4](ManualChapter4.md). These statements are also checked by the IMP system as
they are encountered and appropriate diagnostic messages are printed when errors are detected.

In order to simulate the motions in a particular system, the most essential numeric data required
are the descriptions of the relative locations and orientations of the joint elements on the various
links. Since the possibility of interference between links is not necessarily considered by IMP, a
complete description of the physical shape of each link, though possible, is not always necessary.
The more important "kinematic shape" of each rigid link is described by specifying the locations
of strategically placed, right-hand Cartesian coordinate systems attached to each link at each joint
[[5](ManualChapter1#Footnotes.md)].

The constant spatial relationships between these coordinate systems and the local coordinate system
of the link itself are stored in the form of transformation matrices. Taken together, these
represent the shapes of the rigid links. Similarly, each joint is represented internally by a
variable transformation matrix relating the coordinate systems attached to the mating joint
elements.

These "local" coordinate systems attached to the links prove convenient reference frames for the
specification of center of mass locations, moments and products of inertia, attachment points for
springs and dampers, points of application for applied forces, etc. They are also quite important in
interpreting the sign conventions of much of the printed results, particularly the joint variable
positions, velocities, and accelerations, and constraint force components.

### Position Analysis ###
The closure of the kinematic loops discussed in Section 1-3.1 leads to a set of matrix loop
equations involving the transformation matrices discussed in Section 1-3.2. These equations require
that, for the system to be assembled at any position, the loops must remain closed. An iterative
technique is, therefore, applied to discover the correct joint variable values at each
position simulated.[[6](ManualChapter1#Footnotes.md)] Once the joint variables are known, all other position information is readily
determined.

Positions of the system other than the original design position for which the data was specified
cannot be determined, of course, until the positions of certain input variables are specified. These
input variables may be considered the "generalized coordinates" of the system; their number equals
the number of degrees of freedom (_DF_) of the system.

In general, some of these _DF_ generalized coordinates of the system may be
controlled (driven) by external agents; these will be referred to as "specified generalized
coordinates" (_SGC_). Any remaining degrees of freedom then assume values dictated by static
equilibrium or by the dynamic conditions, depending on the mode of the simulation. The number of
"free generalized coordinates" (_FGC_) is thus defined by the following simple equation:
```
FGC = DF - SGC
```
The number of _FGC_ may take on any value between zero and _DF_, depending on the number of _SGC_. When _SGC = DF_, there are no _FGC_
and the position of the system is defined by kinematic considerations alone. When, on the other
hand, _SGC_ equals zero and _FGC_ equals DF, all of the generalized coordinates assume
values determined by the mode of the simulation. IMP is designed to operate in any of three
different modes: kinematic (geometric) mode, static (equilibrium) mode, or dynamic (time response)
mode.


### Kinematic Mode ###
In kinematic (geometric) mode the user alone specifies the range of motion and the step size for
each of the generalized coordinates. The user may specify input velocities, input
accelerations, and applied forces, and solve for quantities of interest over a specified range of
positions. When operating in this mode, IMP recognizes the presence of any inadvertently overlooked
FGC and holds its value constant as the system is moved over the specified positions. If, on the
other hand, more generalized coordinates are assigned than there are degrees of freedom in the
system simulated, then difficulty will almost certainly be encountered in solving for the positions
and assembling the system.

The user should be wary of the possible presence of any _FGCs_ when performing force analysis in the
kinematic mode. When either the user or IMP chooses a joint variable to represent an _SGC_ or _FGC_,
respectively, and sets its position, IMP assumes that any necessary driving force or torque is
applied to that joint variable to maintain force balance in the system at the defined position. This
assumption can lead to erroneous interpretation of results if the user is not cognizant of the
presence of such an applied force or torque.


### Static Mode ###
For spring restrained systems acted on by steady forces, the user may wish to specify only some of
the generalized coordinates (_SGCs_) and allow the _FGCs_ to assume positions dictated by static
equilibrium conditions. Or perhaps the user may wish to increment the applied forces acting on the
system and study the various equilibrium positions attained. This static (equilibrium) mode of
simulation can be useful, for example, in analyzing a vehicle suspension system.

The analytical technique used to locate the static equilibrium position is an iterative (gradient)
search procedure which seeks a position of minimum potential energy for the system. The procedure is
similar to that developed by Livermore [[7](ManualChapter1#Footnotes.md)]. The _FGC_ positions are
corrected by the following equation until the system is brought sufficiently close to a static
equilibrium configuration.
```
[K]{dX} = {dF}
```
where `[K]` is the symmetric (_FGC_ x _FGC_) stiffness matrix of the system (which
changes with each new position), `{dX}` is a vector of first-order corrections to the _FGC_ position
values, and `{dF}` is a vector of the net unbalanced forces at the FGCs. If 25 search steps are taken
without reaching equilibrium, then the search is halted and a diagnostic message is printed.

Unless the stiffness matrix is singular, that is, unless one or more of the _FGC_ variables can be
moved without producing a change in the forces, then the search procedure attempts to converge to a
position where there are no unbalanced forces at the _FGCs_. The gradient search procedure used,
however, has far less information to guide its progress when the stiffness matrix is singular, and
is much more likely to fail to achieve equilibrium within the 25 steps permitted.

### Dynamic Mode ###
Two distinct types of dynamic problems may be identified. The first type is characterized by small
amplitude oscillations of the system about a position of static (or quasi-static) equilibrium. As an
example, an automotive suspension system traveling on a smooth straight road may be disturbed by a
wheel encountering a small bump, thus inducing a small oscillation dynamic state. Typically the
simulation of such motions make use of linearized equations of motion and geometric non-linearities
are neglected. This type of simulation is possible within the IMP system and is described in
Section 1-3.11; it does not require that the simulation be done in the dynamic mode.

The second type of dynamic problem is characterized by large amplitude motions and requires dealing
with geometric non-linearities. A linkage system driven by a constant torque motor is an example.
Such a problem is simulated by IMP in the dynamic (time response) mode, wherein IMP numerically time
integrates the dynamic equations of motion.

Before the time integration procedure is begun, the specified driving motions at the SGCs and the
applied forces are set to their initial values. Any user specified initial conditions are then
applied to the _FGCs_ and the time integration is initiated.

The integration algorithm used is unique to IMP and is intended to optimize response by allowing
reasonably sized time steps compared to other algorithms. Each integration step is taken as follows:

  1. The equations of motion are formulated for the current position [[8](ManualChapter1#Footnotes.md)].
  1. The equations are linearized assuming that the change in position of the system and the change in the applied forces during the time step are small [[9](ManualChapter1#Footnotes.md)].
  1. The principal modes of vibration are calculated for the linearized system.
  1. The initial conditions for the time step are applied to determine the participation amplitudes of the principal modes. Both the transient and the steady state terms are included.
  1. The time step is taken by the assumption that the linearized principal mode vibration response is a reasonable approximation to the non-linear response during the time interval [[10](ManualChapter1#Footnotes.md)], [[11](ManualChapter1#Footnotes.md)].
  1. The time step used henceforth is recalculated in order to minimize error accumulation during integration while still keeping efficiency high [[12](ManualChapter1#Footnotes.md)].
  1. The requested results are calculated and printed for the current value of time.
  1. The procedure is repeated for the next time step until the user specified total time interval is completed.


### Collision and Impact Analysis[[13](ManualChapter1#Footnotes.md)] ###
If operating in dynamic mode and if solid shapes are defined for at least portions of some links,
IMP can be requested to monitor specified pairs of solid link shapes for possible collision during
the motion simulated. When a collision is detected an appropriate impact is simulated, using
supplied three-dimensional coefficients of restitution and Coulomb friction, and new velocities
resulting from such an impact are discovered. The dynamic mode simulation then proceeds as usual. If
operating in kinematic or static mode, collision and impact analysis are not active.

### Velocity and Acceleration Analyses ###
No matter whether the system achieves each new position in the kinematic, static, or dynamic mode,
the iterative procedure described in 1-3.3 for position analysis is carried out to insure that all
data is current for the new position. Velocity and acceleration analyses are then performed, if
requested by the user, by taking first and second time derivatives of the matrix loop equations.[^14^](ManualChapter1#Footnotes.md)
Because of the derivatives already calculated in the iterative position analysis, this is a very
easy and efficient procedure.

### Force Analysis ###
The constraint forces acting through the joints onto adjoining links at each position may be of
design interest. Another quantity which is often of design interest is the driving force required to
maintain the specified motion of the system _SGCs_. IMP includes the ability to determine
all statically determinate constraint and driving forces at the joints designated by the user. The
resultant forces include the cumulative effects of all force producing elements as well as
gravitational forces and the dynamic forces produced by the masses of the moving links. These forces
are determined by a method combining the virtual work and variation of constraint techniques.[^15^](ManualChapter1#Footnotes.md)

In general, there are a set of three forces and three moments transmitted through each joint. The
coordinate systems attached to the various links at their joint elements, which were used for data
specification, are used again here for the directions and sign conventions of the calculated
constraint force and torque components.

### Natural Frequencies and Damping Ratios ###
Natural frequencies and damping ratios are only truly defined for linear systems. Strictly speaking,
therefore, there are no such definitions for systems which are inherently non-linear. It is common
practice, however, to extend these definitions to cover the linearized equations of non-linear
systems operating within a small range of motion about some known position.

IMP includes the capability of calculating and printing these properties of the linearized system;
(cf. especially footnotes [8-12](ManualChapter1#Footnotes.md), including references). These properties change, of
course, with each new position of the system as the equations are relinearized. They do, however,
give some insight into the dynamic behavior of the system in the immediate vicinity of each
position.

### Transfer Function Analysis ###
Another quantity only properly defined for linear systems is referred to under the title of
_transfer function_. Assuming small oscillations around the current position, IMP is able to
calculate the linearized vibratory response of any joint or point of the system to a small
oscillatory applied force or motion. These are calculated from the principal modes of vibration (the
eigenvalues and eigenvectors) of the linearized equations of motion `[8]`, and can be
printed, listed, plotted, or stored as functions of the exciting frequency.

Although the transfer functions change with the system geometry, they are not calculated at every
position simulated. They are formulated only for the most recent position analyzed.

### Special Cases ###
The simulation algorithms are all well defined and IMP produces reliable and accurate solutions once
a system is properly modeled. A generalized program, however, must foresee certain types of
pathological numeric difficulties and must include some means of coping with them.

One of the most common difficulties in the simulation of mechanical systems occurs when the system
being simulated reaches a locking position (dead point) or an extreme-range position. The numeric
computations cause difficulty in such a position because one or more of the velocity ratios
approaches infinity. However, a dead-center position is dependent on the choice of the driving
joint(s) of the system. If some other suitable joint(s) become the driving joint(s) for a small
portion of the motion near such a position, the problem is eliminated.

IMP recognizes this problem as identical with the problem of _optimum_ choice of the FGCs for the
system at each position, the _optimum_ set of FGCs being defined as the set giving the lowest
rates of change of the dependent joint variables with respect to the chosen FGC positions. The
selection of FGCs and the determination of the total degrees of freedom of a system at each position
is done by elementary matrix operations on the set of velocity equations corresponding to that
position [[16](ManualChapter1#Footnotes.md)].

The numerical integration scheme used for the dynamic mode solution is complicated by the fact that
the optimum set of FGCs may not always be comprised of the same coordinates as the system achieves
successive positions.

As an aid in detecting a problem with a "near" locking position, IMP calculates and prints a
"quality index" value at each position simulated. By itself, this number has no use; it is the
determinant of the simultaneous equations which relate the velocities of the dependent joint
variables. However, as the system moves to each new position, the value of this index varies. If the
quality index becomes small -- say, more than an order of magnitude smaller than its value at some
other position -- this is an indication of potential difficulty, either in the design of the system
itself, in the simulation model, or in the choice of the driving links, the SGCs. The quality index
is a qualitative measure, somewhat analogous to the concept of the "pressure angle" of a cam
system, or the "transmission angle" of a four-bar linkage. If this index becomes very small, then
such a system, driven in the manner simulated, has extremely high ratios between some of its
dependent velocity variables, and requires extremely large forces to overcome the imposed loads.

Other potential numeric difficulties are encountered when the stiffness matrix `[K]`
or the mass matrix `[M]` of the system become singular in a static or dynamic mode
simulation, for example, when the masses of some of the links have been neglected and when it is
possible to move any of the FGCs in such a manner that only massless links move. These pathological
cases are recognized and appropriate diagnostic messages are printed.

## Background Processing vs. Interaction ##
As brought out in Section 1-1, the IMP system is intended for use as a design tool in a human
iteration loop. IMP should provide computational power while the user retains all decision making
power. This relationship implies the necessity for interaction between IMP and the user. For this
reason, IMP is intended for use in an interactive environment.

The interactive or on-line approach implies that the user is seated at a graphic display or similar
terminal connected to a computer containing the IMP system. He types the IMP language statements on
the terminal and they are interpreted and executed, giving responses shortly after the requests. The
user may at any time modify the simulation model and request further analysis.

In principle, the same design process can take place in the background-processing mode, with longer
interaction delays. However, there are several differences caused by the interactive nature of the
on-line process; some of these may be listed as follows:

  1. The user has control over and can halt the simulation if he or she sees that further computation will be fruitless.
  1. The user can perform the design analysis in an adaptive way, in the sense that they are able to _guide_ the simulation rather than to have to preset it, and then possibly _suffer the consequences_ of a long delay for useless results.
  1. Often, at the early design stage, the definition of the system to be simulated is either incomplete or unclear. Simulation performed in an on-line design environment allows the definition and solution efforts to take place in parallel.
  1. The user can perform the simulation in a conversational manner; their thought processes need not be interrupted by long delays.

There are situations, on the other hand, where background processing is advantageous. When the
complexity of the problem requires lengthy computations and prevents immediate response, the on-line
mode becomes a burden to the user. Also, when the quantity of the printed results desired is high,
the extremely slow speed of a printing terminal can make it undesirable for these situations, and
background processing may be preferable.

## Diagnostics ##
Throughout the IMP system there are a great number of tests and comparisons to detect errors, either
in the format of the statements, in their compatibility with other statements, or ambiguities or
conflicts with basic kinematic or dynamic laws or principles. All detected errors cause appropriate
diagnostic messages to be printed. These messages should be self-explanatory. However, if questions
arise, more information may be found in the notes in this manual appropriate to the statement which
precedes the message.

Although IMP has been programmed to detect errors, whenever possible they are treated as non-fatal;
that is, IMP attempts some adjustment for the error (such as to neglect the offending statement) and
proceeds with the next IMP statement. Only in rare cases does an error cause the IMP program to
terminate. Many of the actions taken for errors are detailed in the notes appropriate to each
statement.

The decision to treat most errors as non-fatal can be bothersome, particularly in background
processing, since the message may be overlooked in scanning through the printed results and also
because of the possible additional cost of analyzing an erroneously simulated problem. However, in
the interactive environment, this ability to retype offending statements and continue, rather than
to start over, is essential in providing the conversational style which is natural to interaction.

## The IMP Data Structure ##
The IMP language, which is described in the following chapters, provides the user with a means of
communicating a problem to the computer in a way which is natural to him or her. However, IMP's
understanding (storage format) of a particular problem takes the form of an elaborate data structure
in the memory of the computer.

It should be emphasized that the usual FORTRAN procedure of creating arrays of fixed length cannot
adequately satisfy the requirements of the IMP system. The ability to add system components at will,
without restrictions on the maximum number of components of a given type, requires that the data
structure evolve in an adaptive fashion as the IMP language statements are encountered. The limit
set by the size of the computer memory should not restrict the number of combination of components
for a given problem.

Also, when an element (a particular joint, for example) is deleted, the items which depend on it
(such as an applied force within the joint) should also be automatically deleted, while other
related items (such as the links which were connected) should remain. This requires a data structure
which is suited to recursive operations and which stores not only the individual component
descriptions but also a rather detailed account of the relationships and dependencies between
components.

IMP utilizes a rather complex hierarchical data structure implemented in the C language. Because of
its inherent properties, there is no limitation on the size of the problem which IMP can simulate;
any limitation comes from the size of the computer and operating system (RAM and virtual) memory on
which IMP is operating, not from the IMP system itself. Also, the deletion of elements from the
system model causes the natural disappearance of all dependent information.

Another advantage of the data structure in IMP comes in the efficient use of computer memory. When
memory is needed for numeric computations, it is "borrowed" from available unused storage and
released again when the computations are completed. Thus, the same storage is used repeatedly for
entirely different numeric activities. This provides a significant saving in computer space and
allows IMP to simulate much more complex problems than would otherwise be possible within a given
amount of computer memory.

## Footnotes ##
  1. P. N. Sheth, "A Digital Computer Based Simulation Procedure for Multiple Degree of Freedom Mechanical Systems with Geometric Constraints", PhD Dissertation, University of Wisconsin, Madison, WI, 1972, available from University Microfilms, Inc., Ann Arbor, MI.
  1. J. J. Uicker, B. Ravani, and P. N. Sheth, "Matrix Methods in the Design Analysis of Mechanisms and MultiBody Systems", Cambridge University Press, New York, 2010.
  1. P. N. Sheth and J. J. Uicker, Jr., "IMP, (Integrated Mechanisms Program): A Computer Aided Design Analysis System for Mechanisms and Linkages", Journal of Engineering for Industry, ASME Transactions, Vol. 93, Series B, No. 4, 1971.
  1. T. A. Phelps, "Algorithms for Determining the Kinematic Loops in Mechanisms", MS Thesis, University of Wisconsin, Madison, WI, 1983.
  1. P. N. Sheth and J. J. Uicker, Jr., "A Generalized Symbolic Notation for Mechanisms", Journal of Engineering for Industry, ASME Transactions, Vol. 93, Series B, No. 1, 1971.
  1. J. J. Uicker, Jr., J. Denavit, and R. S. Hartenberg, "An Iterative Method for the Displacement Analysis of Spatial Mechanisms", Journal of Applied Mechanics, ASME Transactions, Vol. 86, Series E, No. 2, 1964.
  1. D. F. Livermore, "The Determination of Equilibrium Configurations of Spring-Restrained Mechanisms Using (4x4) Matrix Methods", Journal of Engineering for Industry, ASME Transactions, Vol. 89, Series B, No. 1, 1967.
  1. J. J. Uicker, Jr., "Dynamic Behavior of Spatial Linkages: Part I - Exact Equations of Motion", Journal of Engineering for Industry, ASME Transactions, Vol. 91, Series B, No. 1, 1969.
  1. J. J. Uicker, Jr., "Dynamic Behavior of Spatial Linkages: Part II - Small Oscillations About Equilibrium", Journal of Engineering for Industry, ASME Transactions, Vol. 91, Series B, No. 1, 1969.
  1. R. J. Cipra, "On the Dynamic Simulation of Large Non-Linear Mechanical Systems", Ph.D. Dissertation, University of Wisconsin, Madison, WI, 1978, available from University Microfilms, Inc., Ann Arbor, MI.
  1. R. J. Cipra and J. J. Uicker, Jr., "On the Dynamic Simulation of Large Non-Linear Mechanical Systems", Journal of Mechanical Design, ASME Transactions, Vol. 103, October 1981.
  1. M. L. Hornick, "Use of Modal Techniques in the Numerical Simulation of the Dynamic Response of Spatial Mechanisms", MS Thesis, University of Wisconsin, Madison, WI, 1982.
  1. W. Wisutmethangoon, "Collision Detection and Dynamic Impact Simulation of Mechanisms", Ph.D. Dissertation, University of Wisconsin, Madison, WI, 1998, available from University Microfilms, Inc., Ann Arbor, MI.
  1. J. Denavit, R. S. Hartenberg, R. Razi, and J. J. Uicker, Jr., "Velocity, Acceleration, and Static Force Analysis of Spatial Linkages", Journal of Applied Mechanics, ASME Transactions, Vol. 87, Series E, No. 4, 1965.
  1. J. J. Uicker, Jr., "Dynamic Force Analysis of Spatial Linkages", Journal of Applied Mechanics, ASME Transactions, Vol. 89, Series E, No. 2, 1967.
  1. P. N. Sheth, "Improved Iterative Techniques for the (4x4) Matrix Methods of Kinematic Analysis", MS Thesis, University of Wisconsin, Madison, WI, 1968.