# Examples #


## 4-Bar in API ##
```
Model model = new Model();
ch = new CommandHolder(model);
			
//define the mechanism
ch.addCommand(RevoluteCommand.CreateZPin("J1", "FRAME", "A", new Point(0,0,0), new Point(2,0,0), new Point(2,0,0)));
ch.addCommand(RevoluteCommand.CreateZPin("J2", "A", "B", new Point(0,1,0), new Point(2,0,0), new Point(0,-2,0)));
ch.addCommand(RevoluteCommand.CreateZPin("J3", "B", "C", new Point(1,1,0), new Point(-2,0,0), new Point(0,1,0)));
ch.addCommand(RevoluteCommand.CreateZPin("J4", "C", "FRAME", new Point(1,0,0), new Point(0,1,0), new Point(2,0,0)));
			                      
//sets the ground
ch.addCommand(new GroundCommand("FRAME"));
			        
//sets J1 and J2 to rotate 0.02 and -0.02 per tick respectively
FakeExpression[] expression1 = new FakeExpression[2];
expression1[0] = new Function("", "TICKS");
expression1[1] = new FakeExpressionLiteral(0.02);
ch.addCommand(new JointExpressionCommand("J1", JVAR.THETA, new Function("", "*", expression1)));
			                        
FakeExpression[] expression2 = new FakeExpression[2];
expression2[0] = new Function("", "TICKS");
expression2[1] = new FakeExpressionLiteral(-0.02);
ch.addCommand(new JointExpressionCommand("J2", JVAR.THETA, new Function("", "*", expression2)));
			
//Defines which object files to use
FakeExpression literal = new FakeExpressionLiteral("<Path to Project>/models/4bar/4bar.obj");
ch.addCommand(new PropertyAssignmentCommand("J1","OBJ_FILE", literal));
ch.addCommand(new PropertyAssignmentCommand("J2","OBJ_FILE", literal));
ch.addCommand(new PropertyAssignmentCommand("J3","OBJ_FILE", literal));
			
			
//sets the lighting properties
literal = new FakeExpressionLiteral("1,0,1,1, .7, .1, .3, 1, .2, .4, .3, 1,  .4, .2, .7, 1");
ch.addCommand(new PropertyAssignmentCommand("LIGHT","LIGHT0", literal));
			
literal = new FakeExpressionLiteral("0,1,-1,1, .3, .7, .5, 1, .7, .7, .2, 1, .5, .4, .7, 1");
ch.addCommand(new PropertyAssignmentCommand("LIGHT","LIGHT1", literal));
			
```

<img src='http://impsim.googlecode.com/svn/wiki/images/4Bar Textured.png' />

## 4-Bar in IMP Language ##
```
ZPIN J1 FRAME A 0,0,0 2,0,0 2,0,0;
ZPIN J2 A B 0,1,0 2,0,0 0,-2,0;
ZPIN J3 B C 1,1,0 -2,0,0 0,1,0;
ZPIN J4 C FRAME 1,0,0 0,1,0 2,0,0;

#Sets the ground to the body "FRAME"
GROUND = FRAME;

#Sets J1 and J2 to rotate 0.02 and -0.02 degrees per tick respectively
J1.Theta = ticks() * 0.02;
J2.Theta = ticks() * -0.02;

#Sets the object files for the joints
J1[OBJ_FILE] = "models/4bar/4bar.obj"; 
J2[OBJ_FILE] = "models/4bar/4bar.obj"; 
J3[OBJ_FILE] = "models/4bar/4bar.obj"; 

#Explicitly sets the camera values
#Note: The values here are the same as the default values
CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {0,0,10};
CAMERA[DIRECTION] = {0,0,-1};

#Sets the light properties for Light 0
#The parameters are Position, Ambient, Diffuse, Specular
#xyzw, rgba, rgba, rgba respectively
LIGHT[LIGHT0] = "1,0,1,1   ,.7,.1,.3,1,   .2,.4,.3,1,    .4,.2,.7,1";

#Sets the light properties for Light 1
#The parameters are Position, Ambient, Diffuse, Specular
#xyzw, rgba, rgba, rgba respectively
LIGHT[LIGHT1] = "0,1,-1,1   ,.3,.7,.5,1,   .7,.7,.2,1,    .5,.4,.7,1";


```

<img src='http://impsim.googlecode.com/svn/wiki/images/4Bar Textured.png' />

## Piston in API ##
```
Model model = new Model();
ch = new CommandHolder(model);
ch.addCommand(RevoluteCommand.CreateZPin("R1", "G", "One", new Point(0,0,0), new Point(10,0,0), new Point(0,3,0)));
ch.addCommand(RevoluteCommand.CreateZPin("R2", "One", "Two", new Point(0,3,0), new Point(0,0,0), new Point(4,0,0)));
ch.addCommand(RevoluteCommand.CreateZPin("R3", "Two", "Three", new Point(4,0,0), new Point(0,3,0), new Point(10,0,0)));
ch.addCommand(PrismCommand.CreateXSlide("P", "Three", "G", new Point(4,0,0)));
			
ch.addCommand(new GroundCommand("G"));
		
FakeExpression[] expression1 = new FakeExpression[2];
expression1[0] = new Function("", "TICKS");
expression1[1] = new FakeExpressionLiteral(0.0174532925);
ch.addCommand(new JointExpressionCommand("R1", JVAR.THETA, new Function("", "*", expression1)));
			
```

<img src='http://impsim.googlecode.com/svn/wiki/images/piston textured.png' />

## Piston in IMP Language ##
```
MODEL M4;

ZPIN R1 G One 0,0,0 10,0,0 0,3,0;
ZPIN R2 One Two 0,3,0 0,0,0 4,0,0;
ZPIN R3 Two Three 4,0,0 0,3,0 10,0,0;
XSLIDE P Three G 4,0,0;

#Sets the ground to the body "G"
GROUND = G;

#Sets R1 to rotate -0.2 degrees per tick
R1.Theta = ticks() * -0.02;

#Override the default camera location
CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {0,0,40};
CAMERA[DIRECTION] = {0,0,-1};

#Set the object files for each joint
R2[OBJ_FILE] = "models/piston/pistonBar_short.obj";
R3[OBJ_FILE] = "models/piston/pistonBar.obj";
P[OBJ_FILE] = "models/piston/cylinder.obj";

#Sets the light properties for Light 0
#The parameters are Position, Ambient, Diffuse, Specular
#xyzw, rgba, rgba, rgba respectively
LIGHT[LIGHT0] = "10,0,10,1   ,.7,.1,.3,1,   .2,.4,.3,1,    .4,.2,.7,1";

#Sets the light properties for Light 1
#The parameters are Position, Ambient, Diffuse, Specular
#xyzw, rgba, rgba, rgba respectively
LIGHT[LIGHT1] = "0,10,-10,1   ,.3,.7,.5,1,   .7,.7,.2,1,    .5,.4,.7,1";
```

<img src='http://impsim.googlecode.com/svn/wiki/images/piston textured.png' />

## Stirling Engine in API ##
```
Model model = new Model();
ch = new CommandHolder(model);
			
//define the mechanism
ch.addCommand(RevoluteCommand.CreateZPin("A", "frame", "AB", new Point(0,0,0), new Point(10,0,0), new Point(10,5,0)));
ch.addCommand(RevoluteCommand.CreateZPin("B", "AB", "BD", new Point(10,5,0), new Point(0,0,0), new Point(0,30,0)));
ch.addCommand(RevoluteCommand.CreateZPin("D2", "BD", "DD", new Point(0,30,0), new Point(10,5,0), new Point(0,40,0)));
			                        
ch.addCommand(PrismCommand.CreateYSlide("D", "DD", "frame", new Point(0,30,0)));
			                        
ch.addCommand(RevoluteCommand.CreateZPin("F", "frame", "FE", new Point(-20,20,0), new Point(-10,20,0), new Point(-8,24,0)));
ch.addCommand(RevoluteCommand.CreateZPin("E", "FE", "HE", new Point(-8,24,0), new Point(-20,20,0), new Point(-14,8,0)));
ch.addCommand(RevoluteCommand.CreateZPin("H", "HE", "FH", new Point(-14,8,0), new Point(-8,24,0), new Point(-20,20,0)));
ch.addCommand(RevoluteCommand.CreateZPin("F2", "FH", "frame", new Point(-20,20,0), new Point(-14,8,0), new Point(-10,20,0)));
			
ch.addCommand(RevoluteCommand.CreateZPin("H2", "HE", "HI", new Point(-14,8,0), new Point(-8,24,0), new Point(7,12.5,0)));
ch.addCommand(RevoluteCommand.CreateZPin("I", "HI", "BD", new Point(7, 12.5, 0), new Point(-14,8,0), new Point(0,30,0)));
ch.addCommand(RevoluteCommand.CreateZPin("G2", "ED", "GG", new Point(0,48,0), new Point(-8,24,0), new Point(0,58,0)));
ch.addCommand(RevoluteCommand.CreateZPin("E2", "FE", "ED", new Point(-8,24,0), new Point(0,36,0), new Point(-20,20,0)));
			        
ch.addCommand(PrismCommand.CreateYSlide("G", "GG", "frame", new Point(0,48,0)));
			        
//define the ground
ch.addCommand(new GroundCommand("frame"));
			        
//set A to rotate
FakeExpression[] expression1 = new FakeExpression[2];
expression1[0] = new Function("", "TICKS");
expression1[1] = new FakeExpressionLiteral(-0.02);
ch.addCommand(new JointExpressionCommand("A", JVAR.THETA, new Function("", "*", expression1)));
			
//define the object files to use
FakeExpression literal = new FakeExpressionLiteral("models/stirling/stirling_B.obj");
ch.addCommand(new PropertyAssignmentCommand("B", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/stirling/stirling_D2.obj");
ch.addCommand(new PropertyAssignmentCommand("D2", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/stirling/cylinder.obj");
ch.addCommand(new PropertyAssignmentCommand("D", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/stirling/triplate.obj");
ch.addCommand(new PropertyAssignmentCommand("F", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("AFTER");
ch.addCommand(new PropertyAssignmentCommand("F", "SHOW_AXIS", literal));
			
literal = new FakeExpressionLiteral("models/stirling/stirling_I.obj");
ch.addCommand(new PropertyAssignmentCommand("I", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/stirling/cylinder2.obj");
ch.addCommand(new PropertyAssignmentCommand("G2", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/stirling/stirling_E2.obj");
ch.addCommand(new PropertyAssignmentCommand("E2", "OBJ_FILE", literal));
			
//define the camera position
literal = new FakeExpressionLiteral(new Point(0,1,0));
ch.addCommand(new PropertyAssignmentCommand("CAMERA", "UP", literal));
literal = new FakeExpressionLiteral(new Point(-10,20,100));
ch.addCommand(new PropertyAssignmentCommand("CAMERA", "LOCATION", literal));
literal = new FakeExpressionLiteral(new Point(0,0,-1));
ch.addCommand(new PropertyAssignmentCommand("CAMERA", "DIRECTION", literal));
			
//sets the lighting properties
literal = new FakeExpressionLiteral("10,0,10,1, .1, .1, .1, 1, .1, .1, .1, 1,  .1, .1, .1, 1");
ch.addCommand(new PropertyAssignmentCommand("LIGHT","LIGHT0", literal));
			                        
literal = new FakeExpressionLiteral("0,10,-10,1, .1, .1, .1, 1, .1, .1, .1, 1,  .1, .1, .1, 1");
ch.addCommand(new PropertyAssignmentCommand("LIGHT","LIGHT1", literal));
```

<img src='http://impsim.googlecode.com/svn/wiki/images/sterling engine textured.png' />

## Sterling Engine in IMP ##
```
MODEL M5;

ZPIN A frame AB 0,0,0 10,0,0 10,5,0;
ZPIN B AB BD 10,5,0 0,0,0 0,30,0;
ZPIN D2 BD DD 0,30,0 10,5,0 0,40,0;
YSLIDE D DD frame 0,30,0; #bottom piston

#triangle
ZPIN F frame FE -20,20,0 -10,20,0 -8,24,0;
ZPIN E FE HE -8,24,0 -20,20,0 -14,8,0;
ZPIN H HE FH -14,8,0 -8,24,0 -20,20,0;
ZPIN F2 FH frame -20,20,0 -14,8,0 -10,20,0;
#end triangle

ZPIN H2 HE HI -14,8,0 -8,24,0 7,12.5,0;
ZPIN I HI BD 7,12.5,0 -14,8,0 0,30,0;
ZPIN G2 ED GG 0,48,0 -8,24,0 0,58,0;
ZPIN E2 FE ED -8,24,0 0,36,0 -20,20,0;
YSLIDE G GG frame 0,48,0; #top piston

#Sets the ground to the body named "frame"
GROUND = frame;

#Sets the joint A to rotate -0.02 degrees each tick
A.Theta = ticks() * -0.02;

#Modifies the camera position
CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {-10,20,100};
CAMERA[DIRECTION] = {0,0,-1};

#Defines the object files for each joint
B[OBJ_FILE] = "models/stirling/stirling_B.obj";
D2[OBJ_FILE] = "models/stirling/stirling_D2.obj";
D[OBJ_FILE] = "models/stirling/cylinder.obj";
F[OBJ_FILE] = "models/stirling/triplate.obj";

I[OBJ_FILE] = "models/stirling/stirling_I.obj";
G2[OBJ_FILE] = "models/stirling/cylinder2.obj";
E2[OBJ_FILE] = "models/stirling/stirling_E2.obj";

#Sets the lighting values for Light 0
#The parameters are Position, Ambient, Diffuse, Specular
#xyzw, rgba, rgba, rgba respectively
LIGHT[LIGHT0] = "10,0,10,1   ,.1,.1,.1,1,   .1,.1,.1,1,    .1,.1,.1,1";

#Sets the lighting values for Light 1
#The parameters are Position, Ambient, Diffuse, Specular
#xyzw, rgba, rgba, rgba respectively
LIGHT[LIGHT1] = "0,10,-10,1   ,.1,.1,.1,1,   .1,.1,.1,1,    .1,.1,.1,1";
```

<img src='http://impsim.googlecode.com/svn/wiki/images/sterling engine textured.png' />

## Peaucellier Linkage in API ##
```
Model model = new Model();
ch = new CommandHolder(model);
			
//define the mechanism
ch.addCommand(RevoluteCommand.CreateZPin("O", "FRAME", "L", new Point(-58,0,0), new Point(10,0,0), new Point(0,-188,0)));
	                        
ch.addCommand(RevoluteCommand.CreateZPin("B", "L", "S", new Point(0,18,0), new Point(10,0,0), new Point(-21.5,0,0)));
ch.addCommand(RevoluteCommand.CreateZPin("Q", "S", "R", new Point(15,0,0), new Point(-25,0,0), new Point(-21,30,0)));
ch.addCommand(RevoluteCommand.CreateZPin("D", "R", "A", new Point(0,-18,0), new Point(-30,30,0), new Point(11.8, 20, 0)));
ch.addCommand(RevoluteCommand.CreateZPin("V", "A", "FRAME", new Point(-58,0,0), new Point(10,0,0), new Point(-27.5, -10,0)));
ch.addCommand(RevoluteCommand.CreateZPin("P", "M", "C", new Point(-15,0,0), new Point(10,0,0), new Point(-27.5, -10,0)));
ch.addCommand(RevoluteCommand.CreateZPin("B2", "M", "S", new Point(0,18,0), new Point(10,18,0), new Point(10,18,0)));
ch.addCommand(RevoluteCommand.CreateZPin("D2", "C", "R", new Point(0,-18,0), new Point(10,-18,0), new Point(10,-18,0)));
ch.addCommand(RevoluteCommand.CreateZPin("Op", "FRAME", "T", new Point(-38,0,0), new Point(10,0,0), new Point(10,0,0)));
ch.addCommand(RevoluteCommand.CreateZPin("P2", "M", "T", new Point(-15,0,0), new Point(10,0,0), new Point(-15,100,0)));
			                        
ch.addCommand(RevoluteCommand.CreateZPin("J1", "FRAME", "L1", new Point(-25,-15,0), new Point(0,-15,0), new Point(0,-15,0)));
ch.addCommand(RevoluteCommand.CreateZPin("J2", "L1", "L2", new Point(-16,-15,0), new Point(0,-15,0), new Point(0,-15,0)));
ch.addCommand(RevoluteCommand.CreateZPin("J3", "L2", "T", new Point(-25,0,0), new Point(0,0,0), new Point(0,0,0)));
			                
//define the ground
ch.addCommand(new GroundCommand("FRAME"));                      
			                   
//set J1 to rotate
FakeExpression[] expression1 = new FakeExpression[2];
expression1[0] = new Function("", "TICKS");
expression1[1] = new FakeExpressionLiteral(0.01);
ch.addCommand(new JointExpressionCommand("J1", JVAR.THETA, new Function("", "*", expression1)));
			
//define the object files to use
FakeExpression literal = new FakeExpressionLiteral("models/peaucellier/model_O.obj");
ch.addCommand(new PropertyAssignmentCommand("O", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/peaucellier/model_B.obj");
ch.addCommand(new PropertyAssignmentCommand("B", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/peaucellier/model_Q.obj");
ch.addCommand(new PropertyAssignmentCommand("Q", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/peaucellier/model_D.obj");
ch.addCommand(new PropertyAssignmentCommand("D", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/peaucellier/model_P.obj");
ch.addCommand(new PropertyAssignmentCommand("P", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/peaucellier/model_P2.obj");
ch.addCommand(new PropertyAssignmentCommand("P2", "OBJ_FILE", literal));
literal = new FakeExpressionLiteral("models/peaucellier/model_B2.obj");
ch.addCommand(new PropertyAssignmentCommand("B2", "OBJ_FILE", literal));
			
//define the camera position
literal = new FakeExpressionLiteral(new Point(0,1,0));
ch.addCommand(new PropertyAssignmentCommand("CAMERA", "UP", literal));
literal = new FakeExpressionLiteral(new Point(-25,0,110));
ch.addCommand(new PropertyAssignmentCommand("CAMERA", "LOCATION", literal));
literal = new FakeExpressionLiteral(new Point(0,0,-1));
ch.addCommand(new PropertyAssignmentCommand("CAMERA", "DIRECTION", literal));
			
//hides the crank that is driving the mechanism
literal = new FakeExpressionLiteral("NONE");
ch.addCommand(new PropertyAssignmentCommand("J1", "OBJ_FILE", literal));
ch.addCommand(new PropertyAssignmentCommand("J2", "OBJ_FILE", literal));
ch.addCommand(new PropertyAssignmentCommand("J3", "OBJ_FILE", literal));
```

<img src='http://impsim.googlecode.com/svn/wiki/images/Peaucellier Linkage.png' />

## Peaucellier Linkage in IMP ##
```

ZPIN  O FRAME L    	-58,0,0		10,0,0		0,-188,0;

ZPIN  B L S             0,18,0    	10,0,0          -21.5,0,0;
ZPIN  Q S R             15,0,0     	-25,0,0         -21,30,0;
ZPIN  D R A             0,-18,0         -30,30,0   	11.8,20,0;
ZPIN  V A FRAME         -58,0,0    	10,0,0     	10,0,0;
ZPIN  P M C             -15,0,0    	10,0,0   	-27.5,-10,0;
ZPIN  B2 M S 		0,18,0 		10,18,0 	10,18,0;
ZPIN  D2 C R 		0,-18,0 	10,-18,0 	10,-18,0;
ZPIN  Op FRAME T 	-38,0,0 	10,0,0 		10,0,0;
ZPIN  P2 M T 		-15,0,0 	10,0,0 		-15,100,0;

ZPIN  J1 FRAME L1 	-25,-15,0 	0,-15,0 	0,-15,0;
ZPIN  J2 L1 L2 		-16,-15,0 	0,-15,0 	0,-15,0;
ZPIN  J3 L2 T	 	-25,0,0 	0,0,0 		0,0,0;

#Sets the ground to the body "frame"
GROUND = FRAME;

#Sets the J1 to rotate 0.01 degrees per tick
J1.Theta = Ticks() * 0.01;

#Overrides the default camera settings
CAMERA[UP] = {0,1,0};
CAMERA[LOCATION] = {-25,0,110};
CAMERA[DIRECTION] = {0,0,-1};

#Defines object files for the joints
O[OBJ_FILE] = "models/peaucellier/model_O.obj";
B[OBJ_FILE] = "models/peaucellier/model_B.obj";
Q[OBJ_FILE] = "models/peaucellier/model_Q.obj";
D[OBJ_FILE] = "models/peaucellier/model_D.obj";
P[OBJ_FILE] = "models/peaucellier/model_P.obj";
P2[OBJ_FILE] = "models/peaucellier/model_P2.obj";
B2[OBJ_FILE] = "models/peaucellier/model_B2.obj";

#Hides the crank that is driving the mechanism
J1[OBJ_FILE] = "NONE";
J2[OBJ_FILE] = "NONE";
J3[OBJ_FILE] = "NONE";
```

<img src='http://impsim.googlecode.com/svn/wiki/images/Peaucellier Linkage.png' />