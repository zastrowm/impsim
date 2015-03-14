## Creating a 3D Imp Model in IMP language ##

In this tutorial you will learn how to create a 4 bar mechanism that is drawn as a 3D Model. Doing so is fairly simple and requires that you assign an obj model to each joint you want drawn 3D. For additional examples of this you can see [this](jmanual_APIExamples.md) page. The steps to create the models are basically the same

First start with valid imp code. We will be starting with the code below which defines a wireframe 4bar object:

```
ZPIN J1 FRAME A 0,0,0 2,0,0 2,0,0;
ZPIN J2 A B 0,1,0 2,0,0 0,-2,0;
ZPIN J3 B C 1,1,0 -2,0,0 0,1,0;
ZPIN J4 C FRAME 1,0,0 0,1,0 2,0,0;
GROUND = FRAME;
J1.Theta = ticks() * 0.0174532925;
J2.Theta = ticks() * -0.0174532925;

CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {0,0,10};
CAMERA[DIRECTION] = {0,0,-1};
```
If you run the following code it should look like this:

<img src='http://impsim.googlecode.com/svn/wiki/images/wireframe.png' height='400px' />

If the following code is run, a four bar will be shown, but with wire frame graphics. We need to assign an obj model to each joint we want to be drawn with in 3D. These obj models can be made in any external modeling program such as blender. Blender is a free program that lets you create models and export them in different model formats including OBJ. Once you have made your obj models you will need to associate them with each joint using the OBJ\_FILE property:

```
ZPIN J1 FRAME A 0,0,0 2,0,0 2,0,0;
ZPIN J2 A B 0,1,0 2,0,0 0,-2,0;
ZPIN J3 B C 1,1,0 -2,0,0 0,1,0;
ZPIN J4 C FRAME 1,0,0 0,1,0 2,0,0;
GROUND = FRAME;
J1.Theta = ticks() * 0.0174532925;
J2.Theta = ticks() * -0.0174532925;

CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {0,0,10};
CAMERA[DIRECTION] = {0,0,-1};

#assign the file location of an obj model to each joint with the OBJ_FILE property. 
#sets J1 to be drawn using this model
J1[OBJ_FILE] = "resources/models/lowVertexModels/4bar.obj"; 
#sets J2 to be drawn using this model
J2[OBJ_FILE] = "resources/models/lowVertexModels/4bar.obj";  
#sets J3 to be drawn with this model
J3[OBJ_FILE] = "resources/models/lowVertexModels/4bar.obj"; 

```

That's it. Once you assign the file path of the location of the obj model to the joint the graphics system will take care of the rest. If you like, you can also add your own lights to the scene. If you don't default lights will be added for you. To create a light you will need to enter 4 groups of 4 values. Each 4 values represents a vector 4 component of the light. The values are position, specular, ambient, and diffuse. The following code creates two lights

```
ZPIN J1 FRAME A 0,0,0 2,0,0 2,0,0;
ZPIN J2 A B 0,1,0 2,0,0 0,-2,0;
ZPIN J3 B C 1,1,0 -2,0,0 0,1,0;
ZPIN J4 C FRAME 1,0,0 0,1,0 2,0,0;
GROUND = FRAME;
J1.Theta = ticks() * 0.0174532925;
J2.Theta = ticks() * -0.0174532925;

CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {0,0,10};
CAMERA[DIRECTION] = {0,0,-1};

#assign the file location of an obj model to each joint with the OBJ_FILE property. 
#sets J1 to be drawn using this model
J1[OBJ_FILE] = "resources/models/lowVertexModels/4bar.obj"; 
#sets J2 to be drawn using this model
J2[OBJ_FILE] = "resources/models/lowVertexModels/4bar.obj";  
#sets J3 to be drawn with this model
J3[OBJ_FILE] = "resources/models/lowVertexModels/4bar.obj"; 

#Add some lights to the scene
LIGHT[LIGHT0] = "1,0,1,1   ,.7,.1,.3,1,   .2,.4,.3,1,    .4,.2,.7,1";
LIGHT[LIGHT1] = "0,1,-1,1   ,.3,.7,.5,1,   .7,.7,.2,1,    .5,.4,.7,1";
```

The model should look something like this:

<img src='http://impsim.googlecode.com/svn/wiki/images/4Bar Screenshot.png' height='400px' />