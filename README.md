
<?php

error_reporting(0);

include "koneksi.php";

?>

<html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

</head>

<center>

<body>

    <h1 align="center">LIST KAMAR</h1>

    <form action="" method="post">

    <input type="text" name="search_kamar" placeholder="Masukkan ID Kamar...">

    <input type="submit" name="search" value="Search">

        <table border="1">

            <tr>

                <th> NO </th>

                <th> ID KAMAR </th>

                <th> JENIS KAMAR </th>

                <th> DESKRIPSI </th>

                <th> HARGA </th>

                <th> OPSI </th>

            </tr>

        <?php

        $query=$_POST['search_kamar'];

        if ($query !=''){

            $show_kamar = mysqli_query ($koneksi, "select * from kamar where id_kamar like '%".$query."%' order by id_kamar asc");

        }else{

            $show_kamar = mysqli_query ($koneksi, "select * from kamar order by id_kamar asc");

        }

        if(mysqli_num_rows($show_kamar)){

            $no=1;

            foreach ($show_kamar as $row)

        {

            echo "<tr>

            <th> $no </th>

            <td> ".$row['id_kamar']." </td>

            <td> ".$row['jenis_kamar']." </td>

            <td> ".$row['deskripsi']." </td>

            <td> ".$row['harga']." </td>

            <td>

            <a href='updatekamar.php?id_kamar=$row[id_kamar]'> UPDATE </a> ||

            <a href='deletekamar.php?id_kamar=$row[id_kamar]'> DELETE </a>

            </td>

            </tr>";

            $no++;

        }

        ?>

        <?php }else{

            echo '<tr><td colspan = "6">Tidak ada data</td></tr>';

        }

        ?>

        </table>

    </form>

    <form action="insertkamar.php">

        <input type="submit" value="INSERT">

    </form>

    <form action="home.php">

        <input type="submit" value="GO BACK">

    </form>

    </body>

    </center>

</html>



-



<?php

error_reporting(0);

include "koneksi.php";

?>

<html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

</head>

<center>

<body>

    <h1 align="center">LIST RESERVASI</h1>

    <form action="" method="post">

    <input type="text" name="search_reservasi" placeholder="Masukkan ID Reservasi...">

    <input type="submit" name="search" value="Search">

        <table border="1">

            <tr>

                <th> NO </th>

                <th> ID RESERVASI </th>

                <th> JENIS KAMAR </th>

                <th> NAMA TAMU </th>

                <th> TANGGAL CHECKIN </th>

                <th> TANGGAL CHECKOUT </th>

                <th> OPSI </th>

            </tr>

        <?php

        $query=$_POST['search_reservasi'];

        if ($query !=''){

            $show_reservasi = mysqli_query ($koneksi, "select * from reservasi inner join kamar on kamar.id_kamar=reservasi.id_kamar inner join tamu on tamu.nik_tamu=reservasi.nik_tamu where id_reservasi like '%".$query."%' order by id_reservasi asc");

        }else{

            $show_reservasi = mysqli_query ($koneksi, "select * from reservasi inner join kamar on kamar.id_kamar=reservasi.id_kamar inner join tamu on tamu.nik_tamu=reservasi.nik_tamu order by id_reservasi asc");

        }

        if(mysqli_num_rows($show_reservasi)){

            $no=1;

            foreach ($show_reservasi as $row)

        {

            echo "<tr>

            <th> $no </th>

            <td> ".$row['id_reservasi']." </td>

            <td> ".$row['jenis_kamar']." </td>

            <td> ".$row['nama_tamu']." </td>

            <td> ".$row['tanggal_cin']." </td>

            <td> ".$row['tanggal_cout']." </td>

            <td>

            <a href='updatereservasi.php?id_reservasi=$row[id_reservasi]'> UPDATE </a> ||

            <a href='deletereservasi.php?id_reservasi=$row[id_reservasi]'> DELETE </a>

            </td>

            </tr>";

            $no++;

        }

        ?>

        <?php }else{

            echo '<tr><td colspan = "7">Tidak ada data</td></tr>';

        }

        ?>

        </table>

    </form>

    <form action="insertreservasi.php">

        <input type="submit" value="INSERT">

    </form>

    <form action="home.php">

        <input type="submit" value="GO BACK">

    </form>

    </body>

    </center>

</html> 



-



 <html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

    </head>

    <center>

    <body>

    <h1 align="center">INSERT KAMAR</h1>

    <form method="post" action="prosesinsertkamar.php">

    <table border="1">

        <tr>

            <td> ID KAMAR </td>

            <td> : </td>

            <td> <input type="text" name="id_kamar"> </td>

        </tr>

        <tr>

            <td> JENIS KAMAR </td>

            <td> : </td>

            <td> <input type="text" name="jenis_kamar"> </td>

        </tr>

        <tr>

            <td> DESKRIPSI </td>

            <td> : </td>

            <td> <input type="text" name="deskripsi"> </td>

        </tr>

        <tr>

            <td> HARGA </td>

            <td> : </td>

            <td> <input type="text" name="harga"> </td>

        </tr>

        <tr>

            <td colspan="3" align="right"><button>SUBMIT</button></td>

        </tr>

    </table>

    </form>

    <form action="showkamar.php">

        <input type="submit" value="GO BACK">

    </form>

    </body>

    </center>

</html>



-



<?php

include "koneksi.php";



$id_kamar = $_POST['id_kamar'];

$jenis_kamar = $_POST['jenis_kamar'];

$deskripsi = $_POST['deskripsi'];

$harga = $_POST['harga'];



$query = mysqli_query ($koneksi, "insert into kamar values ('$id_kamar', '$jenis_kamar', '$deskripsi', '$harga')");

header ("location:showkamar.php");

?>



-



<html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

    </head>

    <center>

    <body>

    <h1 align="center">INSERT RESERVASI</h1>

    <form method="post" action="prosesinsertreservasi.php">

    <table border="1">

        <tr>

            <td> ID RESERVASI </td>

            <td> : </td>

            <td> <input type="text" name="id_reservasi"> </td>

        </tr>

        <tr>

            <td> JENIS KAMAR </td>

            <td> : </td>

            <td> <select name="id_kamar" value="id_kamar">

                <option value="">--PILIH KAMAR--</option>

                <?php

                include "koneksi.php";

                $query= mysqli_query ($koneksi, "select * from kamar");

                while ($hasil=mysqli_fetch_array($query))

                {

                    echo "<option value='$hasil[0]' > $hasil[1] </option>";

                }

                ?>

            </select> </td>

        </tr>

        <tr>

            <td> NAMA TAMU </td>

            <td> : </td>

            <td> <select name="nik_tamu" value="nik_tamu">

                <option value="">--PILIH TAMU--</option>

                <?php

                include "koneksi.php";

                $query= mysqli_query ($koneksi, "select * from tamu");

                while ($hasil=mysqli_fetch_array($query))

                {

                    echo "<option value='$hasil[0]' > $hasil[1] </option>";

                }

                ?>

            </select> </td>

        </tr>

        <tr>

            <td> TANGGAL CHECKIN </td>

            <td> : </td>

            <td> <input type="datetime-local" name="tanggal_cin"> </td>

        </tr>

        <tr>

            <td> TANGGAL CHECKOUT </td>

            <td> : </td>

            <td> <input type="datetime-local" name="tanggal_cout"> </td>

        </tr>

        <tr>

            <td colspan="3" align="right"><button>SUBMIT</button></td>

        </tr>

    </table>

    </form>

    <form action="showreservasi.php">

        <input type="submit" value="GO BACK">

    </form>

    </body>

    </center>

</html>



-



<html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

    </head>

    <center>

    <body>

    <?php

    include "koneksi.php";

    $id_kamar = $_GET['id_kamar'];

    $query = mysqli_query ($koneksi, "select * from kamar where id_kamar = '$id_kamar'");

    $row = mysqli_fetch_array($query);

    ?>

    <h1 align="center">UPDATE KAMAR</h1>

    <form method="post" action="prosesupdatekamar.php">

    <table border="1">

        <tr>

            <td> ID KAMAR </td>

            <td> : </td>

            <td> <input type="text" name="id_kamar" readonly="readonly"

            value="<?php echo $row['id_kamar']; ?>"> </td>

        </tr>

        <tr>

            <td> JENIS KAMAR </td>

            <td> : </td>

            <td> <input type="text" name="jenis_kamar"

            value="<?php echo $row['jenis_kamar']; ?>"> </td>

        </tr>

        <tr>

            <td> DESKRIPSI </td>

            <td> : </td>

            <td> <input type="text" name="deskripsi"

            value="<?php echo $row['deskripsi']; ?>"> </td>

        </tr>

        <tr>

            <td> HARGA </td>

            <td> : </td>

            <td> <input type="text" name="harga"

            value="<?php echo $row['harga']; ?>"> </td>

        </tr>

        <tr>

            <td colspan="3" align="right"><button type="submit"> SUBMIT </button></td>

        </tr>

    </table>

    </form>

    <form action="showkamar.php">

        <input type="submit" value="GO BACK">

    </form>

    </body>

    </center>

</html>



-



<?php

include "koneksi.php";



$id_kamar = $_POST['id_kamar'];

$jenis_kamar = $_POST['jenis_kamar'];

$deskripsi = $_POST['deskripsi'];

$harga = $_POST['harga'];



$query = mysqli_query ($koneksi, "update kamar set jenis_kamar ='$jenis_kamar', deskripsi ='$deskripsi', harga ='$harga' where id_kamar='$id_kamar'");

if ($query)

{

    ?>

    <script>

        alert ("Update data berhasil");

        window.location.href="showkamar.php";

    </script>

    <?php

}

?>



-



<html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

    </head>

    <center>

    <body>

    <?php

    include "koneksi.php";

    $id_reservasi = $_GET['id_reservasi'];

    $query = mysqli_query ($koneksi, "select * from reservasi inner join kamar on kamar.id_kamar=reservasi.id_kamar inner join tamu on tamu.nik_tamu=reservasi.nik_tamu where id_reservasi = '$id_reservasi'");

    $row = mysqli_fetch_array($query);

    ?>

    <h1 align="center">UPDATE RESERVASI</h1>

    <form method="post" action="prosesupdatereservasi.php">

    <table border="1">

        <tr>

            <td> ID RESERVASI </td>

            <td> : </td>

            <td> <input type="text" name="id_reservasi" readonly="readonly"

            value="<?php echo $row['id_reservasi']; ?>"> </td>

        </tr>

        <tr>

            <td> JENIS KAMAR </td>

            <td> : </td>

            <td> <select name="id_kamar" value="id_kamar">

                <option value="<?php echo $row['id_kamar']; ?>"><?php echo $row['jenis_kamar']; ?></option>

                <?php

                include "koneksi.php";

                $query= mysqli_query ($koneksi, "select * from kamar");

                while ($hasil=mysqli_fetch_array($query))

                {

                    echo "<option value='$hasil[0]' > $hasil[1] </option>";

                }

                ?>

            </select> </td>

        </tr>

        <tr>

            <td> NAMA TAMU </td>

            <td> : </td>

            <td> <select name="nik_tamu" value="nik_tamu">

                <option value="<?php echo $row['nik_tamu']; ?>"><?php echo $row['nama_tamu']; ?></option>

                <?php

                include "koneksi.php";

                $query= mysqli_query ($koneksi, "select * from tamu");

                while ($hasil=mysqli_fetch_array($query))

                {

                    echo "<option value='$hasil[0]' > $hasil[1] </option>";

                }

                ?>

            </select> </td>

        </tr>

        <tr>

            <td> TANGGAL CHECKIN </td>

            <td> : </td>

            <td> <input type="datetime-local" name="tanggal_cin"

            value="<?php echo $row['tanggal_cin']; ?>"> </td>

        </tr>

        <tr>

            <td> TANGGAL CHECKOUT </td>

            <td> : </td>

            <td> <input type="datetime-local" name="tanggal_cout"

            value="<?php echo $row['tanggal_cout']; ?>"> </td>

        </tr>

        <tr>

            <td colspan="3" align="right"><button type="submit"> SUBMIT </button></td>

        </tr>

    </table>

    </form>

    <form action="showreservasi.php">

        <input type="submit" value="GO BACK">

    </form>

    </body>

    </center>

</html> 



-



 <?php

include "koneksi.php";



$id_kamar = $_GET['id_kamar'];



$delete = mysqli_query ($koneksi, "delete from kamar where id_kamar = '$id_kamar'");

?>

<script>

    alert ("Data berhasil dihapus");

    document.location = "showkamar.php";

</script>



-



 <?php

$koneksi= mysqli_connect("localhost", "root", "", "hotel");

?>



-



 <html>

    <head>

        <title>

            AKSATA MINI HOTEL

        </title>

    </head>

    <br>

    <br>

    <h1 align="center">AKSATA MINI HOTEL</h1>

    <h4 align="center">"because your satisfaction is our priority"</h4>

    <br>

    <br>

    <br>

    <br>

    <br>

    <br>

    <br>

    <br>

    <body>

        <center>

        <form method="POST" action="proseslogin.php">

            <table align="center" border="2">

        <tr>

            <td> USERNAME </td>

            <td> : </td>

            <td> <input type="text" name="username" placeholder="type your username..."> </td>

        </tr>

        <br>

        <tr>

            <td> PASSWORD </td>

            <td> : </td>

            <td> <input type="password" name="password" placeholder="type your password..."> </td>

        </tr>

        <tr>

        <td colspan="3" align="right"><input type="submit" value="SUBMIT" style=padding:7px;>

        <input type="reset" value="RESET" style=padding:7px;>

        </td>

        </tr>

        </table>

        </form>

        <form action="index.php">

            <input type="submit" value="GO BACK">

        </form>

        </center>

    </body>

</html>



-



<?php

include "koneksi.php";



$username = $_POST['username'];

$password = $_POST['password'];

$query = mysqli_query($koneksi, "select * from login where username = '$username' and password = '$password'");

$query1 = mysqli_num_rows($query);



if ($query1) {

 session_start();

 $_SESSION['username']=$username;

 header("location:home.php");

}

else {

?>

<script>

    alert ("Maaf, username atau password anda salah");

    document.location="login.php";

</script>

<?php

}

?>



-



<?php

session_start();

session_destroy();

header("location:login.php");

?>

