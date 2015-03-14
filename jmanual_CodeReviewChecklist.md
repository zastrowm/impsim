# Code Review Checklist #

<table cellpadding='20' border='1' cellspacing='0'>
<tbody><tr>
<td>  Design   </td><td>
<ul><li>Code follows design   </td><td>   1<br>
</td>
<tr>
<td>   Constructors    </td><td>
</li><li>Class variables initialized <br>
</li><li>Accepts proper parameter types <br>
</li><li>Accepts correct number of parameters <br>
</li><li>ArrayList sizes are checked for correct number of elements <br>
</li><li>Null checking<br>
<td>   2</td>
<tr>
<td>   Methods   </td>
<td>
</li><li>Correct returns <br>
</li><li>Not too large (break large methods into several smaller ones for testing and reduce complexity) <br>
</li><li>Check for Null on the public facing API<br>
<td> 3</td></li></ul>

<tr>
<td>   Documentation </td><td>
<ul><li>JavaDoc <br>
</li><li>Commented algorithms <br>
</li><li>Implementation matches diagram<br>
<td> 4</td>
<tr>
<td>   Variables  </td><td>
</li><li>Descriptive names <br>
</li><li>Correct visibility (public/private/protected) <br>
</li><li>Getters/Setters<br>
<td>  5</td>
<tr>
<td>   Resources (IO, Threads, etc.)</td><td>
</li><li>Closed at end of use<br>
<td> 6 </td>
<tr>
<td>   Loops  </td>
<td>
</li><li>Check for off-by-one errors<br>
</li><li>Check for infinite loops<br>
<td> 7</td>
<tr>
<td>  Standards </td><td>
</li><li><a href='jmanual_CodeStandards.md'>Code Standards</a> followed<br>
</li><li><a href='jmanual_CommentStandards.md'>Comment Standards</a> followed<br>
</li><li><a href='jmanual_FormattingStandards.md'>Formatting Standards</a> followed<br>
</li><li><a href='jmanual_NamingStandards.md'>Naming Standards</a> followed<br>
<td> 8<br>
</td>