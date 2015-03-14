## Loop Finding ##


---

Kinematic loop finding is a method of finding the connections between joints and bodies in a system.  These relationships are used to determine how the system moves and how it is connected.
There are two different methods used in finding loops.  The first method uses matrices to simplify and find the possible loops in the model.  While the second method uses graph traversal and a queue of the joints(lines) and the bodies(nodes) in a graphical representation of the model.  The loop finding algorithm used in the loop.LoopFinder class implements a mixture of these two methods.

First the algorithm finds the possible loops using a graph traversal algorithm and then uses matrix math to make sure that the loops are passing through each joint in the same direction.  The full concept for this can be found in a couple hundred page thesis that Dr. Hornick currently has.  This is were a majority of the research came from for this implementation(in addition to looking at the old c code).

Notice that this code uses a named loop to break out of the outer loop from an inner loop:

```
columnLoop: for (int i = 0; i < nLoops; i++) {
    ...more code
    inner loop{
        break columnLoop;
    }
}
```

This is being used to handle early breaks and not loop unnecessarily which would occur if a flag was used instead.

I have comment the code for this very thoroughly but the thesis can also be referenced if needed.  This code is stable and should just work without any need to change.