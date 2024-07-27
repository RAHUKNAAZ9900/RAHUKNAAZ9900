role - VARCHAR - 11
The id of the admin is 1 and other users are > 1 that's how I tried to distinguish admin from other users.

<?php

$host="localhost"; // Host name
$username="root"; // Mysql username
$password="0000"; // Mysql password
$db_name="London Mobile"; // Database name
$tbl_name="members"; // Table name

// Connect to server and select database.
$link = mysqli_connect("$host", "$username", "$password", "$db_name") or die ("can't connect");


// To protect MySQL injection (more detail about MySQL injection)
$username = stripslashes($username);
$password = stripslashes($password);
$username = mysqli_real_escape_string($link, $username);
$password = mysqli_real_escape_string($link, $password);
$sql="SELECT * FROM $tbl_name WHERE username='$username' and password='$password'";
$result = mysqli_query($link, $sql);


// Mysql_num_row is counting table row
$count=mysqli_num_rows($result);

// $Query is where you run the query, and $rows is where you collect the number of records.
$query = mysqli_query($link, "SELECT id FROM MEMBERS WHERE username = username AND password = password");
$rows = mysqli_num_rows($result);


if ($rows == 1) {
    $rows = mysqli_fetch_assoc($query);
    $_SESSION['username'] = 'username';
    $_SESSION['role']   = 'admin';
    header("location: admin.php");
}

elseif ($rows > 1){
    $rows = mysqli_fetch_assoc($query);
    $_SESSION['username'] = 'username';
    $_SESSION['role']   = 'user';
    header("location: index.php");
}



?
