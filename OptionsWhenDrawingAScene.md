When drawing a scene in imp there are a few different options which allow you to configure how an object is drawn. These options are accessed mostly in the Camera class which holds the shaders that are used to draw the scene. Currently there is support for drawing 3D objects, Lighting, Textures, and Materials. If you are extending the GLModel class to create a custom object you can use these features to define how the object should be drawn.


## General ##
There are four layout locations within the shader that can be used for different things:
  * Location 0 - This buffer holds the position of each vertex.
  * Location 1 - This buffer holds the color as a vec4 for each vertex.
  * Location 2 - This buffer holds the normal of each vertex. This is used for lighting calculations.
  * Location 3 - This buffer holds UV coordinates which are used for texturing an object.

## 3D Objects ##
When drawing 3D objects there are a few steps that must be taken in order to be drawn properly:

  * Drawing 3D must be enabled. This is done by calling Camera.draw3D(true).
  * The 3D objects orientation can be set using Camera.setOrientationMatrix(Mat4 matrix). This will orientate the objects vertices by multiplying them with this orientation matrix.
  * Enable using the orientation matrix by calling Camera.useOrientationMatrix(false).
  * Lighting must be present in the scene which is detailed in the section below. Non 3D models do not need lighting enabled.

## Lighting ##
Lighting can also be added to the scene. This must be done to display 3D models properly but is unnecessary for drawing non 3D models. To add Lighting to the scene the following must be done:
  * Set the number of lights that will be used. Currently you can have up to 13 lights in the scene. To set the number of lights being used get the uniform handle to this attribute by using Camera.getNumberOfLightsUniform(). Then use this uniform to set a float value defining the number of lights being used to the current glContext.
  * Pass in data representing the lights being used. To do this you can get the uniform in the shader for this value with Camera.getLightsUniform(). The lights are represented by an array of floats with size 16\*n where n is the number of lights being used. Each individual light has 16 floats, and each consecutive 4 floats represents a vector 4. The format for defining lights is {position, ambient, specular, diffuse}. The final array that is bound to the given uniform should contain all the lights arrays concatenated together.


## Textures ##
Objects can also be drawn using textures. To draw an object using textures do the following:
  * Enable drawing with textures by calling drawTextured(true)
  * Bind the texture you want to use as you normally would to the current glContext using texture.bind(gl);
  * Bind the UV coordinates for the model to location 3.


## Materials ##
You can also draw objects using materials when drawing 3D is enabled. This is how you can make a surface look shiny or dull and reflect different colors. If no materials are defined a default material will be used when drawing the scene. To draw with a certain material you can bind it to the struct uniform called "materialUniform" in the shader. Only one material can be bound to the shader at a time. The struct takes the form of the following GLSL code:
```
struct materialStruct{//custom structure defining materials
        vec4 ambient;
	vec4 diffuse;
	vec4 emissive;
        vec4 specular;
	float shininess;
};
```

The following code shows how you would bind a material to this uniform struct:

```
int cameraShaderProgram = Shader.getShaderProgram(Camera.CAMERA_SHADER_NAME);
float[] diffuseColor = {1.0f,1.0f,1.0f,1.0f};//diffuse color
float[] specularColor = {0.5f,0.5f,0.5f,1.0f};//specular color 
float[] ambientColor = {0.2f,0.2f,0.2f,1.0f};//ambient color
float shininess = .5f;//the shinyness. the higher the value the more concentrated the light is reflected off of it

int materialDiffuse = gl.glGetUniformLocation(cameraShaderProgram, "materialUniform.diffuse");
int materialSpecular = gl.glGetUniformLocation(cameraShaderProgram, "materialUniform.specular");
int materialAmbient = gl.glGetUniformLocation(cameraShaderProgram, "materialUniform.ambient");
int materialShininess = gl.glGetUniformLocation(cameraShaderProgram, "materialUniform.shininess");

gl.glUniform4fv(materialDiffuse,1,diffuseColor,0);
gl.glUniform4fv(materialSpecular,1,specularColor,0);
gl.glUniform4fv(materialEmissive,1,emissiveColor,0);
gl.glUniform4fv(materialAmbient,1,ambientColor,0);
gl.glUniform1f(materialShininess,shininess);
```

The GLModel has a helpful method already implemented that will automaticaly bind a Material to the shader, so If you want to draw an object using defined materials then It may be helpful to extend this class.