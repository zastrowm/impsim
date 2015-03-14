## Formatting Standards ##
  * Whitespace (empty lines) should be used to break up code sections.
  * Keep starting curly bracket on the same line as the 'if' and 'else' statements.
  * The corresponding 'else' for a conditional should be on the same line as the closing curly bracket of the conditional, separated by a space.
  * User defined code folding is enabled through an Eclipse plugin.  The file is in the tools repository.  Simply put the file com.cb.eclipse.folding\_1.0.6.jar in your Eclipse->Plugins folder.  After restarting Eclipse, go to Window->Preferences->Java->Editor->Folding and enable folding on user defined regions.

<img src='http://impsim.googlecode.com/svn/wiki/images/Preferences.png' height='400px' />

```
//[start] description of folded section
public String method(String param1, String param2) {
    String output = "";

    if (param1.equals(param2)) {
        output = "equal";
    } else {
        output = "not equal";
    }

    return output;
}
//[end]
```

Formatting can be done automatically via the IDE (see steps 6/7):

[IDE and Environment Setup](jmanual_IDEandEnvironmentSetup.md)