<?php
     
     session_start();
     $username="";
     $email ="";
     $errors = array( );
    # $password_2="";
     #$password_1="";
    
    //connect to database
    $db=mysqli_connect('localhost','root','','registeration');
    
    //if the register button is clicked
    if (isset($_POST['register']))
     {
    	
    	$username =mysqli_real_escape_string($db,$_POST['username']);

    	$email    =mysqli_real_escape_string($db,$_POST['email']);

    	$password_1 =mysqli_real_escape_string($db,$_POST['password_1']);

    	$password_2 =mysqli_real_escape_string($db,$_POST['password_2']);
    	// ensure that the form fields are filled properly

    	if (empty($username))
    	 {
    		array_push($errors, "<strong><ins> Username</ins></strong> is  required");
    		//add errors to errors array 
    	}
       
       if (empty($email))
    	 {
    		array_push($errors, "<strong><ins>Email</ins></strong> is  required");
    		 
    	}
    	
    	if (empty($password_1))
    	 {
    		array_push($errors, "<strong><ins>Password</ins></strong> is  required");
        }

        if($password_1 != $password_2)
        {
            array_push($errors,"<strong><ins>The Passwords Do not Match</ins></strong>");
        }
        // if there are no errors , save user to database
        $user_check_query = "SELECT * FROM users WHERE username='$username' OR email='$email' LIMIT 1";
          $result = mysqli_query($db, $user_check_query);
          $user = mysqli_fetch_assoc($result);
          
          if ($user) { // if user exists
            if ($user['username'] === $username) {
              array_push($errors, "Username already exists");
            }

            if ($user['email'] === $email) {
              array_push($errors, "Email already exists");
            }
          }
        if(count($errors) == 0)
        {
        	$password =md5($password_1);
        	//encrypt password before storing in database(security)
        	#$sql="INSERT INTO users(username ,email,password) 
             #     VALUES('$username',$email,'$password')";
        	#mysqli_query($db,$sql);
            $sql = "INSERT INTO users (username, email, password) 
              VALUES('$username', '$email', '$password')";
                mysqli_query($db, $sql);
                $_SESSION['username'] = $username;
                $_SESSION['success'] = "You are now logged in";
                header('location: index.php');
        } 
    }

    #login user
    if (isset($_POST['login'])) 
    {
          $username = mysqli_real_escape_string($db, $_POST['username']);
          $password = mysqli_real_escape_string($db, $_POST['password']);

          if (empty($username)) {
            array_push($errors, "Username is required");
          }
          if (empty($password)) {
            array_push($errors, "Password is required");
          }

          if (count($errors) == 0) 
          {
            $password = md5($password);
            $query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
            $results = mysqli_query($db, $query);
            if (mysqli_num_rows($results) == 1)
            {
              $_SESSION['username'] = $username;
              $_SESSION['success'] = "You are now logged in";
              header('location: index.php');
            }
          
            else
            {
                array_push($errors, "Wrong username/password combination");
            }
          }
    }




?>
