# Language Specification/Guide #
Starting the 14th cycle the IMP language changed to a new format.  This format was designed to be efficient while maintaining an easy and understandable format.  We decided to exclude all unnecessary natural language so that experienced users will be able to code a model fast while still leave it in a format that new users can easily understand how to create a model.  Since most users will not know the new language here it is explained.


## Specifying a Model ##
When you first start a new model you will now need a new keyword and you will need to name the model.  This is to allow multiple models to be put into the same imp file.  Putting in multiple models per imp file will allow the program to run multiple models in a single simulation.  The parser differentiates between the models by the Model key word.  It will recognize the Model keyword and assign the name that follows it to the model.  Below is an example on how to define the model.
```
   Model {Model name}
```
**Example:**
```
     Model Hand;
```
  * Model Name can't have a number.
  * Model Name must have either letters or have an underscore before it.
  * Model statement must be ended with a semicolon.

## Delimited Statements ##
The Imp language will now support statements over multiple lines.  This will allow statements to have increased size but most statements won't use it.  All statements will need to be ended with a semicolon including the Model statement and the ground statement.  Below is an example.
```
      [Statement];
```
**Example:**
```
     Revo1 BodyA BodyB 0,0,0 1,1,1 2,2,2 3,3,3;
```
## Specifying Ground ##
You'll need to specify a body name for ground and make sure some joint uses that body name as one of their bodies to make sure the model has loop closure.  This will tell the program that this body will never move and will stay in its current place.
```
      Ground = {Body}
```
**Example:**
```
      Ground = Frame
```
  * Body name specified must not start with a number.  They must be preceded by a underscore or a letter.
  * Ground statement must be ended with a semicolon.
  * Not putting in a ground will give you an error of no ground mentioned and no loop closure.
  * Body name for ground doesn't have to be GROUND.

## Specifying a Joint ##
To create a new Joint you'll be using a new statement.  In the previous language you would create two statements to create a joint.  One would be the initial creation of the Joint while the other statement would tell the joint how exactly to act and where it was.  In the new language this has been combined down to one statement to make it easier to track joints and their data points.  Before you had to keep track of joints so you put the correct data statement with it.  Now you just specify what type of joint you want and what variables it goes with.  Below is a sample of creating a new Joint.
```
{Joint Type} {Joint Name} {Body 1} {Body 2} {Origin} {Point 1/Halfplane} {Point 2/Common Axis} etc... ;
```
  * Body names can't start with numbers.  They must be preceded by an underscore or a letter
  * Each point is separated by spaces while the individual x, y, and Z points are separated by a comma.
  * Joint names can't start with a number.  It must be preceded by an underscore or a letter like the bodies.
  * Each statement must be ended with a semicolon to tell the parser that this is the end of the statement.

### Revolute Joint ###
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_6.png' height='400px' />


The Revolute Joint is one of the basic joints in the program.  This Joint is the basis of the Pin joints.  Basic statement to create a Revolute Joint:
```
   Revolute JointName BodyBeforeName BodyAfterName Origin CommonAxis BodyAxisFirst BodyAxisSecond;
```
**Example:**
```
   Revolute Revo1 BodyA BodyB 0,0,0 1,0,2 1,1,1 2,2,2 -1,3,1;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

#### XPin ####
This Joint is a revolute joint that rotates on the X axis.
```
   XPIN !JointName Body1 Body2 Origin !BodyAxisFirst !BodyAxisSecond;
```
**Example:**
```
   XPin Xpin1 Body1 Body2 0,0,0 1,1,1 2,2,2;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

#### YPin ####
This Joint is a revolute joint that rotates on the Y axis.
```
   YPIN JointName Body1 Body2 Origin BodyAxisFirst BodyAxisSecond;
```
**Example:**
```
   YPin Ypin1 Body1 Body2 0,0,0 1,1,1 2,2,2;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

#### ZPin ####
This Joint is a revolute joint that rotates on the Z axis.
```
   ZPIN !JointName Body1 Body2 Origin !BodyAxisFirst !BodyAxisSecond;
```
**Example:**
```
   ZPin Zpin1 Body1 Body2 0,0,0 1,1,1 2,2,2;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

### Cylinder Joint ###
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_11.png' height='400px' />

**Example:**
```
   Cylinder Cy1 Body1 Body2 1,1,1 2,2,2 0,0,0;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

### Prism Joint ###
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_10.png' height='400px' />

This Joint is one of the basic joints.  It has Slide joints that are made of it.  The rotate in place on an axis.  Has the ability to slide along the joint.
```
   Prism !JointName Body1 Body2 Origin !HalfPlane !CommonAxis;
```
**Example:**
```
   Prism Pris Body1 Body2 8,8,8 9,9,9 5,5,5;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

#### XSlide ####
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_7.png' height='400px' />

This is a joint based off of the Prism joint.  This joint slides along the X axis.
```
   XSlide !JointName Body1 Body2 Origin;
```
**Example:**
```
   XSlide XSl Body1 Body2 8,8,8 9,9,9 5,5,5;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

#### YSlide ####
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_8.png' height='400px' />

This is a joint based off of the Prism joint.  This joint slides along the Y axis.
```
   YSlide !JointName Body1 Body2 Origin;
```
**Example:**
```
   YSlide YSl Body1 Body2 8,8,8 9,9,9 5,5,5;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

#### ZSlide ####
<img src='http://impsim.googlecode.com/svn/wiki/images/Manual_figure_ch4_9.png' height='400px' />

This is a joint based off of the Prism joint.  This joint slides along the Z axis.
```
   ZSlide !JointName Body1 Body2 Origin;
```
**Example:**
```
   ZSlide ZSl Body1 Body2 8,8,8 9,9,9 5,5,5;
```
  * Body Names and Joint Name can't start with a number.  Names must be preceded by an underscore or letter.
  * Statements must be ended by a semicolon.

## Specifying a Property ##
Some objects have some properties attached to them to make them run or show a certain body.  This can be done through the [.md](.md) brackets.  Most of the time this is used in the Camera properties and the models for the bodies
```
   Object Name[Property] = {Expression}
```
**Example:**
```
   CAMERA[UP] = 0,1,0;
```
  * Object/Joint names can't be started with a number.  They must be preceded by a underscore or a letter.
  * Forgetting one [.md](.md) bracket will make the program throw an error.
  * Statement must be ended with a semicolon.  This is where the multiple line statements will be most common as some of models might have long path names and this will tell the program where to stop.

## Supported Property Information ##
Below is the full specification for all supported properties.

### Object File Declaration ###
The most used function of the property value is the ability to define object files to display for each joint.
```
   JOINT[OBJ_FILE] = "filepath"
```
**Example:**
```
   J1[OBJ_FILE] = "joint.obj";
```
Where JOINT is the variable name declared for the desired joint and "filepath" is the absolute or relative path to the desired .obj file to display. This example will cause the "joint.obj" object file to draw itself on the screen with the joint's position as its origin and the joint's before matrix as its orientation. Using the term "NONE" will hide the joint from being displayed and using the term "DEFAULT" will have the joint display as though the object file were not defined.
### Axis Display Option ###
```
   JOINT[SHOW_AXIS] = "BEFORE"/"AFTER";
```
**Example:**
```
   J1[SHOW_AXIS] = "BEFORE";
```
Where JOINT is the variable name declared for the desired joint and "BEFORE"/"AFTER" is the desired orientation matrix of the joint to display. This will cause the joint's BEFORE or AFTER matrix to be visualized in 3D space by displaying its defined coordinate system at the joint's position.
### Camera Position Declaration ###
```
   CAMERA[UP] = {POINT};
   CAMERA[LOCATION] = {POINT};
   CAMERA[DIRECTION] = {POINT};
```
**Example:**
```
   CAMERA[UP]={0,1,0};
```
**Example:**
```
   CAMERA[DIRECTION]={0,0,-1};
```
**Example:**
```
   CAMEERA[LOCATION]={0,0,10};
```
The above example would define the camera to be 10 units from the origin looking down the negative Z axis. It would be ideal for viewing a mechanism positioned at the origin.
### Light Declaration ###
```
   LIGHT[LIGHT#] = "x,y,z,w, r,g,b,a ,r,g,b,a, r,g,b,a";
```
**Example:**
```
   LIGHT[LIGHT0] = "0,0,0,0, 0.5,0.5,0.5,0.5      0.7,0.7,0.7,0.7      1,1,1,1";
```
Where # is a sequential integer starting at 0 for each light being defined. x,y,z,w represent the position of the light source, and each RGBA set represents the ambient, diffuse, and specular light colors respectively.
## Specifying an Expression ##
In making a model you'll need to make expressions on the variables of the joint.  These are commonly done to specify how a joint will move.
```
   JointName.Variable = Expression;
```
**Example:**
```
    Revo1.theta = ticks() x -0.0011556;
```
  * Must have a period between the joint name and the variable
  * Joint Name must start with an underscore or a letter
  * Expression must be ended with a semicolon
  * ticks() is used to specify that each tick will move only so much that you times against it