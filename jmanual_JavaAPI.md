# Java API #
IMP comes with a full API for programming and simulating mechanical links in Java without the need of a plugin or knowing the IMP language.  This document explains the supported features so you can get started on running your own models.

## Imp Engine ##
Access to the API is primary done through the use of an object called the Command Holder.  The Command Holder stores all the commands you pass it in a queue and then will run these commands for making a model when state and loop closure is found.  It also allows you to query the state of the system through getters.

Use this following code template to instantiate and run a mechanical system:
```
       Model model = new Model();
		
       ch = null;
       try {
              ch = new CommandHolder(model);
       } catch (FunctionAlreadyExists e) {
	      //handle exception
       }

       try{
              //Add your commands here...
       } catch (SelfLoopException e){
              //handle exception
       }

       try{
              ch.compile();
              ch.verify();
              ch.runIndefinitely(10);
       } catch (LoopException e){
              //handle exception
       } catch (BodyNotFoundException e){
              //handle exception
       } catch (IMPException e){
              //handle exception
       }
```

### Imp Commands ###

Commands are what make up a model as they tell how to build a model and how to run it.  Each supported joint type implements command and can be added to the command holder.

#### Example ####
```
ch.addCommand(<E extends Command>);
```

## Joint Commands ##
These are the joints handled by the IMP API.  For more information on the joints please consult the Imp Manual [IMP Java Manual](jmanual_ImpIntro.md)

### Revolute ###
[JManual](jmanual_jointRevolute.md)

[Revolute Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/RevoluteCommand.html)
```
RevoluteCommand r = new RevoluteCommand(String jointName, String bodyNameBefore, String bodyNameAfter, Point origin, Point commonAxis,  Point bodyAxisFirst, Point bodyAxisSecond);
```

#### XPIN ####
[JManual](jmanual_jointXPin.md)

[XPIN Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/RevoluteCommand.html)
```
RevoluteCommand r = RevoluteCommand.CreateXPin(String jointName, String bodyNameBefore, String bodyNameAfter, Point commonAxis, Point bodyAxisFirst, Point bodyAxisSecond);
```

#### YPIN ####
[JManual](jmanual_jointYPin.md)

[YPIN Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/RevoluteCommand.html)
```
RevoluteCommand r = RevoluteCommand.CreateYPin(String jointName, String bodyNameBefore, String bodyNameAfter, Point commonAxis, Point bodyAxisFirst, Point bodyAxisSecond);
```

#### ZPIN ####
[JManual](jmanual_jointZPin.md)

[ZPIN Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/RevoluteCommand.html)
```
RevoluteCommand r = RevoluteCommand.CreateZPin(String jointName, String bodyNameBefore, String bodyNameAfter, Point commonAxis, Point bodyAxisFirst, Point bodyAxisSecond);
```

### Prism ###
[JManual](jmanual_jointPrism.md)

[Prism Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/PrismCommand.html)
```
PrismCommand p = new PrismCommand(String jointName, String bodyNameBefore, String bodyNameAfter, Point origin, Point commonAxis, Point halfPlane);
```

#### XSlide ####
[JManual](jmanual_jointXSlide.md)
[XSlide Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/PrismCommand.html)
```
PrismCommand p = PrismCommand.CreateXSlide(String jointName, String bodyNameBefore, String bodyNameAfter, Point commonAxis, Point bodyAxisFirst, Point bodyAxisSecond);
```

#### YSlide ####
[JManual](jmanual_jointYSlide.md)

[YSlide Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/PrismCommand.html)
```
PrismCommand p = PrismCommand.CreateYSlide(String jointName, String bodyNameBefore, String bodyNameAfter, Point commonAxis, Point bodyAxisFirst, Point bodyAxisSecond);
```

#### ZSlide ####
[JManual](jmanual_jointZSlide.md)

[ZSlide Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/joints/PrismCommand.html)
```
PrismCommand p = PrismCommand.CreateZSlide(String jointName, String bodyNameBefore, String bodyNameAfter, Point commonAxis, Point bodyAxisFirst, Point bodyAxisSecond);
```

### Expression Commands ###
There are points when making a model that you'll want to specify an expression for a joint.  To do this you must make use of the JointExpressionCommand which will apply the expression to the specified joint.  Expressions are formed using a FakeExpression array which is then passed to a Function object.  An example is below:
```
FakeExpression[] expression = new FakeExpression[2];
expression[0] = new Function("", "TICKS");
expression[1] = new FakeExpressionLiteral(0.02);
JointExpressionCommand j = new JointExpressionCommand("J1", JVAR.THETA, new Function("", "*", expression));
```
This particular code fragment will define the joint "J1" to set its Theta value to the value of 0.02\*ticks(), where ticks() is a method referring to the number of ticks performed so far. Essentially it allows you to define expressions as a function of time.

[Fake Expression Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/expressions/FakeExpression.html)

[Fake Expression Literal Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/expressions/FakeExpressionLiteral.html)

[Function Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/expressions/Function.html)

[Joint Expression Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/JointExpressionCommand.html)


### Ground ###
It is a requirement of the IMP engine that a body in each linkage be defined as the "Ground".  The command would be:
```
GroundCommand g = new GroundCommand("FRAME");
```

FRAME is the body that would be set to ground.

[Ground Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/GroundCommand.html)

### Property Assignment ###
To assign properties to a joint, you must use a PropertyAssignmentCommand.  This command makes use of FakeExpressions as a way of passing values to it, but in most cases you will only need to use FakeExpressionLiterals.  Here is an example:
```
FakeExpression expression = new FakeExpressionLiteral("BEFORE");
PropertyAssignmentCommand p = new PropertyAssignmentCommand("J1", "SHOW_AXIS", expression);
```

For more information on properties, see: [Supported Properties](jmanual_Properties.md)


[Fake Expression Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/expressions/FakeExpression.html)

[Property Assignment Command Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/PropertyAssignmentCommand.html)

### Command Holder Methods ###
These are methods that are called to run a model or change something in the command holder.

[Command Holder Java Doc](http://impsim.googlecode.com/svn/java_doc/imp/core/commands/encapsulation/CommandHolder.html)

#### Verify Command ####
This checks the model to make sure loop closure is achieved and that all bodies and joints are linked up.
```
ch.verify();
```
This method is used if you want an exception thrown to your application when it fails.  Useful for doing your own error checking.
```
ch.verifyOrFail();
```

#### Run Methods ####
These commands are called to run or simulate the model with the physics engine.

This first one makes the model run indefinitely or until a pause or stop is called on the command holder.
```
ch.runindefinitely(int timeStep);
```
timeStep is how much time you want between each tick of the model.

This one runs the model for so many steps
```
ch.run(int timeStep, int maxSteps);
```
timeStep is how much time you want between each tick of the model and maxSteps is how many ticks of the model you want.

This method pauses the model.
```
ch.pause();
```

This method resumes the model from a paused state.
```
ch.resume();
```

This method resumes the model and runs it for only a number a of ticks before pausing the model again.
```
ch.resume(int timeStep, int numberOfTicks);
```
timeStep is how much time you want between each tick of the model and numberOfTicks is how many ticks you want the model to run.

#### Clear/Removal/Terminate Methods ####

This method removes a command from the command holder.
```
ch.removeCommand(Command cmd);
```

This method clears the Model to a null state.
```
ch.clearModel();
```

This method terminates the Thread the model is running on.  Useful if you get in a stuck loop.
```
ch.terminateThread();
```


#### Add Methods ####

This method adds a list of commands to the command holder.
```
ch.addCommands(List<Command> cmds);
```

This method adds a command to the command holder.
```
ch.addCommand(Command cmd);
```

### Information Getters ###

#### Model Getter ####
Returns an object that contains the model.
```
ch.getModel();
```

#### Loop Getter ####
Returns a list of loops that the model contains.
```
ch.getLoops();
```

#### RunningState Getter ####
Returns the current state of the command holder.
```
ch.getCurrentRunningState();
```

#### Command Getters ####
```
ch.getCommands();
```
Returns the commands in the command holder.

```
ch.getExecutedCommands();
```
Returns the commands that have already been executed by the command holder.

#### Property Manager Getter ####
Returns an object containing the property manager.
```
ch.getPropertyManager();
```

#### Ticks Getter ####
Returns the number of ticks the model has run for.
```
ch.getTicks();
```

## Parsing from IMP Files ##
If you wish to parse the API commands from a properly formatted IMP file, use the SimpleParser object like so:
```
ParserData data = SimpleParser.parseFile(File f);
ch.addCommands(data.commands);
```

## Examples ##
For example models done with the API please consult the [Examples](jmanual_APIExamples.md) page.