<?php
session_start();
?>
<html>
<head><title>Restaurant</title>
<link rel="stylesheet" href="css/style1.css" type="text/css" media="screen" />


</head>
<body>

<div id="maincontainer">
<div id="header">BOOK A TABLE</div>

<center>

<div class="form">

<div class="heading">Login</div>
<div class="form-field">

<center><form method = "post" action = "<?php $_SERVER['PHP_SELF']; ?>"
<br><br>E-mail id:<br>
<BR><div class="txt"><input type="email" name ="email"><br></div>
<br>Password:<br><br>
<div class="txt"><input type="password" name="pass"><br></div>
<br><br><input type="submit"value="Log In" name='submit'>
<br>

<br><br><a href="signup.php">SIGN UP<a>
</form></center>

<?php

if(isset($_POST['submit']))
{
$email=$_POST['email'];
$password=$_POST['pass'];

$flag = 0;

$host="localhost";
$user="root";
$pass="";
$db="rest";

$connection = mysql_connect($host,$user,$pass) or die("unable to connect");

mysql_select_db($db) or die("unable to connect");

$query = "select * from login";

$result = mysql_query($query) or die("unable to connect");

while($row = mysql_fetch_array($result)) 
{


if(($email == "admin@gmail.com") && ($password == "eazydiner"))
{
$userid = "admin@gmail.com";
$_SESSION['userid']=$userid;
 global $flag ;

	
	
	header('Location: admin.php');
}


//$session['id']=$id;
else if(($email == $row['1']) && ($password == $row['2']))
{
$userid = $row['id'];
$_SESSION['userid']=$userid;
 global $flag ;

 $flag = 1 ;
}
}

if($flag == 1)
{
echo "Login Successful";
header('Location: profile.php');
?>



<?php

}
else
{

?><center><FONT COLOR="red"><?php echo "The email-id or password you entered is incorrect.";?></FONT></center><?php
}

mysql_free_result($result);

mysql_close($connection);
}
?>



</div>

</div>
</center>
</body>

</html>
