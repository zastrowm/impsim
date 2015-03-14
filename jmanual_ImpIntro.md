# Imp Manual #
The Imp language was created so that every user that used this Physics Engine would be able to easy create any model that they wanted to no matter what experience they had.  A [plugin](jmanual_IMPPluginInstall.md) was developed for eclipse so that users could write in this language.   The core was developed so that it could also be used as a library in a user's custom java application.  An [API](jmanual_JavaAPI.md) was provided to accomplish that.

# IMP Basics #
The IMP (Integrated Mechanisms Program) language is a problem oriented language. It enables the user to describe a mechanical system to IMP and to request certain types of analyses using terms which are familiar to them. They are not required to be familiar with other computer programming languages such as C or Java.


## Individual Statements ##
Each IMP statement must begin on a separate line.  If a statement becomes too long for one line, the statement my be split onto multiple lines as long as the last part of the statement is delimited by a semicolon.  For example, the following long statement:
```
XPIN P1 Body1 Body2 1.2345678e9, 1.2345678e9, 1.2345678e9 1.2345678e9,1.2345678e9,1.2345678e9 1.2345678e9,1.2345678e9,1.2345678e9;
```
may be split into three lines like so
```
XPIN P1 Body1 Body2 1.2345678e9,1.2345678e9,1.2345678e9
                1.2345678e9,1.2345678e9,1.2345678e9
                1.2345678e9,1.2345678e9,1.2345678e9;
```
by placing a <tt>;</tt> on the end of the last line.

## Case Insensitivity ##
IMP is a case insensitive language, meaning it does not matter whether words are spelled with uppercase letters, lowercase letters, or any combination of the two.  The following three statements are equivalent to each other:

```
XPIN C A B
xpin c a b
xPiN c a B
```

# IMP Words #
Each IMP statement is made up of a series of words and/or numbers.  Each word consists of one or more alphanumeric characters (A-Z or 0-9) or underscore ('`_`') with the condition that the first character is not a number.  The following is a list of combinations and whether or not they are valid
| **Word** | **Valid or Invalid** |
|:---------|:---------------------|
| PIN | Valid |
| PIN12 | Valid |
|3PIN| Invalid (Begins with a number) |
| `_`PIN | Valid |
| Pin\_34 | Valid |
|MY-PIN| Invalid (Contains a dash) |
| `_`123 | Valid |
|Your Pin| Invalid (Contains a space) |

# Keywords #
While the number of words that you can use in IMP is unlimited, there are some words in the language which are reserved.  These are words that are used to define certain commands or expression, and thus cannot be used as a variable name.  The following lists all keywords in the IMP language:

|BECEL   | CYLINDER | DATA  | DATA | GEAR     | GROUND | IS | LINK |
|:-------|:---------|:------|:-----|:---------|:-------|:---|:-----|
| NUMBER | POINT    | PRISM | RACK | REVOLUTE | SCREW  | STRING | TICKS |
| TIME   | XPIN     | XSLIDE| YPIN | YSLIDE   | ZPIN   | ZSLIDE |