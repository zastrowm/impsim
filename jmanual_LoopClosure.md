## Loop Closure ##

Where to start with this beast?  This part of the code is the result of almost 3 full cycles of research and development.  I have gone through and commented the code so there are almost more comments than lines of code.

I will try and explain the concept of loop closure without getting too deep into the details(which can be learned by looking into the code).

The basic idea of loop closure is to modify the magnitude of the different joint variables so that the transformation through the model is still equal to the identity matrix.  The LoopCloser class takes a list of LoopVariable's which have the following properties:
```
   public LoopVariable(String joint, JVAR jvar, double magnitude) {
		jvarType = jvar;
		this.joint = joint;
		this.magnitude = magnitude;
	}
```

These variables tell the model which joints are driving the movement, and how much is being moved.  The LoopCloser class then solves how the other joints change by incrementally solving for the changes in the magnitudes.  Each time the algorithm runs, the values get closer to their actual values(most times this is within 1-5 iterations).  The algorithm in its entirety involves a lot of complex matrix math(A lot of which can be found in pictures under the meeting notes wiki page).

The basic flow is as follows:
  * Save current values in case the loop cannot close
  * Solve for the Transformation-Matrices to each joint
  * Use the Transformation-Matrices to calculate the Delta-Phi Matrices
  * Use the Delta-Phi Matrices to create the Jacobian-Matrix which is a systems of equations to solve all of the unknown variables
  * Solve the Matrix
  * Check the precision and perform another iteration if necessary
  * Save the new values, or revert to the old values if the loop could not close

I know a lot of this will be unclear, and hopefully the algorithm will not need to be modified again.  I did not base this code on its C equivilent(although if you want to delve into that code it will probably be similar, although it is undocumented).  All of this code was developed from scratch using the concepts of loop closure as researched during the cycles and taught by Dr. Hornick.