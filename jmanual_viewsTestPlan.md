# Structures Test Plan #

### Package: imp.Views ###
### Revision History ###


&lt;hr&gt;


<table border='1'>
<tbody><tr>
<th> Date:<br>
</th><td>  09/29/2012<br>
</td></tr>
<tr>
<th> Version:<br>
</th><td> 1<br>
</td></tr>
<tr>
<th> Who:<br>
</th><td> Jake Kuszewski<br>
</td></tr>
<tr>
<th> Comments:<br>
</th><td> Test plan for the views package within the plugin.<br>
</td></tr></tbody></table>


&lt;/hr&gt;



### Introduction ###
This document contains an outlined test plan for the views package.
#### Purpose ####
To verify that the objects function correctly.

### Test Strategy ###
#### Test Plans ####
##### Test 1.0: ObjectComposite.java #####


&lt;hr&gt;


<table border='1'>
<tbody><tr>
<th> Objective:<br>
</th><td> Test class for a an ObjectComposite.<br>
</td>
<tr>
<th> Type of Test:<br>
</th><td> Unit Test<br>
</td></tr>
<tr>
<th> Testing Methodology:<br>
</th><td>
</td></tr>
<tr>
<th> Procedure:<br>
</th><td>
<li> Test Constructor </li>
<ul>
<li> Good data </li>
<li> Null Data </li>
</ul>
<li> Test updateTreeLayout</li>
<ul>
<li> test true</li>
<li> test false</li>
</ul>
<li> Test updateCurrentTreeItem</li>
<ul>
<li> Good String</li>
<li> Bad String</li>
</ul>
<li> Test addJoint</li>
<li> Test addBody</li>
<li> Test setAddJointsEnabled</li>
<ul>
<li> true</li>
<li> false</li>
</ul>
<li> Test clear</li>
</td></tr>
<tr>
<th> Preconditions:<br>
</th><td> No compilation errors.<br>
</td></tr>
<tr>
<th> Expected Results:<br>
</th><td> Running the test should result in no failures or errors.<br>
</td></tr>