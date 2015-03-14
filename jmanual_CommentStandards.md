# Javadoc #
**Add the optimize tag in the Preferences page**

<img src='http://impsim.googlecode.com/svn/wiki/images/Optimize_tag.png' height='400px' />

## Example ##

```

/**
 * Description of function performed.
 *
 * @param  variable Description text.
 * @return Description text.
 * @author Name of author
 * [@author Additional author]
 * [@original path/c-function-name.c]
 */


 //TODO: concise description of task with method name
 //OPTIMIZE: method name, outline algorithm to use if possible
 //FIXME: method name, what needs to be done

```

## Ported IMP Functions ##
  * Standard Javadoc
  * Description of function
  * Description of parameters
  * Description of return variable
  * Author
  * @original path/c-function-name.c

## New Functions ##
  * Standard Javadoc
  * Description of function
  * Description of parameters
  * Description of return variable
  * Author

# Regular Comments #

## All functions ##
  * Any function having more than 5 lines should probably have a comment  in it somewhere.
  * Add comments to denote sections in the code (eg. Error checking, variable initalization, traversing a datastructure, etc.) (ie. Anywhere there is a block of 3 or more lines of code that are closely related.)
  * Don't add unnecessary comments that clutter the code, keep comments concise
  * Comments should explain WHY certain things are done, not just WHAT is done

## Variables ##
  * Label all class variables with comments telling what each variable is used for.
  * For any package scope variables specify that this is intentional with /**package**/ in front e.g.
```
/* package */ int randomValue;
```