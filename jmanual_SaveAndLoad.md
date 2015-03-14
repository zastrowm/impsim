## Purpose ##
This specification document details the requirements of saving and loading of IMP models.  IMP is based on commands and expressions.  Expressions are functions, variables, or literals.  Functions contain arguments that may themselves contain more expressions.

## Saving ##
When the model is saved, IMP will create an XML file based on the expressions and commands for the current model.  Due to a function’s ability to contain more expressions, the XML file may have highly embedded elements.  Save will be implemented via static methods in the Saving class:
```
	Saving.Save(Model currentModel, String fileName);
	Saving.Save(Model currentModel, PrintStream outputStream);
```

## Loading ##
Loading a .imp save file will create a model containing bodies and joints with the properties from the saved expressions and commands.  Loading will be done through the Loading class.
```
	Loading.Load(String fileName, PrintStream outputStream);
	Loading.Load(InputStream inputStream);
	Loading.Load(String fileName);
	Loading.Load(InputStream inputStream, PrintStream outputStream);
```
 
## Example ##
```
<model printStream="C:\impOutput.txt">
  <commands>
    <xpin type="data">
      <origin>4.5;2.2;4.3</origin>
      <axisBefore>2.4;2.134;6.2452</axisBefore>
      <axisAfter>123.5345;435;34.54</axisAfter>
      <jointName>Joint1Name</jointName>
    </xpin>
    <xpin type="definition">
      <bodyBefore>Body1Name</bodyBefore>
      <bodyAfter>Body2Name</bodyAfter>
      <jointName>Joint1Name</jointName>
    </xpin>
    <setvar var="varName">
      <function namespace="imp~math" name="funcName" returnType="double">
        <arg>
          <!-- If no arguments, may be empty -->
        </arg>
        <arg>
          <variable name="var2Name" type="string" />
        </arg>
        <arg>
          <literal type="double">2.53</literal>
        </arg>
      </function>
    </setvar>
    <cylinder type="definition">
      <bodyBefore>Body3Name</bodyBefore>
      <bodyAfter>Body4Name</bodyAfter>
      <jointName>Joint2Name</jointName>
    </cylinder>
    <cylinder type="data">
      <origin>4.5;2.2;4.3</origin>
      <commonAxis>2.4;2.134;6.2452</commonAxis>
      <halfPlane>123.5345;435;34.54</halfPlane>
      <jointName>Joint1Name</jointName>
    </cylinder>
    <setvar var="var3Name">
      <function namespace="imp~math" name="func2Name" returnType="double">
        <arg>
          <!-- If no arguments, may be empty -->
        </arg>
        <arg>
          <variable name="var4Name" type="string" />
        </arg>
        <arg>
          <literal type="double">2.53</literal>
        </arg>
        <arg>
          <function name="func3Name" returnType="int">
            <arg>
              <variable name="var5Name" type="double" />
            </arg>
          </function>
        </arg>
      </function>
    </setvar>
  </commands>
</model>
```