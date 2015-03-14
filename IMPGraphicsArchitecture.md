# IMP Graphics Architecture #

The IMP Graphics Architecture is composed of six classes: AbstractDataSource.java, AbstractGLObject.java, AbstractGraphics.java, AbstractModelView.java, Camera.java, and Shader.java. They compose the framework needed to maintain, calculate, and project three dimensional objects onto the screen's two dimensional plane. This document will explain the purpose of each class, how the class fits within the architecture, and suggested methods of extending the abstract objects.

This image shows how the graphics architecture is structured, and below each class's purpose is explained.

<img src='http://impsim.googlecode.com/svn/wiki/images/Graphics Architecture.png' />
## AbstractGraphics ##
All OpenGL programs require that a class implement the GLEventListener interface. This interface is what the GLCanvas will communicate with to receive graphical information. The AbstractGraphics class is responsible for the proper set up of the virtual 3D environment from which the user will view their models. This set up includes lighting, camera, culling, shader, and direction initialization. It also maintains a single AbstractDataSource object which it uses within its display() method to draw objects from the AbstractDataSource.

The world is drawn in frames (60 frames per second by default). During each update tick, all objects in the data source have their update method called. The update method passes information to each object which they use to modify their position, rotation, orientation, scale, etc. After this time, each object that has been changed has its information sent to the GPU to reflect the changes. Then the draw method is called on each object.

The following pseudocode shows the workflow of the display method:

```
public final void display(GLAutoDrawable g) {
	disposeOld(gl);

	if(ds != null){ //make sure there is something to get data from

				
		updateObjects();

		List<AbstractGLObject> objects = getGLObjects();

		clearColor();

		//have camera calculate its projection matrix and bind its uniforms
		calculateProjectionMatrix();

		//bind camera shader program
		gl.glUseProgram(Shader.getShaderProgram(Camera.CAMERA_SHADER_NAME));		
				
		//for each object
		for (int i = 0; i < objects.size(); i++){
			//draw the object	
			objects.get(i).draw(gl);
		}

		//unbind shader program
		gl.glUseProgram(0);
	}
}
```
## AbstractGLObject ##
The AbstractGLObject exists to guarantee all objects stored within the AbstractDataSource will have a method of initializing, drawing, updating, and disposing of themselves. It is a low functionality class acting mostly as an initerface with a required constructor to specify the object name. Each class that extends this class must define how that class is to be drawn, and each instance must have a unique name which is strictly enforced.

When drawing, the object must at a minimum perform the following task:
```
public void draw(GL3 gl){
	bind the array buffer
	set up vertex attribute pointers
	draw arrays
	disable vertex attribute pointers
	unbind the array buffer
}
```

This class also contains an init method. This is where the GLObject's data is set up and bound to the GPU. The flowing example shows a concrete implementation of this class that is binding vertex, color, and normal data to the GPU:

```
@Override
public void initialize(GL3 gl) {
	//copy loopData information into data
	float[] data = new float[vertexData.length+colorData.length+normalData.length+rawUVData.length];
	for (int i = 0; i < vertexData.length; i++){
		data[i] = vertexData[i];
	}
	//copy colorData information into data
	for (int i = 0; i < colorData.length; i++){
		data[vertexData.length + i] = colorData[i];
	}
	//copy normalData information into data
	for (int i = 0; i < normalData.length; i++){
		data[vertexData.length+colorData.length + i] = normalData[i];
	}

	//copy uvData information into data
	for (int i = 0; i < rawUVData.length; i++){
		data[vertexData.length+colorData.length+normalData.length + i] = rawUVData[i];
	}

	FloatBuffer vertexPositions = FloatBuffer.wrap(data);
	identifier = IntBuffer.allocate(4);
	//generate the identifier
	gl.glGenBuffers(3, identifier);

	//bind the object
	gl.glBindBuffer(GL.GL_ARRAY_BUFFER, identifier.get(1));

	//copy data to the GPU
	gl.glBufferData(GL.GL_ARRAY_BUFFER, vertexPositions.capacity() * SIZE_OF_FLOAT, vertexPositions, GL3.GL_STREAM_DRAW);

	//unbind the object
	gl.glBindBuffer(GL.GL_ARRAY_BUFFER, 0);
}
```
## AbstractDataSource ##
This class is responsible for holding a list of all AbstractGLObjects to be drawn in a scene. It in essence is both a HashMap and an ArrayList to allow for constant time retrieval to be available via iteration and key-value pairs. A single instance of the AbstractDataSource is stored within the AbstractGraphics class, and the instance can be switched via the AbstractGraphics.setGraphicsDataSource() method. This method can be called at any time from within an OpenGL interface method without repercussions, and it allows scenes to be easily transferable.

An example of how to use the data source:
```
public void doStuff(){

	GLModel model = new GLModel("Model1");
	ModelDataSource ds = new ModelDataSource();

	ds.putObject(model); //uses the model's name as the key

	GLModel model2 = ds.getObject("Model1");

	//model2 == model1

}
```
## AbstractModelView ##
Default implementations of engine and input initialization is available through the AbstractModelView class. Extending this class allows for all graphics engine method calls to be abstracted away from the developer, and classes are override-able as necessary. The AbstractModelView is an extension of the AbstractGraphics class and it implements the MouseWheelListener, MouseMotionListener, MouseListener, and KeyListener interfaces. The default controls of the resulting Frame are as follows:

  * W - Forward
  * S - Backward
  * A - Rotate Left
  * D - Rotate Right
  * R - Up
  * F - Down
  * Z - Roll Left
  * X - Roll Right
  * Mouse Drag - Rotate camera
## Camera ##
The Camera class represents the viewpoint of the "eyes" looking in to the virtual scene. Any movement controls from the AbstractModelView modify the Camera position and rotation directly. This class holds the Shader code needed to properly display the world and is instantiated during the initialization process of the AbstractGraphics class. It contains all the methods needed to position or move the camera. Any movement function is velocity based in units per second, while the positioning functions are absolute.


### Controlling the camera ###

To move the camera use the moveDirection methods and pass in the desired speed in units per second. Contained within the camera is a thread that will continuously move the camera in small increments to make it appear as if it is being smoothly moved. To stop moving in a certain direction use the stopDirection methods. The following example of code shows how to move the camera to the right for 100 ms.
```
camera.moveRight(1f);//start moving the camera in its right direction at 1 speed
Thread.sleep(100);//wait for 100 ms before telling the camera to stop moving in the right direction
camera.stopRight();//stop moving right.
```
The moveDirection methods can also be used simultaneously in different directions. For example, if you wanted the camera to move to the right at 1 speed and forward at .5 speed for 100 ms you could do the following:

```
camera.moveRight(1f);//start moving the camera in its right direction at 1 speed
camera.moveForward(.5);//move forward to to make it move diagonaly
Thread.sleep(100);//wait for 100 ms before telling the camera to stop moving in the right direction
camera.stopRight();//stop moving right.
camera.stopForward();//stop moving forward.
```

To rotate the camera in place to look at a certain direction you can use the rotateAboutArbitraryAxis(Vec3 axis, float degrees) method which will rotate the camera around the passed in vector for the given degrees. You can also orbit the camera around a point in the world by using the orbit(Vec3 point, float radians, Vec3 axis) method.

### Accessing Shaders ###

This class also contains the handles to any uniforms used within the vertex and fragment shaders to specify how to draw each model. There are a few different features that a model can be drawn with which is documented [[when Drawing a Scene|here](Options.md)]. [[Creating 3D 4bar](Tutorial.md)]
## Shader ##
The Shader class contains several static methods for managing shader code and making shader programs available to the AbstractGraphics' display() method. Before a Graphics Library Shader Language (GLSL) program can be used, it must be compiled and saved using the compileShader() and createShaderProgram() methods. Whenever something is to be drawn to the screen, the proper shader program must be used. The Shader class stores all created programs, and they can be retrieved using the Shader program's name chosen at creation time.