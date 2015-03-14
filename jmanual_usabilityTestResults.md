# Usability Test Results #
The following test results were gathered after running the usability tests detailed on [this page](jmanual_PluginTestPlan.md). The targeted users for the usability test were those who had some experience in programming, using computers, IMP, or other mechanics related software. Below is a description of the testing process for each user and details about the results of each test that was run with them.


# User 1 #

User one is a ME student at MSOE. They had some experience using a computer and mechanics related software other than IMP, and also had used programming languages before but wasn't and expert.

### Test 1 ###
**Total Time:** 4m 51s

**Errors:**

  * User tried to load the file without first creating a project, which did not result in the model loading.
  * After Creating a project, the user tried using file open which did not work.

**Help Asked:**

  * After trying to load a file without creating a project, the user asked why it was not working. I explained that you needed to first  create an IMP project.
  * The user asked how to create an IMP project. I showed them how to create one using the file menu.
**Rating:** The user said that they would rate the difficulty of this task an 8 or 9 to complete if they dud not have help.

**Comments:**
  * Specify that there is an error when a file is attempted to be loaded outside of a project.
  * Add a help file or feature.
### Test 2 ###
**Total Time:** 6s

**Errors:**
  * No errors.
**Help Asked:**
  * No help ask for.
**Rating:** The user said that this was very easy and rated it a 1 for difficulty.

**Comments:**
  * Overall very easy.
### Test 3 ###
**Total Time:** 40s

**Errors:**
  * The user thought the refresh button was used to rotate the model.
**Help Asked:**
  * The user asked what the controls were to orientate the model. I explained the keys used to move the camera and model
**Rating:** The user said that this task was easy and rated it a 3 for difficulty.

**Comments:**
  * The user said that they would prefer to use the arrow keys instead of the WASD keys for moving the camera.
### Test 4 ###
**Total Time:** 17s

**Errors:**
  * None.
**Help Asked:**
  * none.
**Rating:** The user said that this task was easy because they had learned to do this as part of an earlier test. they rated it a 1 for difficulty.

**Comments:**
  * No Comments or suggestions.
### Test 5 ###
**Total Time:** 8m 54s

**Errors:**
  * The user tried to name the joints starting with numbers and as a result an error was thrown.
  * The user tried to run the model after creating the bodies and joints without adding the ground statement or theta statements.
  * The user tried to create a new file, but when the dialog to create a new file opened the container field was blank and they attempted to create a file and leave it blank. They later said that they did not know that the container field was really the project name.
  * The user tried to add bodies but the file they were working on was not selected in the drop down menu and so the bodies and joints were being added to the last open file.
**Help Asked:**
  * The user asked where to start with creating the model fairly soon into the test after they had created the model. It was then suggested to create the bodies of the model by pressing the bodies button.
**Rating:** The user said that they would rate the difficulty of this task a 7.

**Comments:**
  * The error message with the parser exception was not descriptive and the user felt that it was not obvious what was wrong from reading the error message.
  * Old data was persisting on the screen from previous models.
  * When a new file is created, it would make sense to update the drop down menu so that has the new file selected so new bodies being created are added to the new file.
  * There should be a way to add the ground and other statements with the buttons in the GUI.
### Test 6 ###
**Total Time:** 1m 34s

**Errors:**
  * The user tried to run the model after entering all the test, but the file wasn't saved and so nothing was showing. I then told him to save the file fist before running.
**Help Asked:**
  * None asked.
**Rating:** The user said that they would rate the difficulty of this task a 2.

**Comments:**
  * Overall easy.
  * It would make sense for the run and refresh model to save the file first before running.


# User 2 #
User 2 is an SE student at MSOE. They were an expert with programming languages and computers, and a have some experience with IMP but not with the plugin.

### Test 1 ###
**Total Time:** 2m 41s

**Errors:**
  * The user tried to open the IMP model without creating a project first.
  * Tried opening the file with using file open which did not work.
  * Tried dragging file into project explorer out side a project.
**Help Asked:**
  * After running into the errors being caused by not having a project created it was asked what to do. The suggestion was given to create a new project first.
  * Help was given after file open was not working. I told the user to open the file by dragging the file into the project.
**Rating:** The user said that they would rate the difficulty of this task a 7.

**Comments:**
  * A warning that you cant add a file without a project would be helpful.
  * It would also be helpful if a default project was made for a file  being opened without a project.
  * There should be other ways to open a file besides dragging it into the project explorer, like using file open.

### Test 2 ###
**Total Time:** 7s

**Errors:**
  * Clicked the tick button at first instead of run.
**Help Asked:**
  * None asked.
**Rating:** The user said that they would rate the difficulty of this task a 1.

**Comments:**
  * Tool tips for the buttons should be added.
### Test 3 ###
**Total Time:** 7s

**Errors:**
  * None.
**Help Asked:**
  * None asked.
**Rating:** The user said that they would rate the difficulty of this task a 1.

**Comments:**
  * None.
### Test 4 ###
**Total Time:** 6s

**Errors:**
  * None.
**Help Asked:**
  * None asked.
**Rating:** The user said that they would rate the difficulty of this task a 1.

**Comments:**
  * None.
### Test 5 ###
**Total Time:** The test ran for 4m before the user gave up.

**Errors:**
  * The user was unable to add bodies after adding 2. There was an error that was causing the button to add the body to be non interact-able. the cause of this error was unknown.
  * The user tried to add bodies and joints without having the file they wanted to work being selected in the drop down menu, so the bodies and joints were being added to the previous file.
**Help Asked:**
  * The user asked why they could not add bodies. I was not able to answer the question.
**Rating:** The user said that they would rate the difficulty of this task a 10. There were errors that were preventing the task from being completed.

**Comments:**
  * Delete doesn't seem to work. When delete is pressed after right clicking on a joint the joints do not disappear.
  * When a new file is created it should automatically switch the file in the drop down menu to the new file.
  * The bodies and joints area should be so large initially. There is a lot of unused blank space.
  * When the joint and bodies area is re-sized so that the contents do not entirely fin on the screen, there is no way so scroll the area to make the hidden components visible.
  * It would be easier if when right clicking in the project explorer the option to create a new imp file appeared under the Right click -> new -> new Imp file
### Test 6 ###
**Total Time:** 16s

**Errors:**
  * None.
**Help Asked:**
  * None asked.
**Rating:** The user said that they would rate the difficulty of this task a 2.

**Comments:**
  * The model you are working with should show by default instead of having to select it in the drop down menu. For example, If the user is typing in the text editor for model 6, the drop down should switch to model 6 instead of staying on the last file.

# User 3 #
User 3 is an ME student at MSOE.  They had experience with some light coding and a well versed knowledge in Mechanical systems.  They have used programs like Solidworks and Ansys before.

### Test 1 ###
**Total Time:** 24s

**Errors:**
  * None.
**Help Asked:**
  * None Asked.
**Rating:** The user would rate this at a 2 for easy.

**Comments:**
  * None as he got it intuitively to drag and drop the file.

### Test 2 ###
**Total Time:** 9s

**Errors:**
  * None
**Help Asked:**
  * None asked
**Rating:** The user would rate this a 1 for easy.

**Comments:**
  * Suggested Hover messages for the buttons or Tool tips

### Test 3 ###
**Total Time:** 1m36s

**Errors:**
  * Trial and Error with the buttons so a lot
**Help Asked:**
  * Asked what buttons did what.
**Rating:** The user would rate this a 7 for slightly difficult.

**Comments:**
  * Suggested a key legend to help out the user.
  * Suggested a single button click that would change the mouse into a rotate camera mode.

### Test 4 ###
**Total Time:** 8s

**Errors:**
  * None
**Help Asked:**
  * None asked
**Rating:** The user would rate this a 2 for easy.

**Comments:**
  * Found it very easy

### Test 5 ###
**Total Time:** 9m46s

**Errors:**
  * Quite a few as we ran into a bunch of bugs
**Help Asked:**
  * Ton
**Rating:** The user would rate this a 2 for easy if it worked.

**Comments:**
  * Fix the bugs
  * Also check for a pivot point in the core and suggested the equation S+L < P+Q
  * Also said we might be a little over excessive on decimals.

### Test 6 ###
**Total Time:**

**Errors:**
  * None
**Help Asked:**
  * None asked
**Rating:** Didn't Try

**Comments:**