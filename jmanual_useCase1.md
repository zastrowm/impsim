# Use Case 1 #

<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch9_1.png' height='400px' />

A differential control linkage, which is the kinematic model described in this use case.


This use case describes the flow of events between a modeler and the IMP system as the modeler defines the elements of a kinematic model. For this use case the [differential control linkage](Manual_Chapter9.md) model from [chapter 9](Manual_Chapter9.md) is used as an example model. Definition statements are covered in more detail in [chapter 3](Manual_Chapter3.md) of the IMP user manual.

# Actors #
> _**Modeler**_

> A person using the IMP system to define and analyze a kinematic model.

# Preconditions #
> _**IMP is Running**_

> The IMP system must be operational and ready to accept input for a new kinematic model.
> _**Modeler has Kinematic Model**_

> To ease the definition of the kinematic model in the IMP language, the modeler will have knowledge of the components (such as their names and types) of the kinematic model.

# Basic Flow #


&lt;hr&gt;


<table border='1'>
<tbody><tr>
<th> # </th><th> Modeler </th><th> IMP Engine<br>
</th></tr>
<tr>
<th> 1.<br>
</th><td> The modeler initiates this use case after starting the IMP application, with kinematic model in hand. For example, the modeler may begin by entering the command<br>
<pre>GROUND = FRAME<br>
</pre>
<p>The <tt><a href='/mediawiki/index.php/Physics_Engine:_User_Manual/Chapter_3#The_GROUND_Statement' title='Physics Engine: User Manual/Chapter 3'>GROUND</a></tt> command designates the link in the model which remains stationary and also defines the global coordinate system for the model.<br>
</p>
</td><td>
</td></tr>
<tr>
<th> 2.<br>
</th><td> </td><td> IMP responds that the given command has been executed and replies with any relevant information.  In this example, it replies with<br>
<pre>*** The fixed link is redefined. ***<br>
</pre>
<p>notifying the modeler that the default reference link has been set.<br>
</p>
</td></tr>
<tr>
<th> 3.<br>
</th><td> The modeler defines the links and joints and may enter commands similar to the following.<br>
<pre>YSLIDE (FRAME,A)   = JT1<br>
ZPIN   (A,C)       = JT2<br>
XSLIDE (C,D)       = JT3<br>
ZPIN   (S,D)       = JT4<br>
ZPIN   (FRAME,S)   = JT5<br>
ZPIN   (E,D)       = JT6<br>
ZPIN   (B,E)       = JT7<br>
ZPIN   (FRAME,B)   = JT8<br>
</pre>
<p>These statements define the <tt>LINK</tt>s <i>A</i>,<i>B</i>,<i>C</i>,<i>D</i>,<i>E</i>,<i>S</i>, and <i>FRAME</i>. The <tt><a href='/mediawiki/index.php/Physics_Engine:_User_Manual/Chapter_3#The_LINK_Statement' title='Physics Engine: User Manual/Chapter 3'>LINK</a></tt>s are connected by <tt>JOINT</tt>s of type: <tt><a href='/mediawiki/index.php/Physics_Engine:_User_Manual/Chapter_3#The_XSLIDE_Statement' title='Physics Engine: User Manual/Chapter 3'>XSLIDE</a></tt>, <tt><a href='/mediawiki/index.php/Physics_Engine:_User_Manual/Chapter_3#The_YSLIDE_Statement' title='Physics Engine: User Manual/Chapter 3'>YSLIDE</a></tt>, and <tt><a href='/mediawiki/index.php/Physics_Engine:_User_Manual/Chapter_3#The_ZPIN_Statement' title='Physics Engine: User Manual/Chapter 3'>ZPIN</a></tt>.<br>
</p>
</td><td>
</td></tr>
<tr>
<th> 4.<br>
</th><td> </td><td> There is no response from the IMP system, however the definition of the kinematic model is now complete.<br>
</td></tr></tbody></table>


&lt;/hr&gt;



# Alternate Flows #
> _**Syntax Error**_

> If a syntactual error occurs, the system responds by saying that it did not recognize the command and allows the modeler to try again.

> _**Reverse Order**_

> In the above example, the modeler defines the ground and then the joints and links.  The modeler may do this in the reverse order.

# Postconditions #
> _**Kinematic Model Defined**_

> At the conclusion of this use case, the links and joints of the differential control linkage will be defined, albeit without any numerical data such as positions or orientation.