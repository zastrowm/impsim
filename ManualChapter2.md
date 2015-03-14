# Chapter 2: The IMP Language #

## Table of Contents ##


The IMP (Integrated Mechanisms Program) language is a problem oriented language. It enables the user
to describe a mechanical system to IMP and to request certain types of analyses using terms which
are familiar to them. They are not required to be familiar with other computer programming languages
such as FORTRAN or C.

## Job Initiation ##
In order to use IMP on a particular computer system, the user must first gain access to the computer
itself, and then establish communication with the IMP system. In an interactive environment, a few
standard bits of information may be required to be typed on the keyboard or chosen with a mouse or
other pointing device. This information usually establishes the user's identification, accounting
information, etc., and calls IMP into the computer.

The format of these initial statements vary widely with the particular computer system being used,
whether an interactive or a background simulation is intended, and the policies of the particular
installation. No attempt is made here to explain them in detail. Additional information must be
obtained from the particular installation.

As an example, the current procedure at the author's installation for interactive use of IMP on a
Pentium computer system operating in a Novell network requires the user to log into a valid account,
and then to choose the title IMP from a particular menu.

## IMP Statements ##
The IMP-language program for simulating a particular system consists of a series of statements to be
described individually in the following chapters. In an interactive system these statements are
typed directly on the computer keyboard.

The individual IMP statements are divided into six categories which are described in detail in the
following chapters: Definition statements ([ManualChapter3|Chapter 3]) are used to define the component parts of the
system being modeled, the applied forces and torques, the fixed link, points of interest, etc., and
to specify their relationships to each other. Data statements ([ManualChapter4|Chapter 4]) are used to provide
numeric values for the parameters of the model. Request statements ([ManualChapter5|Chapter 5]) are those which
describe the entities for which analysis should be performed and the form of the output for each.
Control statements ([ManualChapter6|Chapter 6]) are used to set the mode of the analysis and to provide flexibility
and control over the simulation and the user's interaction with the terminal. Delete statements
([ManualChapter7|Chapter 7]) may be used to eliminate components from the system model. Graphics statements
([ManualChapter8|Chapter 8]) are used when a graphic device is at hand, and allow drawing different views of the
system model, showing animations, and plotting graphs of the simulation results.

### Continuation Lines ###
In all IMP statements, up to 72 columns may be typed on a single line and may begin anywhere on the
line, not necessarily in the first column. Characters typed beyond column 72 are ignored.

Each IMP statement must begin on a separate line.

Those IMP statements which are too long to be typed within the 72-column limitation may be continued
on the following line by ending the earlier line with the special character <tt>$</tt>. Upon seeing this
character, IMP ignores the remainder of the line and continues by reading the next line as a direct
extension of the preceding line. The <tt>$</tt> character may be placed within the middle of a word or
number without causing a problem.

Statements may be continued in this manner on as many lines as desired, with the restriction that
the total statement may not contain more than 35 total words and/or numbers.

### End of Statement ###
The end of an IMP statement may be indicated by the special characters <tt>$$</tt>. This is not necessary,
however, since the end of a statement is also assumed when a 72-column line is ended without a
continuation character (<tt>$</tt>).

Upon recognizing the <tt>$$</tt> characters, IMP ignores the remainder of the line, assumes that the
statement is complete, and processes the statement.

### Embedded Remarks ###
Since the remainder of a line is ignored once IMP recognizes the <tt>$</tt> or <tt>$$</tt> characters mentioned
above, the space remaining on a line after these characters may be used as desired. The user may,
for example, wish to add comments to the right of these characters to better document or explain
the model. These comments are printed with the output as the statement is read, but are completely
neglected in the simulation.

Two restrictions on embedded remarks are:

# that they may not be continued beyond the end of the current line, and
# that they may not contain the <tt>$</tt> or <tt>$$</tt> special characters.

#### Example ####
An example of an IMP statement which is continued to a second line and contains embedded remarks
follows:

> PRINT: POSITION (PIN1, PIN2, PIN3, $ THIS STATEMENT
> > PIN4, PTA, PTB)                  $$ REQUESTS POSITION RESULTS.

## IMP Words ##
Each IMP statement is made up of a series of words and/or numbers. Each word consists of one or
more alphanumeric characters (_A_ through _Z_, _a_ through _z_, or _0_ through _9_)
with the first character being alphabetic (_A_ through _Z_ or _a_ through _z_). Examples of
valid, though perhaps long, IMP words are:

**PIN** PINT12
**BallJoint**

Examples of invalid IMP words are:

**2ndJOINT _(invalid first character)_** BALL-SOCKET _(illegal character)_
**PIN JOINT _(two words)_**

Although IMP words may be as long as desired, the IMP system only recognizes the first four
characters of each word. Thus each new word must be distinguishable from other words by uniqueness
in spelling within the first four characters. Words such as <tt>POINT12</tt> and <tt>POINT35</tt> are both
recognized as <tt>POIN</tt>; they are not distinguishable (within the first four characters) and,
therefore, both refer to the same point. IMP prints its results referring to the point as <tt>POIN</tt>; if
two different points are intended, distinct names such as <tt>PT12</tt> and <tt>PT35</tt> should be chosen.

## IMP Keywords ##
Throughout the various IMP statements there are a number of keywords, named below, which are
recognized by IMP as having very specific meanings. For example, each IMP statement begins with a
keyword which signifies the type of statement and specifies the action to be taken.

These keywords and the formats of the IMP statements have been carefully chosen for their
conversational value during interaction. They are intended to provide a usable language, close to
the vocabulary of the typical designer, without requiring an excessive amount of typing.

The keywords recognized within IMP are as follows:


| <tt>ABS</tt> | <tt>ABSO</tt>lute | <tt>ACCE</tt>leration | <tt>ACOS</tt> | <tt>ALL</tt> | <tt>ALPH</tt>a | <tt>ANIM</tt>ate | <tt>ASIN</tt> |
|:-------------|:------------------|:----------------------|:--------------|:-------------|:---------------|:-----------------|:--------------|
| <tt>ATAN2</tt> | <tt>AXES</tt> | <tt>BACK</tt> | <tt>BASE</tt> | <tt>BEVEl</tt> | <tt>BLAC</tt>k | <tt>BLUE</tt> | <tt>BOTT</tt>om |
| <tt>CAM</tt> | <tt>CLEA</tt>r | <tt>CONS</tt>tant | <tt>CONT</tt>act | <tt>COS</tt> | <tt>CYAN</tt> | <tt>CYLI</tt>nder | <tt>DAMP</tt>er |
| <tt>DATA</tt> | <tt>DELE</tt>te | <tt>DENS</tt>ity | <tt>DEVI</tt>ce | <tt>DRAW</tt> | <tt>DYNA</tt>mic | <tt>END</tt> | <tt>EQUI</tt>librium  |
| <tt>ERAS</tt>e | <tt>EXEC</tt>ute | <tt>EXP</tt> | <tt>FIND</tt> | <tt>FINI</tt>sh | <tt>FLAT</tt> | <tt>FORC</tt>e | <tt>FREQ</tt>uency |
| <tt>FRON</tt>t | <tt>GEAR</tt> | <tt>GRAV</tt>ity | <tt>GREE</tt>n | <tt>GROU</tt>nd | <tt>HEAD</tt>ing | <tt>HOLD</tt> | <tt>IC</tt> |
| <tt>IDEN</tt>tify | <tt>IF</tt> | <tt>IMPA</tt>ct | <tt>INER</tt>tia | <tt>INPU</tt>t | <tt>ISOM</tt>etric | <tt>JOIN</tt>t | <tt>LEFT</tt> |
| <tt>LINK</tt> | <tt>LIST</tt> | <tt>LOG</tt> | <tt>LOG10</tt> | <tt>LOOP</tt> | <tt>MAGE</tt>nta | <tt>MASS</tt> | <tt>MOTI</tt>on |
| <tt>NONE</tt> | <tt>OFF</tt> | <tt>ON</tt> | <tt>OPEN</tt> | <tt>ORAN</tt>ge | <tt>PAIR</tt> | <tt>PAUS</tt>e | <tt>PI</tt> |
| <tt>PLAN</tt>ar | <tt>PLOT</tt> | <tt>POIN</tt>t | <tt>POSI</tt>tion | <tt>PRIN</tt>t | <tt>PRIS</tt>m | <tt>RACK</tt> | <tt>RECA</tt>ll |
| <tt>RED</tt> | <tt>REMA</tt>rk | <tt>RESE</tt>t | <tt>RETU</tt>rn | <tt>REVO</tt>lute | <tt>RIGH</tt>t | <tt>RIGI</tt>d | <tt>SCRE</tt>w |
| <tt>SHAP</tt>e | <tt>SHOW</tt> | <tt>SIN</tt> | <tt>SLID</tt>e | <tt>SLOT</tt> | <tt>SOLI</tt>d | <tt>SPHE</tt>re | <tt>SPRI</tt>ng |
| <tt>SQRT</tt> | <tt>STAT</tt>ic | <tt>STOR</tt>e | <tt>SYST</tt>em | <tt>T</tt> | <tt>TABL</tt>e | <tt>TAN</tt> | <tt>TIME</tt> |
| <tt>TITL</tt>e | <tt>TOP</tt> | <tt>TORQ</tt>ue | <tt>TURN</tt> | <tt>UJOI</tt>nt | <tt>UNIT</tt> | <tt>USER</tt> | <tt>VAL</tt> |
| <tt>VALU</tt>e | <tt>VELO</tt>city | <tt>VIEW</tt> | <tt>WHIT</tt>e | <tt>X</tt> | <tt>XPIN</tt> | <tt>XSLI</tt>de | <tt>Y</tt> |
| <tt>YELL</tt>ow | <tt>YPIN</tt> | <tt>YSLI</tt>de | <tt>Z</tt> | <tt>ZERO</tt> | <tt>ZOOM</tt> | <tt>ZPIN</tt> | <tt>ZSLI</tt>de |
| <tt>?</tt> | <tt>????</tt> | <tt>!</tt> |  |  |  |  |

These keywords, but not other words, are recognized by IMP whether they are spelled with upper case
or lower-case letters.

These _keywords_, or other words which begin with the same first four letters (either upper- or
lower-case), should not be used for other purposes, such as for names of components of the system
being modeled.

## IMP Numbers ##
When a numeric value is required in an IMP statement, IMP recognizes numbers made up of the digits
_0_ through _9_. A number may be proceeded by a plus sign or a minus sign and may contain a
decimal point. The decimal point is optional if the number is an integer. Examples of valid numbers
are:

**_-3.141592654_** _7_
**_+25._**

A number may be written with or without an exponent; however, an exponent is usually used only when
the value of the number is very large or very small. The exponent is an integer power of ten by
which the number is to be multiplied. The exponent follows the number and is signaled by the leading
character _E_ or _e_; the exponent may contain a plus or minus sign but may not contain a
decimal point. For example, the value _319,642.76_ may be expressed in any of the following ways:

**_319642.76_** _3.1964276E5_
**_+31.964276e+4_** _31964276E-2_

Numbers are distinguished from words by the fact that the first non-blank character of a number is a
plus or sign followed by a digit, a minus sign followed by a digit, a decimal point, or a digit
(_0_ through _9_). Once a number has been started, unrecognized characters are ignored. The
number is ended when a separator (see the next section) is encountered.

## IMP Separators ##
Adjacent words or numbers within an IMP statement must be separated from each other by one or more
blanks or by one of the following special characters called _separators_:

Table 2.2: IMP Separators
| , | comma |
|:--|:------|
| + | plus sign |
| ; | semicolon |
| - | minus sign |
| | asterisk |
| ( | left parenthesis |
| / | slash |
| = | equals sign |
| @ | at sign |


Except in <tt>VALUE</tt> expressions (see Section 2-7), these separators are treated in identical manner to
each other and are, therefore, interchangeable. The format of each IMP statement, however, leads to
the use of one over another because of their usual grammatical or algebraic connotations. Except in
<tt>VALUE</tt> expressions, if two separators other than blanks follow one another directly, the number
zero is implied between them. For example, the string of numbers:


> 3.14159, 2.25, , 1, 3.5

is read as:

> 3.14159, 2.25, 0, 1, 3.5

Since the plus and minus signs may either be separators or sign indications for numbers, however, a
plus or minus sign at the beginning of a number may follow a separator without an implied zero. For
example, the string of numbers:

> 3.14159 -2.25, , 1,+3.5

is interpreted as:

> 3.14159, -2.25, 0, 1, 3.5

It should be noticed that the right parenthesis character <tt>)</tt> is not listed as a separator. Except
in <tt>VALUE</tt> expressions, it is ignored by the IMP interpreter and may be used to balance the left
parenthesis without being counted as a separator. When a string of numbers is expected in an IMP
statement, and the final several numbers are zeros, the string of numbers may be truncated without
explicitly typing the trailing zeros or the separators. For example, the five numbers:

> 3.2,-1.5, 0, 0, 0

may be written as:

> 3.2,-1.5

if they appear at the end of an IMP statement. Use of this practice will be signaled with a warning
message, however.

## IMP Expressions - The <tt>VALUE</tt> Statement ##
In certain IMP statements it is desirable to allow data, which must otherwise be only numeric, to
depend on variable expressions or algebraic formulae involving time or the geometry or forces of the
system being simulated. When a simulation is made in the dynamic mode, for example, it is sometimes
useful to be able to describe the applied forces or motions as time dependent functions. This is the
purpose of the <tt>VALUE</tt> statement of the IMP language.

A <tt>VALUE</tt> statement is of the form:

> VALUE (name) = expression

where _name_ is an alphanumeric name identifying the expression, and _expression_ may be of any
of the several formats defined below. The _name_ chosen may then be used at certain appropriate
places in other statements of the IMP language in place of the corresponding numeric data.

There are several possible formats which may be used for the _expression_ in a <tt>VALUE</tt> statement.
These are intended, in general, to follow the familiar rules of algebra regarding the priority of
operations, the use of nested parentheses, etc. The recursive nature of nested parentheses permits
extremely complex expressions. However, it must be remembered that no IMP statement can exceed a
total of 35 words and/or numbers.

The possible formats which can be used for a <tt>VALUE</tt> _expression_ are as follows:

### A Number ###
An expression can consist of a single number or numeric value.

### The Keyword <tt>PI</tt> ###
The keyword <tt>PI</tt> can be used as a valid expression in place of the numeric value, _3.141592654_.

### A <tt>VALUE</tt> Name ###
The alphanumeric name of a previously defined <tt>VALUE</tt> expression may be used in forming a new
expression. The numeric value of the previous expression is used in evaluating the new expression.

### Another expression ###
Any valid form of expression can be used directly as a part of a more complex expression. It is not
necessary to define the partial expression with a <tt>VALUE</tt> name and to use its name in the more
complex expression, although this is also valid.

### Another Expression Enclosed in Parentheses ###
Any valid expression enclosed in parentheses also forms a valid expression. Enclosing an expression
in parentheses and using it as part of a more complex expression allows control over the priority of
operations in the evaluation of expressions since evaluation always proceeds with the innermost
level of parentheses first.

Any left parenthesis in an expression must be balanced by a corresponding right parenthesis. If
parentheses are not properly balanced, a message is printed and the <tt>VALUE</tt> statement is ignored.
The improper <tt>VALUE</tt> statement is not defined and its name has no defined value for use in the
evaluation of later expressions.

### The Sum of Two or More Expressions ###
Two or more expressions can be added to form a new expression. This is done by combining the two or
more expressions with plus signs in the form:

> expression + expression + expression

### The Difference of Two Expressions ###
One expression can be subtracted from another to form a new expression by combining them with a
minus sign in the form:

> expression - expression

If more than two expressions are combined with minus signs without parentheses, then the order of
the subtractions proceeds from left to right. If both plus and minus signs are used to combine
multiple expressions without parentheses, then all subtractions take place before additions.

In IMP expressions, the minus sign is used to imply subtraction rather than negation of an
expression. Except for a number without parentheses, a single expression should not begin with a
minus sign. Examples of invalid expressions are:

> VALUE (A) = -PI
> VALUE (B) = -(2.5)

This difficulty can be avoided by subtracting an expression from zero or by multiplying it by
negative unity when negation is desired.

### The Product of Two or More Expressions ###
Two or more expressions can be multiplied to form a new expression by combining them with an
asterisk (<tt>**</tt>). The format is:**

> expression **expression** expression

If expressions are multiplied without parentheses, then the order of the multiplication proceeds
from left to right. Multiplication is treated as a higher priority operation than addition or
subtraction; multiplications are done first unless otherwise indicated by parentheses.

### The Quotient of Two Expressions ###
Two expressions can be divided to form a new expression by combining them with a slash (<tt>/</tt>). The
format is:

> dividend expression / divisor expression

If multiple division operations are indicated among expressions without parentheses, then the order
of the divisions proceeds from left to right. Division is treated as a higher priority operation
than multiplication, and is done first unless otherwise indicated by parentheses.

If the _divisor expression_ has a zero value upon evaluation, then the resulting expression has an
undefined value.

### An Expression to the Power of Another ###
One expression can be raised to the power of another to form a new expression by combining them with
the operator (<tt>@</tt>) in the form:

> base expression @ power expression

If multiple power operations are indicated without parentheses, then the order of their evaluation
proceeds from left to right. The taking of powers is treated as a higher priority operation than
division and is done first unless otherwise indicated by parentheses.

Since the ultimate evaluation is done by logarithms, if the _base expression_ has a negative or
zero value upon evaluation, then the resulting expression has an undefined value.

### A Function Reference ###
An expression can consist of a reference to any of several possible IMP functions whose meanings are
defined below. Functions are of higher priority than algebraic operations and are evaluated first
unless otherwise indicated by parentheses.

### The <tt>TIME</tt> Function ###
The value of time during a simulation can be used to form an expression by reference to the function
<tt>TIME</tt> or its abbreviation <tt>T</tt>.

### The <tt>ABS</tt> Function ###
The absolute value of an expression can be used to form another expression by reference to the <tt>ABS</tt>
function in the following format:

> ABS (expression)

### The <tt>SIN</tt> Function ###
The trigonometric sine of an expression (in radians) can be used to form another expression by
reference to the <tt>SIN</tt> function in the following format:

> SIN (expression)

### The <tt>ASIN</tt> Function ###
The inverse trigonometric sine of an expression whose absolute magnitude is less than or equal to
one can be used to form another expression by reference to the <tt>ASIN</tt> function in the following
format:

> ASIN (expression)

The value returned by the <tt>ASIN</tt> function is in radians and is in the range -<tt>PI</tt>/2 &amp;lt;= <tt>ASIN</tt>
&amp;lt;= <tt>PI</tt>/2.

### The <tt>COS</tt> Function ###
The trigonometric cosine of an expression (in radians) can be used to form another expression by
reference to the <tt>COS</tt> function in the following format:

> COS (expression)

### The <tt>ACOS</tt> Function ###
The inverse trigonometric cosine of an expression whose absolute magnitude is less than or equal to
unity can be used to form another expression by reference to the <tt>ACOS</tt> function in the following
format:

> ACOS (expression)

The value returned by the <tt>ACOS</tt> function is in radians and is in the range 0 &amp;lt;= <tt>ACOS</tt> &amp;lt;=
<tt>PI</tt>.

### The <tt>EXP</tt> Function ###
The exponential, <tt>E</tt> (_2.7182818..._) raised to the power of an expression, can be used to form
another expression by reference to the <tt>EXP</tt> function in the following format:

> EXP (expression)

### The <tt>LOG</tt> Function ###
The natural (base <tt>E</tt>) logarithm of an expression can be used to form another expression by
reference to the <tt>LOG</tt> function in the following format:

> LOG (expression)

If the argument expression has a negative or zero value upon evaluation, then the <tt>LOG</tt> function
yields an undefined value.

### The <tt>LOG10</tt> Function ###
The decimal (base 10) logarithm of an expression can be used to form another expression by reference
to the <tt>LOG10</tt> function in the following format:

> LOG10 (expression)

If the argument expression has a negative or zero value upon evaluation, then the <tt>LOG10</tt> function
yields an undefined value.

### The <tt>SQRT</tt> Function ###
The positive square root of an expression can be used to form another expression by reference to the
<tt>SQRT</tt> function in the following format:

> SQRT (expression)

If the argument expression has a negative value upon evaluation, then the <tt>SQRT</tt> function yields an
undefined value.

### The <tt>TAN</tt> Function ###
The trigonometric tangent of an expression (in radians) can be used to form another expression by
reference to the <tt>TAN</tt> function in the following form:

> TAN (expression)

If the absolute magnitude of the expression is an odd multiple of <tt>PI</tt>/2, then the result of the
<tt>TAN</tt> function is undefined.

### The <tt>ATAN2</tt> Function ###
The inverse trigonometric tangent of the ratio of two expressions can be used to form another
expression by reference to the <tt>ATAN2</tt> function in the following format:

> ATAN2 (numerator expression, denominator expression)

The value returned by the <tt>ATAN2</tt> function is in radians. It is in the range -<tt>PI</tt> &amp;lt; <tt>ATAN2</tt>
&amp;lt;= <tt>PI</tt> as determined by assuming the signs of the two expressions to agree with the sine and
cosine of the angle, respectively. If both expressions have zero magnitude, the result of the
<tt>ATAN2</tt> is undefined.

Note that IMP has no <tt>ATAN</tt> function, and that IMP keywords are only distinct to the first four
characters. Therefore, the <tt>ATAN2</tt> function, with two arguments, should be used instead.

### The <tt>POSITION</tt> Function ###
The current position of a point, joint, spring, or damper in the system model can be used to form an
expression by reference to the <tt>POSITION</tt> function in the following format:

> POSITION (name, component)

where _name_ is the alphanumeric name of the point, joint, spring, or damper, and _component_ is
an integer defining the desired component of the named item's position. An expression can be used
for _component_ if desired, and its value is rounded to the nearest integer before interpreting it
as a component. Valid components depend on the type of the named item and are shown in the following
table:

{| border="1" cellpadding="5"
|+ align="bottom" | _Table 2-3:_ Position Component Numbers
! No. !! Point !! Joint !! Spring !! Damper
|-
| 1 | X coordinate | joint variable | &amp;Delta;X component || &amp;Delta;X component|
|:-------------|:---------------|:-----------------------|
|-
| 2 | Y coordinate | joint variable | &amp;Delta;Y component || &amp;Delta;Y component|
|-
| 3 | Z coordinate | joint variable | &amp;Delta;Z component || &amp;Delta;Z component|
|}

The value returned by the <tt>POSITION</tt> function has units of either radians or length as appropriate.

It must be understood that the <tt>POSITION</tt> function returns the instantaneous numeric value currently
stored in the IMP data structure rather than causing its reevaluation. For example, with the
following set of IMP commands:

> VALUE(X) = POSITION(JT2,1)
> DATA MOTION(JT4) = X
> EXECUTE

the position of joint _JT4_ will not necessarily be the true position of joint _JT2_, but may
lag by one time step. The value of _X_ is first set to the most recent value of _X_ (i.e., the
previous position of joint _JT2_; the position of SGC joint _JT4_ is then set to this position.
Finally, the mechanism is analyzed, probably causing joint _JT2_ to change position!)

### The <tt>VELOCITY</tt> Function ###
The current velocity of a point, joint, spring, or damper in the system model can be used to form an
expression by reference to the <tt>VELOCITY</tt> function in the following format:

> VELOCITY (name, component)

where _name_ is the alphanumeric name of the point, joint, spring, or damper, and _component_ is
an integer defining the desired component of the named item's velocity. A real number or an
expression can be used for _component_ if desired, and its value is rounded to the nearest integer
before interpreting it as a component. The valid components are similar to those in the above table
of <tt>POSITION</tt> components, except that the first time derivatives of the <tt>POSITION</tt> components are
evaluated. The value returned by the <tt>VELOCITY</tt> function has units of either radians per second or
length per second as appropriate.

It must be understood that the <tt>VELOCITY</tt> function returns the instantaneous numeric value currently
stored in the IMP data structure rather than causing its reevaluation. (See Section 2-7.24 for
further explanation).

Also note that, since IMP does not analyze for the derivative of acceleration, the second derivative
of the <tt>VELOCITY</tt> function returns an undefined value. Thus, it is not wise to use the <tt>VELOCITY</tt>
function in a <tt>VALUE</tt> expression to be used for a <tt>DATA MOTION</tt> statement, for example.

### The <tt>ACCEL</tt> Function ###
The current acceleration of a point, joint, spring, or damper in the system model can be used to
form an expression by reference to the <tt>ACCEL</tt> function in the following format:

> ACCEL (name, component)

where _name_ is the alphanumeric name of the point, joint, spring, or damper, and _component_ is
the integer number defining the desired component of the named item's acceleration. An expression
can be used for _component_ if desired; its value is rounded to the nearest integer before
interpreting it as a component number. The valid component numbers are similar to those in the above
table of <tt>POSITION</tt> component numbers, except that the second time derivatives of the <tt>POSITION</tt>
components are evaluated. The value returned by the <tt>ACCEL</tt> function has units of either radians per
second squared or length per second squared as appropriate.

It must be understood that the <tt>ACCEL</tt> function returns the instantaneous numeric value currently
stored in the IMP data structure rather than causing its reevaluation. (See Section 2-7.24 for
further explanation).

Also note that, since IMP does not analyze for derivatives of acceleration, the first and second
derivatives of the <tt>ACCEL</tt> function return undefined values. Thus, it is not wise to use the <tt>ACCEL</tt>
function in a <tt>VALUE</tt> expression to be used for a <tt>DATA MOTION</tt> statement, for example.

### The FORCE function ###
The current value of the force or torque within a joint, spring, or damper in the system model can
be used to form an expression by reference to the FORCE function in the following format:

> FORCE (name, component)

where _name_ is the alphanumeric name of the joint, spring, or damper, and _component_ is the
integer number of the force component to be evaluated. An expression can be used for _component_
if desired, and its value is rounded to the nearest integer before interpreting it as a component
number. For a spring or damper the component number must be one. For a joint, the component number
may be between one and six, and indicates the force along the local u, v, or w axis, or the torque
about the local u, v, or w axis of the joint, respectively. The value returned by the <tt>FORCE</tt>
function has units of either force or torque as appropriate.

It must be understood that the FORCE function causes evaluation of the desired force component(s)
under the current instantaneous conditions at the time of evaluation. If this <tt>FORCE</tt> value is then
used to set another input force, for example, the first force component found may change, and will
not necessarily be reevaluated until the next time step.

Also note that since IMP does not analyze for derivatives of forces, the first and second
derivatives of the <tt>FORCE</tt> function return undefined values. Thus, it is not wise to use the <tt>FORCE</tt>
function in a <tt>VALUE</tt> expression to be used for a <tt>DATA MOTION</tt> statement, for example.

### The <tt>IF</tt> Function ###
Conditional expressions can be formed by reference to the <tt>IF</tt> function in the following format:

> IF (value0: value1, value2, value3)

where each _value_ is a valid expression. The <tt>VALUE</tt> resulting from the evaluation of the <tt>IF</tt>
function is either _value1_, _value2_, or _value3_, depending on whether _value0_ is found
to be negative, zero, or positive, respectively.

### Tabular Data - The <tt>TABLE</tt> Function ###
Sometimes it is desirable to treat a tabular set of numerical (perhaps experimentally measured) data
as an expression in a <tt>VALUE</tt> statement. This may be done by reference to the <tt>TABLE</tt> function in
the following format:

> TABLE (name): filename

where _name_ is the alphanumeric name of another <tt>VALUE</tt> which acts as the independent variable
for the tabular data. For example, if the tabular data represent the functional relation
_Y = F(X)_, then the <tt>VALUE</tt> expression would be:

> VALUE (Y) = TABLE (X): filename

The _filename_ is the name of a previously prepared file which contains the numeric data. This
file contains one numeric value per line. The first two lines contain the minimum and maximum values
of the independent variable _X_, respectively, and thus signify the range of the tabular data. The
remaining lines of the file contain the numeric values of the tabular data, assumed given at equally
spaced increments and in increasing order of the independent variable _X_. During the IMP
simulation, the independent variable or expression _X_ is evaluated first; the value of the
<tt>TABLE</tt> function is then found by interpolating between the tabular data values using a Fourier
series for interpolation. If values of _X_ outside of the given range are encountered, the
interpolation is accomplished by assuming that the tabular data represents one cycle of a periodic
function.

### The <tt>USER</tt> Function ###
Specially developed functions, describing phenomena not otherwise available through IMP expressions,
can be incorporated into an expression by reference to the special <tt>USER</tt> function in the following
format:

> USER (name)

where _name_ is an alphanumeric name specified by the user to distinguish one reference to the
<tt>USER</tt> function from other possible references.

In order to evaluate a <tt>USER</tt> function, the user must also supply their own C function to describe
its meaning, and must obtain the cooperation of those supporting IMP at their installation in
compiling and loading this special C function with the rest of the IMP system. If such a C function
is not properly loaded, the default <tt>USER</tt> function has an undefined value whenever it is evaluated.

The user's special C function must have the following name and arguments:

  1. nclude "libimp.h"
> real user(Word name, real t, int nderiv)
> {
> > real value;
> > ...
> > value = ... ;
> > return(value);

> }

where the _name_ argument is of type Word (four-character, null terminated string) containing the
value of the _name_ parameter used in the <tt>USER</tt> function reference in the <tt>VALUE</tt> statement, the
_t_ argument is of type real (float or double as defined in libimp.h) and contains the current
value of time, and the _nderiv_ argument contains the integer value of 0, 1, or 2, requesting
return of a type real (float or double) value of the special <tt>USER</tt> function or its first or second
time derivative, respectively (when evaluated for use in an IMP statement).

### The <tt>RETURN</tt> and <tt>END</tt> Functions ###
The keywords <tt>RETURN</tt> and <tt>END</tt> can be used as IMP expressions in an IMP <tt>VALUE</tt> statement to cause
an immediate halt in the simulation at the time of its evaluation. This can be useful, for example,
along with the <tt>IF</tt> function, to cause a simulation to halt when some predefined condition of the
system is met. The <tt>RETURN</tt> function causes the simulation to halt, but returns to the IMP
interpreter to treat further IMP language statements. The <tt>END</tt> function, on the other hand, causes
an <tt>END</tt> to the entire simulation and a return to the computer's operating system.

## Units of Measurement ##
Among the four fundamental units of measurement (force, mass, length, and time), IMP treats the
units of force, length, and time as basic and the unit of mass to be derived consistent with
Newton's laws. Thus IMP presumes a _gravitational_ system of units.

IMP does not, however, make any presumption about which set of units is used. Any consistent set of
gravitational units is acceptable. What units are used for IMP input data is chosen by the user;
IMP then computes and presents results in consistent units of force, length, and time.

Because IMP presumes a consistent gravitational set of units has been chosen by the user, the
derived unit of mass must be defined by the user by use of the <tt>UNIT (MASS)</tt> statement
(see [ManualChapter6|Chapter 6]) before any mass or moments of inertia are entered. If a <tt>UNIT (MASS)</tt> statement is
not entered, IMP assumes that mass data are given in units of force time squared per unit length. As
examples, if force, length and time data are entered in pounds, feet, and seconds, then `UNIT (MASS)
= 1.0` should be specified and mass should be entered in pounds seconds squared per foot (slugs); if
data is entered in Newtons, meters, and seconds, then <tt>UNIT (MASS) = 1.0</tt> should be specified and
mass data should be entered in Newton seconds squared per meter (kilograms). If data is entered in
pounds, inches, and seconds, then <tt>UNIT (MASS) = 0.00259</tt> (the default) can be specified and mass
data may be entered in pounds.

## IMP Filenames ##
Under various circumstances the IMP user finds it desirable to save information in a computer file
or to have IMP access data from such a file. The conventions for naming such files, controlling
access to them, eliminating them after their need has been served, etc. vary widely with the
computer system being used and the policies of the particular installation. No attempt is made here
to explain these files in detail other than to say that IMP expects its files to be named consistent
with the particular installation. Additional information may be obtained from the group supporting
the installation of IMP on your system.