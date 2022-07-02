<!DOCTYPE html>
<html lang="en">
<head>
    <title>PHP Form Validation</title>
    <style>
        .error {
            color: brown;
        
        }

        .font {
            font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        }
        
    </style>
</head>
<body class="font">
    <?php
     $namaErr = $emailErr = ""; //false
     $nama = $email = ""; //true

     if ($_SERVER["REQUEST_METHOD"]=="POST"){
        if(empty($_POST["nama"])){
            $namaErr ="Nama harus diisi :)";
        }else{
            $nama = data_validasi($_POST["nama"]);
            if(!preg_match("/^[a-zA-Z-' ]*$/",$nama)){
                $namaErr = "Nama tidak sesuai!";
            }
        }

            if(empty($_POST["email"])){
                $emailErr ="Email harus diisi :)";
            }else{
                $email = data_validasi($_POST["email"]);
                if(!filter_var($email,FILTER_VALIDATE_EMAIL))
                $namaErr = "Email tidak sesuai!";
               
                }

        }
     function data_validasi($data){
        $data = trim($data);
        $data = stripslashes($data);
        $data = htmlspecialchars($data);
        return $data;

     }    
    ?>
     <h1>
        Form Validasi
    </h1>
    <p><span class="error">* WAJIB DIISI :(</span></p>
    <form method="POST" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
    Full Name :
    <input type="text" name="nama">
    <span class="error">* <?php echo $namaErr;?></span><br><br>
    Email :
    <input type="email" name="email" >
    <span class="error">* <?php echo $emailErr;?></span><br><br>

    <input type="submit" name="save" value="SAVE">

    </form>

    <?php
    echo "<h1>Output Data</h1>";
    echo "Full Name = ".$nama."<br>";
    echo "Email = ".$email."<br>";
    ?>
</body>
</html>
