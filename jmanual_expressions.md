# Introduction #

IMP expressions allow you to dynamically change the positions of joints and bodies as time goes on.  Expressions are core to the idea of transforming IMP from a modeling engine into a simulation engine.

# Expressions #
In order to reach a large audience, expressions in IMP are familiar to expressions in math and other programming languages, with one exception.  In most languages, a variable assignment results in a value being assigned to a variable.  However, in IMP, the expressions themselves are stored into variables.

For instance, in most programming languages the following expression:
```
X = Y + 3
```
would take the value of Y, add 3, and assign the result to X. Thus,
```
Y = 3
X = Y + 3
Y = 12
```
would result in X having a value of 6, and Y having a value of 12.

In IMP, when the above commands are executed, the expression "Y + 3" is stored into X, meaning that whenever the value of X is requested, the expression "Y + 3" is reevaluated.  Thus at the end of the following:
```
Y = 3
X = Y + 3
Y = 12
```
X would evaluate to 15, and Y would evaluate to 12.

## Operators ##
As has already been demonstrated, IMP understands the concept of operators.  In fact, IMP supports several operators, most of which are math based.  The operators supported, with their precedence, are as follows:

| **Precedence** |  **Symbol** |  **Name** |  **Description** |
|:---------------|:------------|:----------|:-----------------|
| 1 |  () |  Parenthesis |  Used for grouping |
| 1 |  {} |  Curly Brackets |  Used for specifying lists |
| 2 |  - |  Negation |  Used to negate a number/point |
| 3 |  ^ |  Exponent |  Raise one number to another |
| 4 |  |  Multiplication |  Multiply two numbers together |
| 4 |  / |  Division |  Divide two numbers together |
| 5 |  + |  Plus |  Add two numbers together |
| 5 |  - |  Minus |  Subtract two numbers |
| 6 |  & |  Concatenation |  Concatenate two values to a string |
| 7 |  , |  Comma |  Parameter Separation |
| 10 |  = |  Equals |  Assign a value to a variable |

## Functions ##
While many expressions can be represented only with operators, there are some situations in which it is more efficient or even necessary to express an expressions with higher level constructs.  For this purpose, IMP has functions.

Functions in IMP resemble functions in other languages.  Use the name of the function, a parenthesis, the parameters to give to the function, and a closing parenthesis.
```
X = MYFUNCTION(ARG1, 7)
```
For instance, the SIN of the absolute value of X can be found as follows:
```
Y = SIN( ABS(X) )
```
The list of functions that IMP supports by default can be found at [jmanual\_functionlist](jmanual_functionlist.md).

If multiple functions exist with the same name, use the namespace qualifier to distinguish between functions:

```
X1 = IMP~CORE~ABS(-Y)
X2 = YOUR~OWN~ABS(-Y)
```

## Data Types ##

While the most common type of data used in a physics engine is a single number, there are a couple of other data types supported to make the IMP engine more robust.

### Numbers ###
The most basic data type, the number, is also the most familiar to the world.  As such, it can be used in the same manner as in math:
```
X1 = 3.4323
X2 = 2
X3 = 234e3
X4 = -34e-1
```

### Points ###
Points are merely a set of 3 numbers, constructed with the POINT function.  Points are used to hold coordinates and to specify locations of data:
```
P1 = POINT(12.3, 43.2, 10.3)
P2 = POINT()
#POINT() without parameters is equivalent to:
P3 = POINT(0,0,0)
```

### Strings ###
Strings in IMP are used to relay information to the user as messages, or for specifying filenames:
```
SYSTEM[TITLE] = "Hello, World!"
```
In order to create dynamic messages, the concatenation operator can be used to "glue" data (even different data types) together:
```
SYSTEM[TITLE] = "Hello " & NAME & "!"
```

## Mathematical Expressions ##
The expression `“X + 7*(Y+3)”` will be represented as a tree of expressions, with each level of the tree having sub expressions.  In list format, the mathematical expression would be:

```
(ExpressionNumberAddition
	(ExpressionNumberVariable X)
	(ExpressionNumberMultiplication
		(ExpressionNumberLiteral 7)
		(ExpressionNumberAddition 
			(ExpressionNumberVariable Y)
			(ExpressionNumberLiteral 3)
		)
	)
)
```

The above tree also shows how the execution would occur in the java language. If this expression was named exampleExpression, then executiong exampleExpression.getValue() would take the following steps:
```
1.Retrieve the value of X
2.Retrieve the value of The Multiplication Expression
       a.Retrieve the value of the Literal Number (in this case, 7)
       b.Retrieve the value of the Addition Expression
              i.Retrieve the value of Y
              ii.Retrieve the value of the Literal Number (in this case 3)
              iii.Add together (i & ii)
              iv.return (iii)
       c.Multiply together (a & b)
       d.Return (c)
3.Add together (1 & 2)
4.Return (3)
```

Using this format for executing expressions allows the length of the expressions to be limited only to the memory available to the program, and simplifies the process of executing expressions because each expression only needs to understand the interface of sub expressions  and not how the individual expression operate.

## Value vs. Expression Assignment ##
When the IMP engine parses an expression, it shall construct a tree as described in the previous section.  When it assigns an expression to a variable, it shall assign the top level expression (exampleExpression) to be the value of the variable.  For value assignments, the expression shall be constructed as normal, but instead of assigning the top level expression to the variable, the engine shall construct a new expression literal with a value of the top level expression’s getValue() and assign this newly created expression to the variable.

In pseudo code, these two methods of assignment would be:
```
expression = parseAndReturnExpression(impcode)

#assigning an expression to a variable
variables.setValue(varname, expression)

#assigning a value to a variable
variables.setValue(varname, new ExpressionLiteral( expression.getValue() ) )
```


## Miscellaneous Notes ##
### Expression Methods ###
For each expression, the only the only method which may return a constant will be getValue().  Any other method should return either an expression or should be used for informational purposes only.  Thus, the ExpressionPoint getX() (which shall return the X coordinate of the point) should return an ExpressionNumber, even if the value is constant.  Thus to get the X coordinate of a point, one would use:

double x = pointExpression.getX().getValue();

### Function Expressions ###
Each function in the IMP language will take expressions as arguments and shall return expressions as results.  More information about functions will be included in a function specification at a later point in time.