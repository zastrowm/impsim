# 4-Bar with API Tutorial #

In this tutorial, you will learn how to model a 4-bar mechanism using the API and have that mechanism display on an OpenGL canvas. After configuring your build path, you will need to initialize the canvas, define a CommandHolder, and then assign the DataSource for the graphics to render from.

The full source code for the tutorial can be found here: [Source](http://code.google.com/p/impsim/source/browse/impsim-java/trunk/Examples/APITest.java)

## Configuring the Build Path ##
Create a new Java project in eclipse, then obtain the required libraries found below:
  * [IMP](http://code.google.com/p/impsim/downloads/detail?name=Imp_1.0.jar)
  * [JOGL](http://jogamp.org/deployment/jogamp-current/archive/) (choose jogamp all platforms, this link valid as of 11/14/2012)

In your eclipse project, add IMP, Jogl, and Gluegen to your project build path.
  1. Right click your project
  1. Go to Build Path -> Configure Build Path
  1. Click "Add External  JARs" in the Libraries tab
  1. Select IMP\_1.0.jar, jogl-all.jar, and gluegen-rt.jar libraries

Note that for the Jogl and Gluegen libraries, you will also need to include the appropriate platform natives. There should be a total of five external jars on your build path including the IMP library after this step.

## Initializing the Canvas ##

The AbstractModelView class provided is the simplest method of initializing an OpenGL canvas to be used with IMP. Simply extend that class. You can then retrieve an OpenGL canvas with the getGLCanvas() method. GLCanvas is compatible with AWT, Swing, and SWT frames and can be embedded in any of these.

```
public class APITest extends AbstractModelView{

	/**
	 * Main method
	 */
	public static void main(String[] args) {
		APITest model = new APITest();
		model.init();
	}

	/**
	 * Basic initialization of the canvas
	 */
	public void init(){
		//initializes the GL canvas
		JFrame frame = new JFrame();
		frame.getContentPane().add(this.getGLCanvas());

		
		frame.setSize(600, 600);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setVisible(true);
	}
}
```

When init is called, a new frame with the OpenGL canvas will appear.

## Defining the Command Holder ##
Now that a window is displaying, we need to define our model. This is done using a CommandHolder object. Each command defines an attribute of the model, and when compiled the full model can be executed. The following code will generate a 4-bar mechanism.

```
/**
* Creates and executes a model using the IMP API
*/
public void runModel(){
	stopGraphics();

	//clear the reference to the current command holder
	CommandHolder ch = null;

	//add commands
	try {

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
		//end add commands


		ch.compile(); //compile the model
		ch.verifyOrFail(); //check for errors
		ch.runIndefinitely(10); //begin model execution

	} catch (SelfLoopException e){
		e.printStackTrace();
	} catch (FunctionAlreadyExists e) {
		e.printStackTrace();
	} catch (LoopException e) {
		e.printStackTrace();
	} catch (BodyNotFoundException e) {
		e.printStackTrace();
	} catch (IMPException e) {
		e.printStackTrace();
	}
}
```


## Assigning a Rendering Source ##
The IMP graphics framework uses a DataSource object to control what is drawn to the screen. The ModelDataSource is built specifically for rendering IMP models.

To assign a CommandHolder as the rendering source and begin rendering execution, simply add these lines to the end of runModel():
```
//Sets command holder to use when drawing to the canvas
ModelDataSource ds = new ModelDataSource(ch, this.getCamera());
setGraphicsDataSource(ds);
startGraphics();
```

Note that if model starts too quickly, an exception will be thrown until the graphics completes initialization, but it won't affect the state of the IMP system. This can be resolved by waiting for the graphics to initialize fully before calling runModel()

## More Information ##
For more information about the IMP API, please see [Java API](http://code.google.com/p/impsim/wiki/jmanual_JavaAPI)