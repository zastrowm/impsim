# Supported Property Information #

## Object File Declaration ##
The most used function of the property value is the ability to define object files to display for each joint.

`JOINT[OBJ_FILE] = "filepath"`

> _**Example:**_ `J1[OBJ_FILE] = "joint.obj";`

Where JOINT is the variable name declared for the desired joint and "filepath" is the absolute or relative path to the desired .obj file to display. This example will cause the "joint.obj" object file to draw itself on the screen with the joint's position as its origin and the joint's before matrix as its orientation. Using the term "NONE" will hide the joint from being displayed and using the term "DEFAULT" will have the joint display as though the object file were not defined.
## Axis Display Option ##

`JOINT[SHOW_AXIS] = "BEFORE"/"AFTER";`

> _**Example:**_ `J1[SHOW_AXIS] = "BEFORE";`

Where JOINT is the variable name declared for the desired joint and "BEFORE"/"AFTER" is the desired orientation matrix of the joint to display. This will cause the joint's BEFORE or AFTER matrix to be visualized in 3D space by displaying its defined coordinate system at the joint's position.
## Camera Position Declaration ##

`CAMERA[UP] = {POINT};`

`CAMERA[LOCATION] = {POINT};`

`CAMERA[DIRECTION] = {POINT};`

> _**Example:**_ `CAMERA[UP]={0,1,0};`

> _**Example:**_ `CAMERA[DIRECTION]={0,0,-1};`

> _**Example:**_ `CAMERA[LOCATION]={0,0,10};`

The above example would define the camera to be 10 units from the origin looking down the negative Z axis. It would be ideal for viewing a mechanism positioned at the origin.
## Light Declaration ##
`LIGHT[LIGHT#] = "x,y,z,w, r,g,b,a ,r,g,b,a, r,g,b,a";`

> _**Example:**_ `LIGHT[LIGHT0] = "0,0,0,0, 0.5,0.5,0.5,0.5      0.7,0.7,0.7,0.7      1,1,1,1";`

Where # is a sequential integer starting at 0 for each light being defined. x,y,z,w represent the position of the light source, and each RGBA set represents the ambient, diffuse, and specular light colors respectively.