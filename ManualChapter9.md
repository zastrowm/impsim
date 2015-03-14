# Chapter 9: Application Examples #
The purpose of this chapter is to present examples of simulations performed on the IMP system, thereby demonstrating the use of the IMP language and showing the form of the output.

Many of the pages of this chapter are direct reproductions of IMP output. Some symbols have been added in the right-hand margins, however, which refer to notes of explanation on subsequent pages. Careful attention should also be paid to the figures accompanying each example since these show the alphanumeric names used for links, joints, etc.

The examples chosen are merely illustrative and, for lack of space, are not intended to be exhaustive. Not all details of each example are explained, and the reader should consult the previous chapters as questions arise. These examples do show, however, how many of the IMP statements interrelate, and illustrate some of the more useful features of the IMP system.

## A Differential Control Linkage ##
The first example presented is the two degree of freedom differential control linkage shown in the figure on the next page. In this device, the sliding joint JT1 and the pin joint JT8 are both driven externally, and the output of the linkage is the rotation of the pin joint JT5. The purpose of the analysis is to verify the geometric relationship between the output position of JT5 and the input JT8, while holding JT1 fixed at various settings.

The next several pages show portions of the printed IMP output. The IMP language statements typed by the user are printed exactly as submitted to the IMP interpreter.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_1.png' />
_Figure 9-1_ A Differential Control Linkage.

> <<<  Notice  >>>

> This is the Integrated Mechanisms Program (IMP-2000).
> (C)Copyright, JML Research, Inc., 1984-2000. All rights reserved.

> JML Research, Inc. is endeavoring to make this program as complete,
> accurate, and easy to use as possible. Suggestions and comments are
> welcomed. Any errors encountered in either the documentation or in the
> results should be immediately brought to our attention.

> Neither JML Research, Inc. nor those supplying the computer facilities
> for this analysis assume any responsibility for the validity, accuracy,
> or applicablitiy of any results obtained from this system; users must
> verify their own results.

  * 
  * Integrated Mechanisms Program (IMP-2000)               *** Win/NT Version -- Released 01 Jan 2000**
  * on 19 Dec 99               at 14:49:23                *****

> What kind of terminal are you using?
> > alpha, graphic [graphic](graphic.md):> graphic                                        [#Notes|(1)]

> > print input                                                               [#Notes|(2)]
> > recall input                                                              [#Notes|(3)]
> Enter a name for a command input file.                                      [#Notes|(3)]
> > Filename: > diflnk.dat                                                    [#Notes|(3)]

> TITLE = DIFFERENTIAL CONTROL LINKAGE
> REMARK: DEFINITION AND DATA STATEMENTS.                                     [#Notes|(4)]
> GROUND = FRAME
  * **The fixed link is redefined.**                                        [#Notes|(4)]
> YSLIDE(FRAME,A) = JT1
> > DATA YSLIDE(JT1)=-6,-1, 0

> ZPIN(A,C) = JT2
> > DATA ZPIN(JT2) =-6, 2, 0                                                  [#Notes|(5)]
  * **Warning: 6 zeroes are added to complete statement.**                  [#Notes|(5)]

> XSLIDE(C,D) = JT3
> > DATA XSLIDE(JT3)=-6, 2, 0

> ZPIN(S,D) = JT4
> > DATA ZPIN(JT4) = 0, 2, 0                                                  [#Notes|(5)]
  * **Warning: 6 zeroes are added to complete statement.**                  [#Notes|(5)]

> ZPIN(FRAME,S) = JT5
> ZPIN(E,D) = JT6
> > DATA ZPIN(JT6) = 5, 2, 0; 6, 1, 0; 6, 2,  0

> ZPIN(B,E) = JT7
> > DATA ZPIN(JT7) = 6, 1, 0; , , ; 5, 2,     0

> ZPIN(FRAME,B) = JT8
> > DATA ZPIN(JT8) = 6, 0, 0                                                  [#Notes|(5)]
  * **Warning: 6 zeroes are added to complete statement.**                  [#Notes|(5)]

> REMARK: POINT DATA FOR GRAPHICS.
> POINT(A) = PA1,PA2,PA3,PA4,PA1
> > DATA POINT(PA1,ABS) =-6.2,-1.5,0
> > DATA POINT(PA2,ABS) =-5.8,-1.5,0
> > DATA POINT(PA3,ABS) =-5.8, 2.2,0
> > DATA POINT(PA4,ABS) =-6.2, 2.2,0

> POINT(B) = PB1,PB2,PB3,PB4,PB1
> > DATA POINT(PB1,ABS) = 5.8,-0.2,0
> > DATA POINT(PB2,ABS) = 6.2,-0.2,0

> DATA POINT(PB3,ABS) = 6.2, 1.2,0
> > DATA POINT(PB4,ABS) = 5.8, 1.2,0

> POINT(C) = PC1,PC2,PC3,PC4,PC1
> DATA POINT(PC1,ABS) =-6.3, 1.5,0
> > DATA POINT(PC2,ABS) =-5.7, 1.5,0

> DATA POINT(PC3,ABS) =-5.7, 2.5,0
> DATA POINT(PC4,ABS) =-6.3, 2.5,0
> POINT(D) = END,PD1,PD2,PD3,PD4,END
> > DATA POINT(END,JT3) =-3 , 0 ,0                                            [#Notes|(6)]
> > DATA POINT(PD1,JT3) =-3 ,-0.3,0
> > DATA POINT(PD2,JT6) = 0.3,-0.3,0
> > DATA POINT(PD3,JT6) = 0.3, 0.3,0
> > DATA POINT(PD4,JT3) =-3 , 0.3,0

> POINT(E) = PE1,PE2,PE3,PE4,PE1
> > DATA POINT(PE1,JT6) =-0.2,-0.2,0
> > DATA POINT(PE2,JT7) =-0.2, 0.2,0
> > DATA POINT(PE3,JT7) =-0.2,-0.2,0
> > DATA POINT(PE4,JT6) =-0.2, 0.2,0

> POINT(S) = PS1,PS2,PS3,PS4,PS1
> > DATA POINT(PS1,ABS) =-0.2,-0.2,0
> > DATA POINT(PS2,ABS) = 0.2,-0.2,0
> > DATA POINT(PS3,ABS) = 0.2, 2.2,0
> > DATA POINT(PS4,ABS) =-0.2, 2.2,0

> POINT(FRAME) = PF1,PF2,PF3,PF1
> > DATA POINT(PF1,ABS) = 0 , 0 ,0
> > DATA POINT(PF2,ABS) =-0.5,-0.5,0
> > DATA POINT(PF3,ABS) = 0.5,-0.5,0

> POINT(FRAME) = PF4,PF5,PF6,PF4
> > DATA POINT(PF4,ABS) = 6 , 0 ,0
> > DATA POINT(PF5,ABS) = 5.5,-0.5,0
> > DATA POINT(PF6,ABS) = 6.5,-0.5,0

> POINT(FRAME) = PG1,PG2,PG3,PG1
> > DATA POINT(PG1,ABS) =-6.2, 0 ,0
> > DATA POINT(PG2,ABS) =-6.7, 0.3,0
> > DATA POINT(PG3,ABS) =-6.7,-0.3,0

> POINT(FRAME) = PG4,PG5,PG6,PG4
> > DATA POINT(PG4,ABS) =-5.8, 0 ,0
> > DATA POINT(PG5,ABS) =-5.3, 0.3,0
> > DATA POINT(PG6,ABS) =-5.3,-0.3,0

> REMARK: GRAPHIC VISIBILITY AND COLOR SETTINGS.
> DATA VIEW    = FRONT         $$ SCALE FIGURE TO FIT SCREEN.
> SHOW WHITE   = FRAME                                                        [#Notes|(7)]
> SHOW RED     = A                                                            [#Notes|(7)]
> SHOW BLUE    = B                                                            [#Notes|(7)]
> SHOW MAGENTA = C                                                            [#Notes|(7)]
> SHOW YELLOW = D                                                             [#Notes|(7)]
> SHOW CYAN    = E                                                            [#Notes|(7)]
> SHOW BLUE    = S                                                            [#Notes|(7)]
> REMARK: GRAPHIC COMMANDS.
> AXES 1 ALL                   $$ MAKE JOINT AXES VISIBLE.
> DRAW                         $$ DRAW NOW.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_2.png' />
_Figure 9-2_ Example of a modeled system.

> AXES 0 ALL                   $$ MAKE JOINT AXES INVISIBLE.
> REMARK: REQUEST STATEMENTS.
> LIST POSITION(JT5,END)
> PLOT POSITION(JT5)
> PAUSE ON                     $$ PAUSE TO STUDY EACH RESULT.                  [#Notes|(8)]
> REMARK: DATA FOR INPUT POSITIONS.
> DATA POSITION(JT1) = 0       $$ HOLD JOINT JT1 STATIONARY.                   [#Notes|(9)]
> DATA POSITION(JT8) = 0,-5,5 $$ INCREMENT JOINT JT8.                         [#Notes|(10)]
> DATA TIME = 5,1,1                                                           [#Notes|(11)]
> RETURN                                                                      [#Notes|(12)]
> > execute                                                                   [#Notes|(12)]
  * 
  * DIFFERENTIAL CONTROL LINKAGE                     *** Kinematic Mode**
  * on 19 Dec 99     at 14:50:30                     *******> time = 0.000000
> time = 1.000000
> time = 2.000000
> time = 3.000000
> time = 4.000000
> time = 5.000000
> Press 'ENTER' to continue: >
> Listing of position of joint JT5
> > Time    JVar 1
> > 5.0 0.000
> > 5.0 -2.507
> > 5.0 -5.019
> > 5.0 -7.526
> > 5.0 -10.018
> > 5.0 -12.487

> Press 'ENTER' to continue: >**

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_3.png' />
_Figure 9-3_ Position of joint JT5 vs. time

> Listing of position of point END
> > Time         X          Y          Z
> > 0.000000     -9.000      2.000      0.000
    1. 000000     -8.913      2.001      0.000
> > 2.000000     -8.825      2.004      0.000
> > 3.000000     -8.738      2.008      0.000
> > 4.000000     -8.652      2.013      0.000
> > 5.000000     -8.567      2.019      0.000

> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> > recall input                                                              [#Notes|(13)]
> > [#Notes|(14)]

> REMARK: CHANGE THE POSITION OF JT1 AND REANALYZE.
> REMARK: USE THE SAME POSITION INCREMENTS FOR JT8.
> DATA POSITION(JT1) =-0.5
  * **Input motion for joint JT1 1 is redefined.**                          [#Notes|(15)]
> ANIMATE                      $$ SET UP FOR ANIMATED PICTURES.               [#Notes|(16)]
> RETURN
> > execute                                                                   [#Notes|(17)]

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_4.png' />
_Figure 9-4_ Animation of the differential control linkage.[#Notes|(18)]

> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Listing of position of joint JT5
> > Time     JVar 1
> > 0.000000    -12.938
    1. 000000    -14.295
> > 2.000000    -15.853
> > 3.000000    -17.564
> > 4.000000    -19.389
> > 5.000000    -21.298

> Press 'ENTER' to continue: >
> Listing of position of point END
> > Time         X          Y      Z
> > 0.000000     -8.530      1.324  0.000
    1. 000000     -8.486      1.332  0.000
> > 2.000000     -8.435      1.342  0.000
> > 3.000000     -8.379      1.353  0.000
> > 4.000000     -8.321      1.365  0.000
> > 5.000000     -8.260      1.378  0.000

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_5.png' />
_Figure 9-5_ Position of joint JT5 vs. time.

> Press 'ENTER' to continue: >
> > recall input
> REMARK: CHANGE THE POSITION OF JT1 AGAIN.
> DATA POSITION(JT1) = 0.5
  * **Input motion for joint JT1 1 is redefined.**                 [#Notes|(15)]
> RETURN
> > execute

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_6.png' />
_Figure 9-6_ Animation of the differential control linkage.

> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Listing of position of joint JT5
> > Time     JVar 1
> > 0.000000      8.426
    1. 000000      5.549
> > 2.000000      2.692
> > 3.000000     -0.131
> > 4.000000     -2.909
> > 5.000000     -5.632

> Press 'ENTER' to continue: >
> Listing of position of point END
> > Time         X          Y      Z
> > 0.000000     -9.256      2.798  0.000
    1. 000000     -9.159      2.777  0.000
> > 2.000000     -9.062      2.760  0.000
> > 3.000000     -8.964      2.747  0.000
> > 4.000000     -8.868      2.736  0.000
> > 5.000000     -8.773      2.728  0.000

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_7.png' />
_Figure 9-7_ Position of joint JT5 vs. time.

> Press 'ENTER' to continue: >
> > recall input                                                     [#Notes|(19)]
  * **RETURN statement simulated at end of file.**                 [#Notes|(19)]
> > end                                                              [#Notes|(20)]

### Notes ###
# The response specifies that the user is currently operating with a graphic display terminal and expects to be drawing plots of results.
# Data is to be read from a data file and printed at the terminal as it is read.
# The <tt>RECALL INPUT</tt> statement initiates the request to read command input from a file. Since no filename is given in the statement, the IMP system prompts the user for the filename.
# The <tt>GROUND</tt> statement would not have been required if the name <tt>BASE</tt> had been chosen for the fixed link.
# Note that only one point is specified in each of these <tt>DATA ZPIN</tt> statements; the global origin is implied for the location of the missing second and third points.
# Note that this data is described relative to the local joint coordinate systems. It places the point <tt>END</tt>, for example, at the left end of link <tt>D</tt>.
# Although the figures in this manual do not show in color, these <tt>SHOW</tt> statements specify colors for display on color capable terminals. If the device is not color capable, the <tt>SHOW</tt> statements may still be used in the input data file without causing errors.
# The <tt>PAUSE ON</tt> statement is used to cause pauses and messages in the output which read "Press <tt>ENTER</tt> to continue: >", thus allowing the user to study results before they are lost from the screen.
# Note that, if this statement were not included, IMP would arbitrarily choose some joint to hold stationary since the system has two degrees of freedom and the simulation is in kinematic mode.
# The simulation is requested to proceed through six positions; the position of joint <tt>JT8</tt> is incremented five times.
# Note the use of the <tt>DATA TIME</tt> statement in kinematic mode. This feature allows use of functions of time in kinematic mode. The <tt>DATA TIME</tt> statement was not necessary here and would have been implied by the five position increments of the previous line; it is used to illustrate the procedure.
# The <tt>RETURN</tt> statement is read from the command input file and causes control to return to the terminal. The user then manually enters the <tt>EXECUTE</tt> command.
# After the simulation is completed, the user may continue the problem, modifying the model and analysing again.
# Here, since no filename is given, IMP continues reading statements from the same <tt>DIFLNK.DAT</tt> command input file used earlier until the next <tt>RETURN</tt> statement is encountered.
# These warning messages are not part of the user's input statements; they are given by the IMP system as reminders to the user when previous data are redefined. The <tt>ANIMATE</tt> statement causes an animated drawing sequence,
# not immediately, but after the next <tt>EXECUTE</tt> statement. Since the input position data are not respecified for <tt>JT8</tt>, the time increments and final time values from the last execution are used again.
# Since there is no intervening <tt>DRAW</tt> command, the <tt>ANIMATE</tt> command is still active for this execution.
# When <tt>RECALL INPUT</tt> is attempted with no further data in the file, an error message is printed and control is returned to the user's terminal.
# The analysis of this system is terminated here and the IMP program is exited. Another analysis could have been initiated without exiting the IMP program by use of the <tt>CLEAR</tt> statement.

## A Front End Loader ##
The second example is the lift mechanism of a front end loader, with hydraulic coupling of the actuators simulated in the model. A drawing of the linkage is shown in the figure on the next page. The objective here is to design the loader to achieve maximum height while maintaining the horizontal position of the bucket.

The first portion of the simulation demonstrates the kinematic performance of the loader and also illustrates some of the graphic capabilities of IMP. The second portion examines the forces at particular joints during the lift operation with a load applied in the bucket. IMP's plotting capabilities are demonstrated here.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_8.png' />
_Figure 9-8_ Unnamed.

> <<< Notice >>>

> This is the Integrated Mechanisms Program (IMP-2000).
> (C)Copyright, JML Research, Inc., 1984-2000. All rights reserved.

> JML Research, Inc. is endeavoring to make this program as complete,
> accurate, and easy to use as possible. Suggestions and comments are
> welcomed. Any errors encountered in either the documentation or in the
> results should be immediately brought to our attention.

> Neither JML Research, Inc. nor those supplying the computer facilities
> for this analysis assume any responsibility for the validity, accuracy,
> or applicablitiy of any results obtained from this system; users must
> verify their own results.

  * 
  * Integrated Mechanisms Program (IMP-2000) *** Win/NT Version -- Released 01 Jan 2000**
  * on 20 Dec 99 at 11:23:58                 *****

> What kind of terminal are you using?
> alpha, graphic [graphic](graphic.md):> graphic

> > print input
> > recall input loader.dat
> TITLE=FRONT END LOADER

> REMARK: LINKAGE ASSEMBLY DEFINITION.
> ZERO(POSITION)=0.001
> ZPIN(L1,BASE)=J1
> DATA ZPIN(J1)=76.25,72.75,0/139.26,9,0 (1)
  * **Warning: 3 zeroes are added to complete statement.**
> ZPIN(L4,L1)=J2
> DATA ZPIN(J2)=83.6,65.75,0/112.556,52.479,0
  * **Warning: 3 zeroes are added to complete statement.**
> ZPIN(L3,L1)=J3
> DATA ZPIN(J3)=92.033,56.071,0
  * **Warning: 6 zeroes are added to complete statement.**
> PRISM(L2,L3)=J4
> DATA PRISM(J4)=88.298,50.385,0/92.033,56.071,0/0,0,0
> ZPIN(L2,BASE)=J5
> DATA ZPIN(J5)=66.2,18.25,0/92.033,56.071,0
  * **Warning: 3 zeroes are added to complete statement.**
> PRISM(L4,L5)=J6
> DATA PRISM(J6)=98.078,59.1145,0/112.556,52.479,0/0,0,0
> ZPIN(L7,L6)=J7
> DATA ZPIN(J7)=112.556,65.75,0
  * **Warning: 6 zeroes are added to complete statement.**
> ZPIN(L6,L1)=J8
> DATA ZPIN(J8)=112.556,39.487,0
  * **Warning: 6 zeroes are added to complete statement.**
> ZPIN(L5,L6)=J9
> DATA ZPIN(J9)=112.556,52.479,0/134.396,33.536,0/112.556,39.487,0
> ZPIN(L7,L8)=J13
> DATA ZPIN(J13)=139.26,25.125,0
  * **Warning: 6 zeroes are added to complete statement.**
> ZPIN(L1,L8)=J14
> DATA ZPIN(J14)=139.26,9,0
  * **Warning: 6 zeroes are added to complete statement.**
> REMARK: LINK SHAPE DEFINITIONS FOR FIGURES.
> SHOW(YELLOW)=L1
> POINT(L1)=P100,P101,P102,P103,P104,P105,P106,P107,P108,P109,P100
> DATA POINT(P100,J1) =0,0,40 (2)
> DATA POINT(P101,ABS)=78,65,40
> DATA POINT(P102,ABS)=95,40,40
> DATA POINT(P103,ABS)=118,20,40
> DATA POINT(P104,ABS)=135,6,40
> DATA POINT(P105,J14)=0,0,40
> DATA POINT(P106,ABS)=133.895,17.4434,40
> DATA POINT(P107,ABS)=125,28,40
> DATA POINT(P108,ABS)=102,60,40
> DATA POINT(P109,ABS)=80,73,40
> POINT(L1)=P110,P111,P112,P113,P114,P115,P116,P117,P118,P119,P110
> DATA POINT(P110,J1) =0,0,-40 (2)
> DATA POINT(P111,ABS)=78,65,-40
> DATA POINT(P112,ABS)=95,40,-40
> DATA POINT(P113,ABS)=118,20,-40
> DATA POINT(P114,ABS)=135,6,-40
> DATA POINT(P115,J14)=0,0,-40
> DATA POINT(P116,ABS)=133.895,17.4434,-40
> DATA POINT(P117,ABS)=125,28,-40
> DATA POINT(P118,ABS)=102,60,-40
> DATA POINT(P119,ABS)=80,73,-40
> SHOW(RED)=L2,L3
> POINT(L2)=P200,P201,P202,P203,P204,P200
> DATA POINT(P200,J5)=0,0,40
> DATA POINT(P201,J5)=2,-2,40
> DATA POINT(P202,J5)=39,-2,40
> DATA POINT(P203,J5)=39,2,40
> DATA POINT(P204,J5)=2,2,40
> POINT(L2)=P210,P211,P212,P213,P214,P210
> DATA POINT(P210,J5)=0,0,-40
> DATA POINT(P211,J5)=2,-2,-40
> DATA POINT(P212,J5)=39,-2,-40
> DATA POINT(P213,J5)=39,2,-40
> DATA POINT(P214,J5)=2,2,-40
> POINT(L3)=P300,P301
> DATA POINT(P300,J3)=0,0,40
> DATA POINT(P301,J4)=0,40,-29.8
> POINT(L3)=P310,P311
> DATA POINT(P310,J3)=0,0,-40
> DATA POINT(P311,J4)=0,-40,-29.8
> SHOW(GREEN)=L4,L5
> POINT(L4)=P400,P401,P402,P403,P404,P400
> DATA POINT(P400,J2)=0,0,40
> DATA POINT(P401,J2)=2,-2,40
> DATA POINT(P402,J2)=27,-2,40
> DATA POINT(P403,J2)=27,2,40
> DATA POINT(P404,J2)=2,2,40
> POINT(L4)=P410,P411,P412,P413,P414,P410
> DATA POINT(P410,J2)=0,0,-40
> DATA POINT(P411,J2)=2,-2,-40
> DATA POINT(P412,J2)=27,-2,-40
> DATA POINT(P413,J2)=27,2,-40
> DATA POINT(P414,J2)=2,2,-40
> POINT(L5)=P500,P501
> DATA POINT(P500,J9)=0,0,40
> DATA POINT(P501,J6)=0,-40,-7.75
> POINT(L5)=P510,P511
> DATA POINT(P510,J9)=0,0,-40
> DATA POINT(P511,J6)=0,40,-7.75
> SHOW(WHITE)=L6
> POINT(L6)=P600,P601,P602
> DATA POINT(P600,J8)=0,0,40
> DATA POINT(P601,J9)=0,0,40
> DATA POINT(P602,J7)=0,0,40
> POINT(L6)=P610,P611,P612
> DATA POINT(P610,J8)=0,0,-40
> DATA POINT(P611,J9)=0,0,-40
> DATA POINT(P612,J7)=0,0,-40
> SHOW(MAGENTA)=L7
> POINT(L7)=P700,P701
> DATA POINT(P700,J7)=0,0,40
> DATA POINT(P701,J13)=0,0,40
> POINT(L7)=P710,P711
> DATA POINT(P710,J7)=0,0,-40
> DATA POINT(P711,J13)=0,0,-40
> SHOW(CYAN)=L8
> POINT(L8)=P800,P801,P802,P803,P804,P800
> DATA POINT(P800,J13)=0,0,40
> DATA POINT(P801,J14)=0,0,40
> DATA POINT(P802,ABS)=139.26,0.0,40
> DATA POINT(P803,ABS)=172.56,0.0,40
> DATA POINT(P804,ABS)=146.26,25.125,40
> POINT(L8)=P810,P811,P812,P813,P814,P810
> DATA POINT(P810,J13)=0,0,-40
> DATA POINT(P811,J14)=0,0,-40
> DATA POINT(P812,ABS)=139.26,0,-40
> DATA POINT(P813,ABS)=172.56,0,-40
> DATA POINT(P814,ABS)=146.26,25.125,-40
> POINT(L8)=P800,P810
> POINT(L8)=P801,P811
> POINT(L8)=P802,P812
> POINT(L8)=P803,P813
> POINT(L8)=P804,P814
> SHOW(BLUE)=BASE
> POINT(BASE)=P900,P901,P902,P900
> DATA POINT(P900,J1)=0,0,40
> DATA POINT(P901,J1)=-5,-5,40
> DATA POINT(P902,J1)=5,-5,40
> POINT(BASE)=P910,P911,P912,P910
> DATA POINT(P910,J1)=0,0,-40
> DATA POINT(P911,J1)=-5,-5,-40
> DATA POINT(P912,J1)=5,-5,-40
> POINT(BASE)=P903,P904,P905,P903
> DATA POINT(P903,J5)=0,0,40
> DATA POINT(P904,J5)=-5,-5,40
> DATA POINT(P905,J5)=5,-5,40
> POINT(BASE)=P913,P914,P915,P913
> DATA POINT(P913,J5)=0,0,-40
> DATA POINT(P914,J5)=-5,-5,-40
> DATA POINT(P915,J5)=5,-5,-40
> REMARK: DRAW SCHEMATIC FIGURE.
> DATA VIEW=ISOMETRIC
> SLIDE (Y)=-20
> ZOOM(0.7)

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_9.png' />
_Figure 9-9_ Unnamed.

> Press 'ENTER' to continue: >

> REMARK: DEFINE ANGLE OF THE BUCKET WITH RESPECT TO GROUND.
> VALUE(ANGLE)=57.295\*ATAN2(POSIT(P803,2)-POSIT(P802,2),$ (3)
> POSIT(P803,1)-POSIT(P802,1))

> REMARK: RUN LOADER TO FULL LIFT POSITION.
> DATA POSITION(J4)=0,4.965,6 $$ INCREMENT HYDRAULIC CYLINDER J4.
> DATA TIME 6,1,1

> REMARK: DEFINE HYDRAULIC COUPLING BETWEEN CYLINDERS.
> VALUE(V)=0.3\*POSITION(J4,1) (4)
> DATA MOTION(J6)=V (5)

> REMARK: OUTPUT REQUESTS.
> LIST POSITION(J1,J14,P803)
> PLOT VALUE(ANGLE)
> PAUSE ON
> ANIMATE
> RETURN
> > exec hold
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_10.png' />
_Figure 9-10_ Unnamed.

> Press 'ENTER' to continue: >

> Listing of position of joint J1
> Time JVar 1
> 0.000000 45.334
  1. 000000 32.862
> 2.000000 20.364
> 3.000000 7.281
> 4.000000 -7.057

> 5.000000 -23.879
> 6.000000 -47.002
> Press 'ENTER' to continue: >

> Listing of position of joint J14
> Time JVar 1
> 0.000000 0.000
  1. 000000 -10.951
> 2.000000 -20.960
> 3.000000 -30.589
> 4.000000 -40.155

> 5.000000 -49.899
> 6.000000 -60.062
> Press 'ENTER' to continue: >
> Listing of position of point P803
> Time X Y Z
> 0.000000 172.560 0.000 40.000
  1. 000000 185.069 16.001 40.000
> 2.000000 194.130 34.911 40.000
> 3.000000 199.349 56.792 40.000
> 4.000000 199.656 82.025 40.000

> 5.000000 192.615 111.554 40.000
> 6.000000 170.339 148.479 40.000
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_11.png' />
_Figure 9-11_ Unnamed.

> Press 'ENTER' to continue: >

  * **The current position is set as reference.** (6)
> > reset (7)
> > recall input

> REMARK: TILT BUCKET TO DUMP POSITION.
> DATA POSITION(J4)=29.79 $$ HOLD CYLINDER J4 STATIONARY. (8)
  * **Input motion for joint J4 1 is redefined.**
> DATA POSITION(J6)=9,1,7 $$ INCREMENT CYLINDER J6. (9)
  * **Input motion for joint J6 1 is redefined.**
> DATA TIME 7,1,1
> RETURN
> > exec

> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_12.png' />
_Figure 9-12_ Unnamed.

> Press 'ENTER' to continue: >

> Listing of position of joint J1
> Time JVar 1
> 0.000000 -47.002
  1. 000000 -47.002
> 2.000000 -47.002
> 3.000000 -47.002
> 4.000000 -47.002

> 5.000000 -47.002
> 6.000000 -47.002
> 7.000000 -47.002
> Press 'ENTER' to continue: >

> Listing of position of joint J14
> Time JVar 1
> 0.000000 -60.505
  1. 000000 -67.728
> 2.000000 -75.396
> 3.000000 -83.675
> 4.000000 -92.818

> 5.000000 -103.247
> 6.000000 -115.774
> 7.000000 -132.441
> Press 'ENTER' to continue: >

> Listing of position of point P803
> Time X Y Z
> 0.000000 170.416 148.224 40.000
  1. 000000 171.401 143.991 40.000
> 2.000000 171.855 139.401 40.000
> 3.000000 171.653 134.425 40.000
> 4.000000 170.601 129.027 40.000

> 5.000000 168.373 123.167 40.000
> 6.000000 164.351 116.804 40.000
> 7.000000 157.051 109.972 40.000
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_13.png' />
_Figure 9-13_ Unnamed.

> Press 'ENTER' to continue: >
> > recall input

> REMARK: RETURN THE MODEL TO ITS ORIGINAL POSITION.
> DATA POSITION(J4)=29.79,-4.965,6 $$ INCREMENT CYLINDER J4 BACK DOWN.
  * **Input motion for joint J4 1 is redefined.**
> DATA MOTION(J6)=V $$ REESTABLISH COUPLING TO CYL. J4. (10)
  * **Input motion for joint J6 1 is redefined.**
> DATA TIME 6,1,1
> DELETE LIST ALL
> RETURN
> > exec hold

> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_14.png' />
_Figure 9-14_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_15.png' />
_Figure 9-15_ Unnamed.

> Press 'ENTER' to continue: >

  * **The current position is set as reference.** (6)
> > reset (7)
> Ø recall input
> Ø
> UNIT(MASS)=0.0025901
> DATA MASS(L8,J14)=1000/15,0,0 (11)
> DATA GRAVITY=0,-386.088,0
> DATA POSITION(J4)=0,4.965,6
  * **Input motion for joint J4 1 is redefined.**
> DATA MOTION(J6)=V (10)
  * **Input motion for joint J6 1 is redefined.**
> PLOT FORCE(J4,J6,J1,J3,J14) (12)
> RETURN
> > exec
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_16.png' />
_Figure 9-16_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_17.png' />
_Figure 9-17_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_18.png' />
_Figure 9-18_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_19.png' />
_Figure 9-19_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_20.png' />
_Figure 9-20_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_21.png' />
_Figure 9-21_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_22.png' />
_Figure 9-22_ Unnamed.

> Press 'ENTER' to continue: >

> > recall input

  * **RETURN statement simulated at end of file.**
> > end

### Notes: ###
# Note that this is actually a 2-D kinematic model of the loader. Only one set of links and joints are defined along the central plane of the model (Z = 0).
# In spite of note (1) above, the picture is made to appear 3- D by defining two sets of points, one at Z = 40 and the other at Z = -40
# Two of the points used to define the shape definition of the bucket for DRAW purposes are also used here to determine the angle of the bottom of the bucket with respect to ground.
# The result of this VALUE statement is that the variable V at all times has a value which is three tenths of the value of the rotation of joint J
# This statement causes the motion of the sliding joint J6 to be set by the value of the variable V, thus defining the hydraulic coupling between the actuators. The motion of J6 now becomes an SGC in the simulation.
# Because of the EXECUTE HOLD statement this message is a warning to the user that the geometry has not returned to its starting position.
# This RESET statement is required because of the previous EXECUTE HOLD. Without this RESET the value of time is not reset to zero for the beginning of the next EXECUTE.
# A new DATA POSITION statement is issued to fix the position of joint J4 at its current position; if this were not done, IMP would use the earlier data which determined the lift motion.
# This statement removes the dependence of the motion of joint J6 on the value of the variable V. 1
# Here, the hydraulic coupling is reestablished in the model. 1
# Note that mass units are consistent with the use of pounds, inches, and seconds. See UNIT(MASS) statement for details. 1
# The outputs requested are plots of the values of forces in specified joints of the model. In this simulation, these forces depend only on how the weight in the bucket is transmitted through the joints and links of the model and adds to weights of the other links.

## An Industrial Sewing Machine ##
The third example presented is a drive train for the thread looper in an industrial sewing machine. It is illustrated in the figure on the next page. The main crankshaft is driven by an electric motor at a speed of 8000 rpm. The purpose of the simulation is twofold: First, the designer is interested in the path of the tip of the thread looper since it must not interfere with the needle. Secondly, because of the high speed, there is concern about the dynamic bearing reactions throughout the cycle of operation.

The first of these two problems, being strictly geometric, is solved in kinematic mode. The second problem can also be solved in kinematic mode if it is assumed that the motor speed is constant under the variable dynamic load. This very reasonable assumption results in considerable saving over use of the dynamic mode. 1. Courtesy of Union Special Machine Company, Chicago, Illinois.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_23.png' />
_Figure 9-23_ Unnamed.

> <<< Notice >>>

> This is the Integrated Mechanisms Program (IMP-2000).
> (C)Copyright, JML Research, Inc., 1984-2000. All rights reserved.

> JML Research, Inc. is endeavoring to make this program as complete,
> accurate, and easy to use as possible. Suggestions and comments are
> welcomed. Any errors encountered in either the documentation or in the
> results should be immediately brought to our attention.

> Neither JML Research, Inc. nor those supplying the computer facilities
> for this analysis assume any responsibility for the validity, accuracy,
> or applicablitiy of any results obtained from this system; users must
> verify their own results.

  * 
  * Integrated Mechanisms Program (IMP-2000) *** Win/NT Version -- Released 01 Jan 2000**
  * on 21 Dec 99 at 09:25:28                 *****

> What kind of display are you using?
> alpha, graphic [graphic](graphic.md): > (1)

> > print input
> > recall input sewing.dat
> TITLE=SEWING MACHINE UPPER LOOPER DRIVE TRAIN

> REMARK: MODEL ASSEMBLY DATA.
> XPIN(BASE,SHFT)=MAIN (2) DATA XPIN(MAIN) =0.388,1.812,0
  * **Warning: 6 zeroes are added to complete statement.**
> SPHERE(ROD,SHFT)=LBAL
> DATA LINK(ROD, LBAL)=3.766,1.812,-.232;3.766,4.890,0;10,1.812,-.232
> DATA LINK(SHFT,LBAL)=3.766,1.812,-.232;10,1.812,-.232;3.766,1.812,-3
> UJOINT(ROD,LEVR)=UBAL (3) DATA UJOINT(UBAL) =3.766,4.890,0;3.766,4.658,3.083;5.000,4.890,0
> ZPIN(BASE,LEVR)=PIN
> DATA ZPIN(PIN) =4.625,4.890,0
  * **Warning: 6 zeroes are added to complete statement.**
> YSLIDE(FORK,LEVR)=SLIP (4) DATA YSLIDE(SLIP) =4.625,3.443,0.5
> SPHERE(FORK,ULPR)=BALL (4) DATA LINK(FORK,BALL)=4.625,3.443,0.5;10,3.443,0.5;4.625,4.890,0.5
> DATA LINK(ULPR,BALL)=4.625,3.443,0.5;4.625,3.443,3;4.625,4.890,0.5
> SCREW(BASE,ULPR)=CAM (5) DATA LINK(BASE,CAM) =3.080,3.443,0.5;10,3.443,0.5;3.080,3.443,3
> DATA LINK(ULPR,CAM) =3.080,3.443,0.5;10,3.443,0.5;3.080,3.443,3
> DATA SCREW(CAM) =3.60
> POINT(ULPR)=TIP
> DATA POINT(TIP,CAM) =0.500,0.242,-3.189
> UNIT(MASS)=0.0025901
> DATA MASS(ROD,LBAL) =0.204;,,1.300
> DATA INERTIA(ROD,LBAL)=0.00172,0.00166,0.00019
  * **Warning: 3 zeroes are added to complete statement.** (6) DATA MASS(ULPR,CAM) =0.158;0,0,-0.052
> DATA INERTIA(ULPR,CAM)=0.00057,0.00057,0
  * **Warning: 3 zeroes are added to complete statement.** (6) DATA MASS(LEVR,PIN) =0.137;0.116,-0.375,0.413
> DATA INERTIA(LEVR,PIN)=0.00046,0.00029,0.00021,,,-0.00004

> REMARK: INPUT MOTION INSTRUCTIONS.
> VALUE(DRIVE)=837.75\*TIME $$ INPUT DRIVE ANGLE AT 8000 RPM.
> DATA MOTION(MAIN)=DRIV
> DATA TIME=0.0075,0.00025,0.00025 $$ ONE REVOLUTION OF INPUT.

> REMARK: OUTPUT REQUESTS.
> LIST POSITION(TIP)
> PLOT VELOCITY(CAM,TIP)
> PLOT ACCEL(TIP)
> LIST FORCE(MAIN) (7) PLOT FORCE(MAIN, BALL) (7) PAUSE ON $$ SO THAT PLOTS CAN BE STUDIED.
> RETURN
> > execute

  * *** SEWING MACHINE UPPER LOOPER DRIVE TRAIN**
  * Kinematic Mode                          *** on 21 Dec 99 at 09:26:00**
  * 

> time = 0.000000
> time = 0.000250
> time = 0.000500
> time = 0.000750
> time = 0.001000
> time = 0.001250
> time = 0.001500
> time = 0.001750
> time = 0.002000
> time = 0.002250
> time = 0.002500
> time = 0.002750
> time = 0.003000
> time = 0.003250
> time = 0.003500
> time = 0.003750
> time = 0.004000
> time = 0.004250
> time = 0.004500
> time = 0.004750
> time = 0.005000
> time = 0.005250
> time = 0.005500
> time = 0.005750
> time = 0.006000
> time = 0.006250
> time = 0.006500
> time = 0.006750
> time = 0.007000
> time = 0.007250
> time = 0.007500
> Press 'ENTER' to continue: >
> Listing of position of point TIP
> Time X Y Z
> 0.000000 -0.109 3.201 1.000
> 0.000250 -0.191 3.275 1.029
> 0.000500 -0.271 3.350 1.048
> 0.000750 -0.347 3.423 1.055
> 0.001000 -0.414 3.488 1.054

> 0.001250 -0.469 3.541 1.047
> 0.001500 -0.508 3.578 1.039
> 0.001750 -0.528 3.597 1.034
> 0.002000 -0.528 3.597 1.034
> 0.002250 -0.508 3.578 1.039

> 0.002500 -0.469 3.541 1.047
> 0.002750 -0.414 3.488 1.054
> 0.003000 -0.347 3.423 1.055
> 0.003250 -0.271 3.350 1.048
> 0.003500 -0.191 3.275 1.029

> 0.003750 -0.109 3.201 1.000
> 0.004000 -0.028 3.133 0.961
> 0.004250 0.048 3.074 0.916
> 0.004500 0.118 3.027 0.868
> 0.004750 0.179 2.990 0.822

> 0.005000 0.227 2.965 0.782
> 0.005250 0.261 2.949 0.754
> 0.005500 0.279 2.941 0.738
> 0.005750 0.279 2.941 0.738
> 0.006000 0.261 2.949 0.754

> 0.006250 0.227 2.965 0.782
> 0.006500 0.179 2.990 0.822
> 0.006750 0.118 3.027 0.868
> 0.007000 0.048 3.074 0.916
> 0.007250 -0.028 3.133 0.961

> 0.007500 -0.109 3.201 1.000
> Press 'ENTER' to continue: >
> Listing of force in joint MAIN
> Time FX FY FZ MX MY MZ
> 0.000000 9.766 16.992 14.717 3.942 -51.981 57.397
> 0.000250 9.388 -30.258 18.152 -7.020 -63.497 -102.212
> 0.000500 7.247 -76.812 42.640 -17.820 -145.719 -259.472
> 0.000750 3.444 -115.923 89.009 -26.894 -301.472 -391.587
> 0.001000 -1.566 -138.480 154.629 -32.127 -521.973 -467.787

> 0.001250 -6.943 -134.778 230.353 -31.268 -776.523 -455.279
> 0.001500 -11.549 -99.322 299.325 -23.043 -1008.441 -335.511
> 0.001750 -14.226 -36.719 341.083 -8.519 -1148.877 -124.037
> 0.002000 -14.226 36.709 341.086 8.516 -1148.888 124.002
> 0.002250 -11.549 99.315 299.334 23.041 -1008.469 335.486

> 0.002500 -6.944 134.775 230.364 31.268 -776.559 455.269
> 0.002750 -1.567 138.482 154.639 32.128 -522.008 467.792
> 0.003000 3.443 115.928 89.018 26.895 -301.500 391.603
> 0.003250 7.247 76.819 42.645 17.822 -145.736 259.493
> 0.003500 9.388 30.265 18.154 7.021 -63.504 102.235

> 0.003750 9.766 -16.985 14.716 -3.940 -51.978 -57.375
> 0.004000 8.561 -60.139 30.365 -13.952 -104.560 -203.150
> 0.004250 6.152 -95.224 62.854 -22.092 -213.750 -321.667
> 0.004500 3.038 -118.161 109.256 -27.413 -369.772 -399.149
> 0.004750 -0.235 -124.641 164.793 -28.917 -556.617 -421.038

> 0.005000 -3.156 -111.198 221.709 -25.798 -748.201 -375.627
> 0.005250 -5.318 -77.373 269.402 -17.951 -908.805 -261.366
> 0.005500 -6.459 -27.794 296.860 -6.448 -1001.293 -93.890
> 0.005750 -6.459 27.771 296.866 6.443 -1001.314 93.810
> 0.006000 -5.318 77.354 269.419 17.946 -908.862 261.303

> 0.006250 -3.157 111.188 221.732 25.796 -748.279 375.592
> 0.006500 -0.237 124.640 164.818 28.916 -556.701 421.034
> 0.006750 3.036 118.168 109.279 27.415 -369.847 399.171
> 0.007000 6.151 95.237 62.872 22.095 -213.808 321.710
> 0.007250 8.561 60.156 30.376 13.956 -104.596 203.208

> 0.007500 9.766 17.005 14.719 3.945 -51.987 57.442
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_24.png' />
_Figure 9-24_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_25.png' />
_Figure 9-25_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_26.png' />
_Figure 9-26_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_27.png' />
_Figure 9-27_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_28.png' />
_Figure 9-28_ Unnamed.

> Press 'ENTER' to continue: >
> > end

### Notes: ###
# A carriage return was given for this question, thus accepting the default response which is "graphic". Though most output is printed lists, the "graphic" response is still neccessary to see plots.
# The GROUND statement is not necessary since the name BASE is chosen for the fixed link.
# Notice that the fork engaging the stud on the ball at the upper end of the connecting rod prevents rotation about the axis of the connecting rod. Thus, although this joint resembles a spheric joint, it is, in effect, equivalent to a universal joint.
# The joint at the forked end of the link LEVR is not of a type available in the IMP language. Therefore, it is remodelled as coincident ZSLIDE and SPHERE joints. The ZSLIDE joint allows sliding within the fork while the SPHERE joint allows complete freedom for rotation. Although the true fork is not able to rotate about one axis (along the link LEVR), this is prevented in the present model by the joints CAM and PIN.
# The curved slot in this barrel cam is a true helix. Thus, this joint is equivalent to a long lead screw.
# The products of inertia are interpreted as zero since they are not given explicitly.
# Note how the order in which the links are named in the joint definition statements determines which force is listed and plotted, the action or the reaction.

## A Left-Front Automotive Suspension ##
The fourth example presented is the left-front suspension system of a standard, midsize, passenger car. It was simulated as a part of a study done by the Vehicle Modeling Task Force of the Fatigue Design and Evaluation Committee of the Society of Automotive Engineers (SAE).

The suspension system modeled is shown in the figure on the next page. It can be noted that the vehicle frame is assumed stationary and that the steering arm is fixed to the frame. Thus, there is only one predominant motion possible, the jounce of the wheel.

In the first simulation presented, the equilibrium position is sought, while the geometry, and the forces in all joints are printed. This is followed by a second simulation in which the bottom of the tire is subjected to a deep hole at a speed corresponding to the first resonant frequency, the "wheel hop" frequency. VALUE statements are used to simulate the separation of the tire from the road, to allow impact with the jounce and rebound bumpers, and to change the shock absorber damping rates for extension and compression. Partial listings are presented of the dynamic mode simulation results. These were compared and correlated well with experimental results gathered by tests made for the committee under the same conditions by a major US auto company.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_29.png' />
_Figure 9-29_ Unnamed.

> <<< Notice >>>

> This is the Integrated Mechanisms Program (IMP-2000).
> (C)Copyright, JML Research, Inc., 1984-2000. All rights reserved.

> JML Research, Inc. is endeavoring to make this program as complete,
> accurate, and easy to use as possible. Suggestions and comments are
> welcomed. Any errors encountered in either the documentation or in the
> results should be immediately brought to our attention.

> Neither JML Research, Inc. nor those supplying the computer facilities
> for this analysis assume any responsibility for the validity, accuracy,
> or applicablitiy of any results obtained from this system; users must
> verify their own results.

  * 
  * Integrated Mechanisms Program (IMP-2000) *** Win/NT Version -- Released 01 Jan 2000**
  * on 02 Jan 2000 at 16:16:52               *****

> What kind of display are you using?
> alpha, graphic [graphic](graphic.md): >
> > print input
> > recall input demo\saetst.dat

> TITLE=SAE LEFT FRONT SUSPENSION MODEL
> REMARK: PREPARED FOR THE VEHICLE MODELING TASK FORCE OF THE $
> SAE FATIGUE DESIGN AND EVALUATION COMMITTEE $
> BY DR. J.J. UICKER, JR., UNIVERSITY OF WISCONSIN.

> GROUND=BODY
  * **The fixed link is redefined.**
> UNIT(MASS)=0.0025901 $$ CUSTOMARY US UNITS.
> DATA GRAVITY=0,0,-386.088 $$ GLOBAL Z IS UPWARD.

> REMARK: PROVISION FOR ROAD MOVEMENT WITH VEHICLE FRAME FIXED.
> ZSLIDE(BODY,ROAD)=BUMP $$ DRIVEN PER ROAD PROFILE. (1,2)

> REMARK: PRIMARY SUSPENSION MEMBERS
> REVOLUTE(BODY,LCA)=LPIN $$ LOWER CONTROL ARM PIVOT. (3)
> DATA REVOLUTE(LPIN)= 14.17, -6.19, 2.92; 9.34,-18.60, 3.36; $
> 26.23,-18.65, 2.92; 26.23,-18.65, 2.92
> DATA SPRING(LPIN)=28.0,0 $$ BUSHING STIFFNESS.
> DATA DAMPER(LPIN)=3.44 $$ BUSHING DAMPING.
> REVOLUTE(BODY,UCA)=UPIN $$ UPPER CONTROL ARM PIVOT.
> DATA REVOLUTE(UPIN)= 15.81,-12.30, 12.03; 14.69,-23.64, 14.86; $
> 24.40,-18.39, 12.03; 24.40,-18.39, 12.03
> DATA SPRING(UPIN)=38.4,0 $$ BUSHING STIFFNESS.
> DATA DAMPER(UPIN)=4.58 $$ BUSHING DAMPING.
> SPHERE(LCA,SPND)=LBAL $$ LOWER BALL JOINT.
> DATA LINK(LCA/LBAL)= 26.23,-18.65, 3.20; 17.81,-16.85, 2.52; $
> 24.40,-18.39, 13.99 $$ Z-AXIS ALONG LCA.
> DATA LINK(SPND/LBAL)=26.23,-18.65, 3.20; 24.40,-18.39, 13.99; $
  1. .81,-16.85, 2.52 $$ Z-AXIS UP SPINDLE.
> DATA SPRING(LBAL)=20.0,0.0;20.0,90.0;20.0,180.0
> DATA DAMPER(LBAL)=143.2;143.2;28.6 $$ BALL JOINT DAMPING.
> DATA MASS(LCA/LBAL)=15.85;0,0,8.64
> DATA INERTIA(LCA/LBAL)=1955.4,1646.5,389.9
  * **Warning: 3 zeroes are added to complete statement.**

> SPHERE(UCA,SPND)=UBAL $$ UPPER BALL JOINT.
> DATA LINK(UCA/UBAL)= 24.40,-18.39, 13.99; 20.71,-19.15, 14.37; $
> 26.23,-18.65, 3.20 $$ Z-AXIS ALONG UCA.
> DATA LINK(SPND/UBAL)=24.40,-18.39, 13.99; 26.23,-18.65, 3.20; $
> 20.71,-19.15, 14.37 $$ Z-AXIS DOWN SPINDLE.
> DATA SPRING(UBAL)=20.0,-180.0;20.0,90.0;20.0,0.0
> DATA DAMPER(UBAL)=143.2;143.2;28.6 $$ BALL JOINT DAMPING.
> DATA MASS(UCA/UBAL)=7.00;0,0,3.79
> DATA INERTIA(UCA/UBAL)=274.2,193.2,108.1
  * **Warning: 3 zeroes are added to complete statement.**

> REMARK: STEERING LOOP WITH TIE ROD BALL GROUNDED.
> UJOINT(SPND,TROD)=KBAL $$ KNUCKLE ARM BALL. (4)
> DATA UJOINT(KBAL)= 25.29,-25.01, 2.99; 25.29,-25.01, 12.99; $
> 25.29,-15.01, 2.99
> DATA DAMPER(KBAL)=143.2;143.2 $$ BALL JOINT DAMPING.
> POINT(SPND)=KPT
> DATA POINT(KPT,KBAL)=0,0,0
> SPHERE(BODY,TROD)=TBAL $$ GROUNDED TIE ROD END.
> DATA LINK(BODY/TBAL)= 7.30,-21.60, 3.41; 7.30,-21.60, 13.41; $
  1. .30,-21.60, 3.41 $$ GLOBAL AXES.
> DATA LINK(TROD/TBAL)= 7.30,-21.60, 3.41; 25.29,-25.01, 2.99; $
> 7.30,-21.60, 13.41 $$ Z-AXIS ALONG TIE ROD.
> DATA DAMPER(TBAL)=143.2;143.2;57.3 $$ ROD END DAMPING.
> DATA MASS(TROD/TBAL)=3.43;0,0,9.15
> DATA INERTIA(TROD/TBAL)=403.0,403.0,19.3
  * **Warning: 3 zeroes are added to complete statement.**

> REMARK:TIRE-ROAD INTERFACE
> XPIN(WHEL,SPND)=AXLE $$ ALLOW ROLL OF WHEEL. (5)
> DATA XPIN(AXLE)= 30.72,-18.57, 6.30; $
> 30.72,-18.57, 16.30; 30.72,-18.57, 16.30
> DATA MASS(SPND/AXLE)=29.90;1.31,1.38,-3.29
> DATA INERTIA(SPND/AXLE)=726.6,627.4,150.1,53.9,-125.9,-138.7
> DATA MASS(WHEL/AXLE)=67.45;0,0,0.32
> DATA INERTIA(WHEL/AXLE)=2590.0,2590.0,4567.0
  * **Warning: 3 zeroes are added to complete statement.**
> ZSLIDE(RIM,WHEL)=RIDE $$ ALLOW TIRE FLEXIBILITY. (5)
> DATA ZSLIDE(RIDE)= 30.72,-18.57, -6.25
> VALUE(NOFLEX)=0.83
> VALUE(TFLEX)=POSITION(RIDE,1)-NOFLEX
> VALUE(TSPG)=IF(TFLEX:1450,0,0) (6)
> DATA SPRING(RIDE)=TSPG,NOFLEX $$ TIRE STIFFNESS (6)
> VALUE(TDMP)=IF(TFLEX:0.30,0,0)
> DATA DAMPER(RIDE)=TDMP $$ TIRE DAMPING.
> YPIN(TIRE,RIM)=CMBR $$ ALLOW CAMBER CHANGES. (5)
> DATA YPIN(CMBR)= 30.72,-18.57, -6.25; $
> 40.72,-18.57, -6.25; 40.72,-18.57, -6.25
> FLAT(ROAD,TIRE)=PACH $$ ALLOW CASTOR/TREAD CHANGES. (5)
> DATA LINK(ROAD/PACH)= 0.00,-18.57, -6.25; 0.00,-18.57, 3.75; $
> 30.72,-18.57, -6.25
> DATA LINK(TIRE/PACH)=30.72,-18.57, -6.25; 30.72,-18.57, 3.75; $
> 40.72,-18.57, -6.25

> REMARK:SUSPENSION SPRING AND SHOCK ABSORBER.
> POINT(LCA)=P311,P317
> DATA POINT(P311/ABSO)=18.40,-17.64,-0.41 $$ SPRING BOTTOM. (7)
> DATA POINT(P317/ABSO)=18.88,-17.84,-0.10 $$ SHOCK ABSORBER BOTTOM.
> POINT(BODY)=P315,P320
> DATA POINT(P315/ABSO)=17.34,-16.91,10.08 $$ SPRING TOP.
> DATA POINT(P320/ABSO)=17.88,-17.20,11.03 $$ SHOCK ABSORBER TOP.
> SPRING(P311,P315)=SPNG $$ MAIN SUSPENSION SPRING.
> DATA SPRING(SPNG)=365.0,16.25
> DAMPER(P317,P320)=SHCK $$ MAIN SHOCK ABSORBER
> VALUE(CDIR)=VELOCITY(SHCK,1) $$ FIND SENSE OF MOTION.
> VALUE(CDMP)=IF(CDIR:5,5,10) $$ SET HIGHER IN TENSION. (8)
> DATA DAMPER(SHCK)=CDMP (8)
> SPRING(P317,P320)=STIF $$ SHOCK ABSORBER STIFFNESS.
> DATA SPRING(STIF)=100.0,11.0

> REMARK: JOUNCE AND REBOUND BUMPERS.
> POINT(LCA)=P348
> DATA POINT(P348/ABSO)=20.43,-21.02,5.20
> POINT(BODY)=P349,P351
> DATA POINT(P349/ABSO)=20.19,-20.87,6.41
> DATA POINT(P351/ABSO)=20.53,-19.63,11.38
> POINT(UCA)=P350
> DATA POINT(P350/ABSO)=21.02,-19.19,13.33
> SPRING(P348,P349)=JNCS $$ JOUNCE BUMPER STIFFNESS.
> VALUE(JOUNCE)=POSITION(JNCS,3)
> VALUE(JSPG)=IF(JOUNCE:170,0,0) (9)
> DATA SPRING(JNCS)=JSPG,0 (9)
> DAMPER(P348,P349)=JNCD $$ JOUNCE BUMPER DAMPING.
> VALUE(JDMP)=IF(JOUNCE:0.67,0,0) (9)
> DATA DAMPER(JNCD)=JDMP (9)
> SPRING(P350,P351)=RBNS $$ REBOUND BUMPER STIFFNESS.
> VALUE(RBOUND)=POSITION(RBNS,3)
> VALUE(RSPG)=IF(RBOUND:0,0,1730) (9)
> DATA SPRING(RBNS)=RSPG,0 (9)
> DAMPER(P350,P351)=RBND $$ REBOUND BUMPER DAMPING.
> VALUE(RDMP)=IF(RBOUND:0,0,1.70) (9)
> DATA DAMPER(RBND)=RDMP (9)

> REMARK: OPERATING CONDITIONS
> DATA POSITION(BUMP)=0 $$ FLAT ROAD PROFILE. (10)

> REMARK:OUTPUT REQUESTS.
> ZERO POSITION 0.000001 (11)
> ZERO EQUILIBRIUM 0.0001 (11)
> FIND EQUILIBRIUM
> PRINT HEADINGS
> PRINT POSITION(ALL)
> PRINT FORCE(ALL)
> PAUSE ON
> RETURN
> > execute hold (12)

  * *** SAE LEFT FRONT SUSPENSION MODEL**
  * Static Mode                     *** on 02 Jan 2000 at 16:17:40**
  * 

  * **'DATA TIME = 0.00000, 0.00000, 1.00000' is assumed.**
> time = 0.000000

> The Generalized Coordinates are:
> Joint Set by Position Velocity Acceleration
> BUMP 1 user 0.0000 0.000 0.000
> RIDE 1 imp 0.1947 0.000 0.000

> Equilibrium found after 2 search steps.
> Degree of freedom = 2. Quality index = 1.41e-005 with 3 iterations.

> Position Results:
> Item Name Magnitude X Y Z
> Joint BUMP 0.0000 0.0000 0.0000 0.0000
> Joint LPIN 0.6921 14.1700 -6.1900 2.9200
> Joint UPIN 1.2090 15.8100 -12.3000 12.0300
> Joint LBAL -1.1704 26.2307 -18.6435 3.3902
> 85.3931
  1. 1.1875
> Joint UBAL -180.3888 24.3890 -18.3422 14.1772
> 76.2229
> 0.5839
> Joint KBAL -0.0145 25.2947 -25.0049 3.2042
> -0.5780
> Joint TBAL 93.4583 7.3000 -21.6000 3.4100
> 79.2663
> 86.4998
> Joint AXLE -0.2253 30.7174 -18.5487 6.4947
> Joint RIDE 0.1947 30.7308 -18.5487 -6.0553
> Joint CMBR -0.0615 30.7310 -18.5487 -6.2500
> Joint PACH 0.0397 30.7310 -18.5487 -6.2500
> 30.7310
> -0.0059
> Point P311 25.5304 18.4415 -17.6527 -0.3120
> Point P317 26.0107 18.9180 -17.8511 0.0042
> Point P348 29.7711 20.4095 -21.0072 5.3352
> Point P350 31.4672 21.0273 -19.1607 13.4501
> Point KPT 35.7118 25.2947 -25.0049 3.2042
> Point P315 26.2341 17.3400 -16.9100 10.0800
> Point P320 27.1513 17.8800 -17.2000 11.0300
> Point P349 29.7369 20.1900 -20.8700 6.4100
> Point P351 30.5994 20.5300 -19.6300 11.3800
> Spg. SPNG 10.4766 -1.1015 0.7427 10.3920
> Spg. STIF 11.0936 -1.0380 0.6511 11.0258
> Spg. JNCS 1.1055 -0.2195 0.1372 1.0748
> Spg. RBNS 2.1801 -0.4973 -0.4693 -2.0701
> Dmp. SHCK 11.0936 -1.0380 0.6511 11.0258
> Dmp. JNCD 1.1055 -0.2195 0.1372 1.0748
> Dmp. RBND 2.1801 -0.4973 -0.4693 -2.0701

> Force Results:
> Magnitude X Y Z
> through Joint BUMP from Link BODY onto Link ROAD:
> Forc 1081.119 0.000 0.000 -1081.119
> Torq 38817.930 20074.939 33223.915 0.000
> through Joint LPIN from Link BODY onto Link LCA :
> Forc 1254.419 637.778 -1068.299 -159.824
> Torq 13185.198 10856.450 7482.417 19.379
> through Joint UPIN from Link BODY onto Link UCA :
> Forc 387.140 -365.260 -108.452 68.564
> Torq 2809.526 917.909 -2654.944 46.424
> through Joint LBAL from Link LCA onto Link SPND:
> Forc 1092.317 973.853 131.960 -476.817
> Torq 593.847 -23.409 -80.146 587.948
> through Joint UBAL from Link UCA onto Link SPND:
> Forc 386.489 60.853 -40.829 379.478
> Torq 287.238 -7.776 274.989 -82.621
> through Joint KBAL from Link SPND onto Link TROD:
> Forc 21.279 -20.816 3.944 -1.990
> Torq 0.000 0.000 0.000 0.000
> through Joint TBAL from Link BODY onto Link TROD:
> Forc 21.241 -20.820 3.939 -1.478
> Torq 0.000 0.000 0.000 0.000
> through Joint AXLE from Link WHEL onto Link SPND:
> Forc 1013.669 -1.087 -1013.668 0.000
> Torq 14.778 0.000 0.000 -14.778
> through Joint RIDE from Link RIM onto Link WHEL:
> Forc 1081.119 -1.160 0.000 -1081.118
> Torq 21.584 21.584 0.000 -0.023
> through Joint CMBR from Link TIRE onto Link RIM :
> Forc 1081.119 1081.119 0.000 0.000
> Torq 21.584 0.000 0.000 21.584
> through Joint PACH from Link ROAD onto Link TIRE:
> Forc 1081.119 0.000 0.000 -1081.119
> Torq 33223.915 -1.438 33223.915 0.000
> Spg. SPNG -2107.299
> Spg. STIF 9.364
> Spg. JNCS 0.000
> Spg. RBNS 0.000
> Dmp. SHCK 0.000
> Dmp. JNCD 0.000
> Dmp. RBND 0.000
> Press 'ENTER' to continue: >

  * **The current position is set as reference.** (12)
> > reset (13)

> > recall input

> DELETE PRINT(ALL)
> DELETE EQUILIBRIUM
> TITLE=A 2.95 INCH HAVERSINE HOLE AT 12.2 HZ.
> FIND DYNAMICS
> DATA TIME=0.25,0.0001,0.005
> ZERO FORC=20.0,5.0
> VALUE(OMEGA)=76.65 $$ DEFINE BUMP WAVELENGTH.
> VALUE(HIGH)=-2.95 $$ DEFINE BUMP HEIGHT.
> VALUE(WAVE)=0.5\*HIGH**(1-COS(OMEGA\*T)) $$ DEFINE BUMP SHAPE. (14)
> VALUE(ROAD)=IF(OMEGA\*T-2\*PI:WAVE,0,0) $$ DEFINE END OF BUMP.
> DATA MOTION(BUMP)=ROAD**

> REMARK: NEW OUTPUT REQUESTS.
> LIST POSITION(KPT)
> PLOT POSITION(RIDE,KPT)
> LIST FORCE(AXLE,PACH)
> PLOT FORCE(AXLE,PACH) (15)
> RETURN
> > execute

  * 
  * A 2.95 INCH HAVERSINE HOLE AT 12.2 HZ. *** Dynamic Mode**
  * on 02 Jan 2000 at 16:18:45             *****

> time = 0.000000
> time = 0.005000
> time = 0.010000
> time = 0.015000
> time = 0.020000
> time = 0.025000
> time = 0.030000
> time = 0.035000
> time = 0.040000
> time = 0.045000
> time = 0.050000
> time = 0.055000
> time = 0.060000
> time = 0.065000
> time = 0.070000
> time = 0.075000
> time = 0.080000
> time = 0.085000
> time = 0.090000
> time = 0.095000
> time = 0.100000
> time = 0.105000
> time = 0.110000
> time = 0.115000
> time = 0.120000
> time = 0.125000
> time = 0.130000
> time = 0.135000
> time = 0.140000
> time = 0.145000
> time = 0.150000
> time = 0.155000
> time = 0.160000
> time = 0.165000
> time = 0.170000
> time = 0.175000
> time = 0.180000
> time = 0.185000
> time = 0.190000
> time = 0.195000
> time = 0.200000
> time = 0.205000
> time = 0.210000
> time = 0.215000
> time = 0.220000
> time = 0.225000
> time = 0.230000
> time = 0.235000
> time = 0.240000
> time = 0.245000
> time = 0.250000
> Press 'ENTER' to continue: >

> Listing of position of point KPT
> Time X Y Z
> 0.000000 25.295 -25.005 3.204
> 0.005000 25.292 -25.008 3.086
> 0.010000 25.282 -25.015 2.748
> 0.015000 25.254 -25.020 2.233
> 0.020000 25.203 -25.019 1.609

> 0.025000 25.128 -25.009 0.963
> 0.030000 25.043 -24.992 0.390
> 0.035000 24.972 -24.975 -0.021
> 0.040000 24.937 -24.966 -0.202
> 0.045000 24.952 -24.970 -0.122

> 0.050000 25.012 -24.985 0.204
> 0.055000 25.094 -25.003 0.721
> 0.060000 25.175 -25.016 1.348
> 0.065000 25.237 -25.021 1.990
> 0.070000 25.273 -25.017 2.556

> 0.075000 25.289 -25.010 2.970
> 0.080000 25.294 -25.006 3.178
> 0.085000 25.295 -25.005 3.197
> 0.090000 25.295 -25.005 3.197
> 0.095000 25.295 -25.005 3.197

> 0.100000 25.295 -25.005 3.197
> 0.105000 25.295 -25.005 3.197
> 0.110000 25.295 -25.005 3.197
> 0.115000 25.295 -25.005 3.197
> 0.120000 25.295 -25.005 3.197

> 0.125000 25.295 -25.005 3.197
> 0.130000 25.295 -25.005 3.197
> 0.135000 25.295 -25.005 3.197
> 0.140000 25.295 -25.005 3.197
> 0.145000 25.295 -25.005 3.197

> 0.150000 25.295 -25.005 3.197
> 0.155000 25.295 -25.005 3.197
> 0.160000 25.295 -25.005 3.197
> 0.165000 25.295 -25.005 3.197
> 0.170000 25.295 -25.005 3.197

> 0.175000 25.295 -25.005 3.197
> 0.180000 25.295 -25.005 3.197
> 0.185000 25.295 -25.005 3.197
> 0.190000 25.295 -25.005 3.197
> 0.195000 25.295 -25.005 3.197

> 0.200000 25.295 -25.005 3.197
> 0.205000 25.295 -25.005 3.197
> 0.210000 25.295 -25.005 3.197
> 0.215000 25.295 -25.005 3.197
> 0.220000 25.295 -25.005 3.197

> 0.225000 25.295 -25.005 3.197
> 0.230000 25.295 -25.005 3.197
> 0.235000 25.295 -25.005 3.197
> 0.240000 25.295 -25.005 3.197
> 0.245000 25.295 -25.005 3.197

> 0.250000 25.295 -25.005 3.197

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_30.png' />
_Figure 9-30_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_31.png' />
_Figure 9-31_ Unnamed.

> Press 'ENTER' to continue: >

> Listing of force in joint AXLE (15)
> Time FX FY FZ MX MY MZ
> 0.000000 0.952 -955.579 11.249 0.000 -10.817 -53.576
> 0.005000 0.223 -912.306 6.291 0.000 -6.516 -26.581
> 0.010000 0.597 -878.665 2.527 0.000 -3.195 5.303
> 0.015000 2.489 -843.843 -1.131 0.000 1.845 29.532
> 0.020000 6.753 -802.643 -5.201 0.000 11.672 28.851

> 0.025000 14.206 -756.590 -9.532 0.000 28.546 -9.216
> 0.030000 24.022 -713.900 -13.609 0.000 51.156 -78.937
> 0.035000 33.220 -682.669 -16.787 0.000 72.999 -152.345
> 0.040000 37.914 -668.771 -18.290 0.000 84.414 -191.535
> 0.045000 35.890 -674.600 -17.657 0.000 79.433 -174.076

> 0.050000 28.049 -700.066 -15.063 0.000 60.606 -109.967
> 0.055000 17.826 -741.877 -11.147 0.000 36.839 -33.934
> 0.060000 8.934 -793.047 -6.547 0.000 16.545 19.066
> 0.065000 3.318 -844.827 -1.748 0.000 3.251 32.880
> 0.070000 0.845 -890.312 2.813 0.000 -3.897 13.375

> 0.075000 0.343 -924.435 6.564 0.000 -7.226 -19.465
> 0.080000 0.514 -942.737 8.696 0.000 -8.496 -42.246
> 0.085000 0.542 -944.325 8.886 0.000 -8.589 -44.448
> 0.090000 0.553 -944.894 8.950 0.000 -8.650 -44.682
> 0.095000 0.564 -945.457 9.013 0.000 -8.711 -44.914

> 0.100000 0.574 -945.975 9.071 0.000 -8.767 -45.127
> 0.105000 0.583 -946.453 9.125 0.000 -8.818 -45.324
> 0.110000 0.591 -946.896 9.175 0.000 -8.866 -45.506
> 0.115000 0.599 -947.307 9.221 0.000 -8.910 -45.675
> 0.120000 0.607 -947.689 9.264 0.000 -8.951 -45.832

> 0.125000 0.613 -948.046 9.304 0.000 -8.990 -45.978
> 0.130000 0.620 -948.386 9.342 0.000 -9.026 -46.118
> 0.135000 0.626 -948.705 9.378 0.000 -9.061 -46.249
> 0.140000 0.632 -949.004 9.411 0.000 -9.093 -46.371
> 0.145000 0.637 -949.285 9.443 0.000 -9.123 -46.487

> 0.150000 0.642 -949.550 9.473 0.000 -9.152 -46.595
> 0.155000 0.647 -949.800 9.501 0.000 -9.179 -46.697
> 0.160000 0.651 -950.036 9.527 0.000 -9.204 -46.794
> 0.165000 0.655 -950.259 9.553 0.000 -9.228 -46.886
> 0.170000 0.659 -950.471 9.576 0.000 -9.251 -46.973

> 0.175000 0.663 -950.672 9.599 0.000 -9.273 -47.055
> 0.180000 0.667 -950.864 9.620 0.000 -9.293 -47.133
> 0.185000 0.670 -951.046 9.641 0.000 -9.313 -47.208
> 0.190000 0.673 -951.219 9.660 0.000 -9.332 -47.279
> 0.195000 0.677 -951.385 9.679 0.000 -9.350 -47.347

> 0.200000 0.680 -951.543 9.697 0.000 -9.367 -47.412
> 0.205000 0.682 -951.694 9.714 0.000 -9.383 -47.473
> 0.210000 0.685 -951.839 9.730 0.000 -9.399 -47.533
> 0.215000 0.688 -951.977 9.746 0.000 -9.414 -47.589
> 0.220000 0.690 -952.110 9.760 0.000 -9.428 -47.644

> 0.225000 0.693 -952.238 9.775 0.000 -9.442 -47.696
> 0.230000 0.695 -952.360 9.789 0.000 -9.455 -47.746
> 0.235000 0.697 -952.478 9.802 0.000 -9.468 -47.794
> 0.240000 0.699 -952.591 9.815 0.000 -9.480 -47.840
> 0.245000 0.701 -952.700 9.827 0.000 -9.492 -47.885

> 0.250000 0.703 -952.805 9.839 0.000 -9.503 -47.928

> Press 'ENTER' to continue: >

> Listing of force in joint PACH (15)
> Time FX FY FZ MX MY MZ
> 0.000000 0.000 0.000 -921.160 -30.618 28308.187 0.000
> 0.005000 0.000 0.000 -922.098 -5.631 28331.466 0.000
> 0.010000 0.000 0.000 -922.212 35.464 28318.363 0.000
> 0.015000 0.000 0.000 -922.413 90.611 28297.210 0.000
> 0.020000 0.000 0.000 -923.389 154.347 28291.056 0.000

> 0.025000 0.000 0.000 -924.196 218.568 28275.478 0.000
> 0.030000 0.000 0.000 -924.852 274.508 28257.820 0.000
> 0.035000 0.000 0.000 -925.148 314.234 28239.045 0.000
> 0.040000 0.000 0.000 -925.172 331.685 28227.416 0.000
> 0.045000 0.000 0.000 -925.264 324.171 28235.657 0.000

> 0.050000 0.000 0.000 -925.794 292.910 28274.024 0.000
> 0.055000 0.000 0.000 -926.918 242.538 28342.976 0.000
> 0.060000 0.000 0.000 -928.414 179.918 28428.987 0.000
> 0.065000 0.000 0.000 -929.782 113.256 28509.497 0.000
> 0.070000 0.000 0.000 -930.776 51.524 28571.344 0.000

> 0.075000 0.000 0.000 -931.130 3.927 28603.348 0.000
> 0.080000 0.000 0.000 -931.233 -21.077 28616.526 0.000
> 0.085000 0.000 0.000 -931.242 -23.310 28617.668 0.000
> 0.090000 0.000 0.000 -931.232 -23.495 28617.366 0.000
> 0.095000 0.000 0.000 -931.222 -23.677 28617.067 0.000

> 0.100000 0.000 0.000 -931.213 -23.846 28616.792 0.000
> 0.105000 0.000 0.000 -931.205 -24.001 28616.538 0.000
> 0.110000 0.000 0.000 -931.197 -24.145 28616.303 0.000
> 0.115000 0.000 0.000 -931.190 -24.279 28616.085 0.000
> 0.120000 0.000 0.000 -931.184 -24.403 28615.881 0.000

> 0.125000 0.000 0.000 -931.178 -24.519 28615.692 0.000
> 0.130000 0.000 0.000 -931.172 -24.630 28615.511 0.000
> 0.135000 0.000 0.000 -931.166 -24.733 28615.342 0.000
> 0.140000 0.000 0.000 -931.161 -24.831 28615.183 0.000
> 0.145000 0.000 0.000 -931.156 -24.922 28615.034 0.000

> 0.150000 0.000 0.000 -931.152 -25.008 28614.894 0.000
> 0.155000 0.000 0.000 -931.147 -25.089 28614.761 0.000
> 0.160000 0.000 0.000 -931.143 -25.166 28614.636 0.000
> 0.165000 0.000 0.000 -931.139 -25.239 28614.517 0.000
> 0.170000 0.000 0.000 -931.136 -25.307 28614.404 0.000

> 0.175000 0.000 0.000 -931.132 -25.373 28614.298 0.000
> 0.180000 0.000 0.000 -931.129 -25.435 28614.196 0.000
> 0.185000 0.000 0.000 -931.126 -25.494 28614.099 0.000
> 0.190000 0.000 0.000 -931.123 -25.551 28614.007 0.000
> 0.195000 0.000 0.000 -931.120 -25.604 28613.919 0.000

> 0.200000 0.000 0.000 -931.117 -25.656 28613.835 0.000
> 0.205000 0.000 0.000 -931.115 -25.705 28613.755 0.000
> 0.210000 0.000 0.000 -931.112 -25.752 28613.678 0.000
> 0.215000 0.000 0.000 -931.110 -25.797 28613.605 0.000
> 0.220000 0.000 0.000 -931.107 -25.840 28613.534 0.000

> 0.225000 0.000 0.000 -931.105 -25.882 28613.467 0.000
> 0.230000 0.000 0.000 -931.103 -25.921 28613.402 0.000
> 0.235000 0.000 0.000 -931.101 -25.960 28613.339 0.000
> 0.240000 0.000 0.000 -931.099 -25.996 28613.279 0.000
> 0.245000 0.000 0.000 -931.097 -26.032 28613.221 0.000

> 0.250000 0.000 0.000 -931.095 -26.066 28613.165 0.000
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_32.png' />
_Figure 9-32_ Unnamed.

> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_33.png' />
_Figure 9-33_ Unnamed.

> Press 'ENTER' to continue: >

> > end

### Notes: ###
# Since link BODY is treated as stationary, provision must be made to allow the ROAD to move. The relative motion between these is controlled to correspond to the road profile, the bump shape passed over by the tire.
# Note that the BUMP joint is located colinear with the global Z axis. Since the ROAD link is completely rigid, the actual location of the BUMP axis is unimportant as long as its orientation is vertical.
# The upper and lower control arm pivots, UPIN and LPIN, could be modeled as cylindric joints with axial motion constraints, perhaps stiff springs. Here they are modeled as revolute joints.
# The actual ball joint at the spindle end of the tie rod is modeled as a universal joint; this eliminates the freedom of the tie rod to spin about its own axis.
# The flexibility of the tire and its freedom to roll on the road surface must be modeled in terms of fictitious links connected by joint types acceptable to IMP. Even though roll, castor, and camber angular movements may be small, joint freedoms must be provided for them.
# VALUE statements are used to represent the stiffness and damping of the tire in compression, with none in tension. This is very important when the tire leaves the road surface since the stiffness would go into tension.
# Note the use of global coordinate data rather than local data to locate certain points. Either is acceptable; the choice depends on the convenience of the user.
# A typical automotive shock absorber has different damping rates in tension and compression. This is modeled here by the use of VALUE statements.
# The jounce and rebound bumpers (not shown in the figure) are modeled as springs and dampers connecting the impact points. The stiffness and damping rates are set to zero when not in contact. 1
# The first simulation is an equilibrium search with the road height held constant. 1
# The default position tolerance is tightened here to allow a more accurate determination of the forces involved in the static equilibrium search. 1
# The simulation is ended with the model remaining in the equilibrium position. 1
# Time is reset to zero after the previous EXECUTE HOLD statement. This was not necessary since time did not change in the equilibrium search. It is a good practice, however, and is often required (see the earlier Front-End Loader example.) 1
# VALUE statements are used here to describe a single-cycle haversine hole as the road profile. 1
# Listings and plots of the requested positions and forces follow the simulation. The first column of each listing gives values of time; the next six columns represent the X,Y,Z components of the constraint force and torque, respectively.
## A Double Toggle Bench Clamp ##
The next example is the simulation of a double toggle bench clamp. This clamp could be used in many places in a manufacturing environment. The purpose of the clamp is to keep the clamping pad forced against a vertical surface holding an object in place while work is performed.

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_34.png' />
_Figure 9-34_ Unnamed.

> <<< Notice >>>

> This is the Integrated Mechanisms Program (IMP-2000).
> (C)Copyright, JML Research, Inc., 1984-2000. All rights reserved.

> JML Research, Inc. is endeavoring to make this program as complete,
> accurate, and easy to use as possible. Suggestions and comments are
> welcomed. Any errors encountered in either the documentation or in the
> results should be immediately brought to our attention.

> Neither JML Research, Inc. nor those supplying the computer facilities
> for this analysis assume any responsibility for the validity, accuracy,
> or applicablitiy of any results obtained from this system; users must
> verify their own results.

  * 
  * Integrated Mechanisms Program (IMP-2000) *** Win/NT Version -- Released 01 Jan 2000**
  * on 27 Dec 99 at 11:39:12                 *****

> What kind of display are you using?
> alpha, graphic [graphic](graphic.md); > graphic
> > print input
> > recall input clamp.dat
> TITLE=LAPEER DTV-1200 CLAMP
> SOLID READ AD = BARAD.geo (1)
> Solid 'AD' was read from file.
> SHAPE(BASE) = AD
> DATA DENSITY AD =0.260 (2)
> SOLID READ BD = BARBD.geo (1)
> Solid 'BD' was read from file.
> SHAPE (LKBD) = BD
> DATA DENSITY BD = 0.260 (2)
> DATA LINK (LKBD LINK) = 1.91,3.8,0; 1.91,3.8,10; 10,3.8,0 (3)
> ZPIN BASE LKBD = D
> DATA ZPIN D = -2.5,4,0; 10,4,0; 10,4,0
> SOLID READ AC = BARAC.geo (1)
> Solid 'AC' was read from file.
> SHAPE (LKAC) = AC
> DATA DENSITY AC = 0.260 (2)
> DATA LINK (LKAC LINK) = -0.5,4,0; -0.5,4,10; 10,4,0 (3)
> ZPIN BASE LKAC = A
> DATA ZPIN A = -0.5,2,0; 10,2,0; 10,2,0
> SOLID READ BC = BARBC.geo (1)
> Solid 'BC' was read from file.
> SHAPE (LKBC) = BC
> DATA DENSITY BC = 0.260 (2)
> DATA LINK (LKBC LINK) = -0.5,4,0; -0.5,4,10; 10,4,0 (3)
> ZPIN LKBD LKBC = B
> DATA ZPIN B = -0.5,4,0; 10,4,0; 10,4,0
> ZPIN LKAC LKBC = C
> DATA ZPIN C = -0.5,6,0; 10,6,0; 10,6,0
> SOLID READ CE = BARCE.geo (1)
> Solid 'CE' was read from file.
> SHAPE (LKCE) = CE
> DATA DENSITY CE = 0.260 (2)
> DATA LINK (LKCE LINK) = 2.06,5.72,0; 2.06,5.72,10; 4.60,5.44,0 (3)
> ZPIN LKAC LKCE = CC
> DATA ZPIN CC = -0.5,6,0; 10,6,0; 10,6,0
> SOLID READ EF = BAREF.geo (1)
> Solid 'EF' was read from file.
> SHAPE (LKEF) = EF
> DATA DENSITY EF = 0.260 (2)
> DATA LINK (LKEF LINK) = 3.94,4.7,0; 3.94,4.7,10; 4.60,5.44,0 (3)
> ZPIN LKCE LKEF = E
> DATA ZPIN E = 4.60,5.44,0; 2.06,5.72,0; 3.25,3.91,0
> ZPIN LKBD LKEF = F
> DATA ZPIN F = 3.25,3.91,0; 10,3.91,0; 4.60,5.44,0
> SOLID READ EG = BAREG.geo (1)
> Solid 'EG' was read from file.
> SHAPE (LKEG) = EG
> DATA DENSITY EG = 0.260 (2)
> DATA LINK (LKEG LINK) = 5.25,6.19,0; 5.25,6.19,10; 4.60,5.44,0 (3)
> ZPIN LKCE LKEG = EE
> DATA ZPIN EE = 4.60,5.44,0; 2.06,5.72,0; 5.9,6.95,0
> SOLID READ GH = BARGH.geo (1)
> Solid 'GH' was read from file.
> SHAPE (LKGH) = GH
> DATA DENSITY GH = 0.260 (2)
> POINT LKGH = F0 (4)
> DATA POINT F0 LINK = -4,-2.75,0
> POINT LKGH = F1 (4)
> DATA POINT F1 LINK = 0,0,0
> POINT LKGH = F2 (4)
> DATA POINT F2 LINK = 10,0,0
> DATA LINK (LKGH LINK) = 6.1,2.84,0; 6.1,2.84,10; 10,2.84,0 (3)
> ZPIN LKEG LKGH = G
> DATA ZPIN G = 5.9,6.95,0; 4.60,5.44,0; 10,6.95,0
> ZPIN LKBD LKGH = H
> DATA ZPIN H = 6.2,3.8.0; 10,3.8,0; 10,3.8.0
> DATA GRAVITY = 0,-386,0
> FORCE F0 F1 F2 = P (4)
> DATA FORCE P = 1200
> RETURN
> > data view isometric (5)
> >
> draw

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_35.png' />
_Figure 9-35_ Unnamed.

> > data view front
> > slide x 5.0
> > draw

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_36.png' />
_Figure 9-36_ Unnamed.

> > data position A = 0 30 2
> > animate
> > execute

  * 
  * JML Research, Inc.             *** Kinematic Mode**
  * on 27 Dec 99 at 11:43:22       *****

  * **'DATA TIME = 2.00000, 0.00000, 1.00000' is assumed.**
> time = 0.000000
> time = 1.000000
> time = 2.000000

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_37.png' />
_Figure 9-37_ Unnamed.

> > data position A = 0 4 15
  * **Input motion for joint A 1 is redefined.**
> > list position F0
> > plot position F0
> > pause on
> > execute
  * **'DATA TIME = 15.00000, 0.00000, 1.00000' is assumed.**
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >
> Press 'ENTER' to continue: >

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_38.png' />
_Figure 9-38_ Unnamed.

> Listing of position of point F0
> Time X Y Z
> 0.000000 2.100 0.090 0.000
  1. 000000 2.184 0.043 0.000
> 2.000000 2.396 -0.036 0.000
> 3.000000 2.698 -0.076 0.000
> 4.000000 3.077 -0.026 0.000

> 5.000000 3.523 0.156 0.000
> 6.000000 4.023 0.521 0.000
> 7.000000 4.549 1.125 0.000
> 8.000000 5.046 2.031 0.000
> 9.000000 5.409 3.282 0.000

  1. .000000 5.491 4.863 0.000
  1. .000000 5.136 6.640 0.000
  1. .000000 4.278 8.371 0.000
  1. .000000 3.004 9.800 0.000
  1. .000000 1.503 10.783 0.000

  1. .000000 -0.037 11.306 0.000

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_39.png' />
_Figure 9-39_ Unnamed.

> Press 'ENTER' to continue: >
> > end

### Notes: ###
# Here the LINK statement defines the existence of a link and the SOLID READ statement refers to a file which contains a solid geometric model of the shape of that link; the two are related by use of the SHAPE statement. In the first use here, the link named BASE becomes defined and its SOLID shape definition comes from a file named BARAD.geo in the users file area. See notes on the SHAPE statement in Chapter 3 and the file format definition in Appendix A for further details.
# If a solid geometric model of the link shape has been supplied (see note 1 above), then the DATA DENSITY statement can be used to cause automatic calculation of the mass, the center of mass, and the mass moments and products of inertia for that link. If this is done, then DATA MASS and DATA INERTIA statements need not be given. Note that the link and its shape must have been defined before the DATA DENSITY statement is given.
# When the solid model has been read from a file (see note 1 above) it is initially positioned at the associated link coordinate system location by the SHAPE statement. The link, including its solid shape, may then be moved to a new position and orientation by using the LINK option in the DATA LINK statement. This link may be moved to a new location either before or after other points or joints are connected to it; however, the form of the data for these connected items may be different depending on the order in which the steps are taken. See the DATA LINK statement of Chapter 4 for details.
# This force represents the resistance applied to the clamping pad, against which the clamp must be caused to close. Notice that the points F0, F1, and F2 were defined by previous POINT statements; points from the part shape file could not be used since they have no names by which to reference them.
# The DATA VIEW statement can be used to choose a viewing direction and to scale the picture to fit the screen.