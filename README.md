# Praktikum 9

Illda Febryawan Budiono
311910749
TI.19.A.2

### LANGKAH-LANGKAH
#### 1. Buka XAMPP, aktifkan Apache dan MySQL
![1](https://user-images.githubusercontent.com/85242560/120509643-e49e1780-c3f2-11eb-8bd7-ce6c723f274c.png)

#### 2. Buat folder `lab9_php_modular` pada root directory web server `(d:\xampp\htdocs)`
![2](https://user-images.githubusercontent.com/85242560/120510084-478fae80-c3f3-11eb-9ee8-00c4414c9360.png)

#### 3. Buat file baru dengan nama `header.php`
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contoh Modularisasi</title>
    <link href="style.css" rel="stylesheet" type="text/stylesheet" media="screen" />
</head>
<body>
    <div class="container">
        <header>
            <h1>Modularisasi Menggunakan Require</h1>
        </header>
        <nav>
        <a href="home.php">Home</a>
        <a href="about.php">Tentang</a>
        <a href="kontak.php">Kontak</a>
        </nav>
```
![3](https://user-images.githubusercontent.com/85242560/120510486-ac4b0900-c3f3-11eb-9bbb-c3498bbba6cf.png)

#### 4. Buat file baru dengan nama `footer.php`
```
        <footer>
            <p>&copy; 2021, Informatika, Universitas Pelita Bangsa</p>
        </footer>
    </div>
</body>
</html>
```
![4](https://user-images.githubusercontent.com/85242560/120510728-e74d3c80-c3f3-11eb-8131-3606cff17e16.png)

#### 5. Buat file baru dengan nama `home.php`
```
<?php require('header.php'); ?>

<div class="content">
    <h2>Ini Halaman Home</h2>
    <p>Ini adalah bagian content dari halaman.</p>
</div>

<?php require('footer.php'); ?>
```
![5](https://user-images.githubusercontent.com/85242560/120510959-211e4300-c3f4-11eb-811f-472c6c84d1b1.png)

#### 6. Buat file baru dengan nama `about.php
```
<?php require('header.php'); ?>

<div class="content">
    <h2>Ini Halaman About</h2>
    <p>Ini adalah bagian content dari halaman.</p>
</div>

<?php require('footer.php'); ?>
```
![6](https://user-images.githubusercontent.com/85242560/120511125-4ad76a00-c3f4-11eb-87b8-080ad150d713.png)

#### Hasil Akhir
* Halaman Home
![7 halaman home](https://user-images.githubusercontent.com/85242560/120511327-82dead00-c3f4-11eb-8001-7ba3fe6e9864.png)
* Halaman About
![7 halaman about](https://user-images.githubusercontent.com/85242560/120511343-86723400-c3f4-11eb-8198-527c5e74e34d.png)

## TUGAS
### Implementasikan konsep modularisasi pada kode program `praktikum 8 tentang database`, sehingga setiap halamannya memiliki template tampilan yang sama.
### LANGKAH-LANGKAH
#### 1. Buat folder `lab9_php_tugas` pada root directory web server `(d:\xampp\htdocs)`
![tugas 1](https://user-images.githubusercontent.com/85242560/120517551-c63c1a00-c3fa-11eb-825a-903e5b4e16d4.png)
#### 2. Buat file baru dengan nama `koneksi.php` untuk mengkoneksikan dengan Database
```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan1";
$conn = mysqli_connect($host, $user, $pass, $db);

if ($conn == false)
{
    echo "Koneksi ke server gagal.";
    die();
} #else echo "Koneksi berhasil";
?>
```
![tugas 2](https://user-images.githubusercontent.com/85242560/120517593-d05e1880-c3fa-11eb-82d4-3781b641235d.png)
#### 3. Buat file baru dengan nama `header.php`
```
<?php
include("koneksi.php");

// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Modularisasi Database</title>
    <link href="style.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <div id="container">
        <header>
            <h1>Database</h1>
        </header>
        <nav>
            <a href="home.php">Home</a>
            <a href="tambah.php">Tambah Barang</a>
        </nav>
```
![tugas 3](https://user-images.githubusercontent.com/85242560/120517801-056a6b00-c3fb-11eb-8618-9c3f7fccf9c1.png)
#### 4. Buat file baru dengan nama `footer.php`
```
        <footer>
            <p>&copy; 2021, Illda Febryawan Budiono, 311910749, TI.19.A.2</p>
        </footer>
    </div>
</body>
</html>
```
![tugas 4](https://user-images.githubusercontent.com/85242560/120517921-2d59ce80-c3fb-11eb-889a-cfe4a551a21b.png)
#### 5. Buat file baru dengan nama `home.php`
```
<?php require('header.php'); ?>

<div class="content">
    <h1>Data Barang</h1>
    <div class="main">
        <table>
        <tr>
            <th>Gambar</th>
            <th>Nama Barang</th>
            <th>Katagori</th>
            <th>Harga Jual</th>
            <th>Harga Beli</th>
            <th>Stok</th>
            <th>Aksi</th>
        </tr>
        <?php if($result): ?>
        <?php while($row = mysqli_fetch_array($result)): ?>
        <tr>
            <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=$row['nama'];?>"></td>
            <td><?= $row['nama'];?></td>
            <td><?= $row['kategori'];?></td>
            <td><?= $row['harga_jual'];?></td>
            <td><?= $row['harga_beli'];?></td>
            <td><?= $row['stok'];?></td>
            <td>
                <a href="ubah.php?id=<?= $row['id_barang'];?>">Ubah</a>
                <a href="hapus.php?id=<?= $row['id_barang'];?>">Hapus</a> 
            </td>
        </tr>
        <?php endwhile; else: ?>
        <tr>
            <td colspan="7">Belum ada data</td>
        </tr>
        <?php endif; ?>
        </table>
    </div>
</div>

<?php require('footer.php'); ?>
```
![tugas 5 (1)](https://user-images.githubusercontent.com/85242560/120518165-7ad63b80-c3fb-11eb-81ec-ac38f3fd7e91.png)
![tugas 5 (2)](https://user-images.githubusercontent.com/85242560/120518169-7c9fff00-c3fb-11eb-8140-24244c2f48d1.png)
#### 6. Buat file baru dengan nama `tambah.php`
```
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit']))
{
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_',$file_gambar['name']);
        $destination = dirname(__FILE__) .'/gambar/' . $filename;
        if(move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }
    
    $sql = 'INSERT INTO data_barang (nama, kategori, harga_jual, harga_beli, stok, gambar) ';
    $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}','{$harga_beli}', '{$stok}', '{$gambar}')";
    $result = mysqli_query($conn, $sql);
    header('location: home.php');
}
?>

<?php require('header.php'); ?>

<div class="content">
    <h1>Tambah Barang</h1>
    <div class="main">
        <form method="post" action="tambah.php" enctype="multipart/form-data">
            <div class="input">
                <label>Nama Barang</label>
                <input type="text" name="nama" style="margin-left: 20px;" />
            </div>
            <div class="input">
                <label>Kategori</label>
                <select name="kategori" style="margin-left: 58px;" >
                    <option value="Komputer">Komputer</option>
                    <option value="Elektronik">Elektronik</option>
                    <option value="Hand Phone">Hand Phone</option>
                </select>
            </div>
            <div class="input">
                <label>Harga Jual</label>
                <input type="text" name="harga_jual" style="margin-left: 40px;" />
            </div>
            <div class="input">
                <label>Harga Beli</label>
                <input type="text" name="harga_beli" style="margin-left: 43px;" />
            </div>
            <div class="input">
                <label>Stok</label>
                <input type="text" name="stok" style="margin-left: 85px;" />
            </div>
            <div class="input">
                <label>File Gambar</label>
                <input type="file" name="file_gambar" />
            </div>
            <div class="submit">
                <input type="submit" name="submit" value="Simpan" />
            </div>
        </form>
    </div>
</div>

<?php require('footer.php'); ?>
```
![tugas 6 (1)](https://user-images.githubusercontent.com/85242560/120518395-bcff7d00-c3fb-11eb-8250-91a2c1983eda.png)
![tugas 6 (2)](https://user-images.githubusercontent.com/85242560/120518403-bec94080-c3fb-11eb-9c06-46f87c3c00a2.png)
![tugas 6 (3)](https://user-images.githubusercontent.com/85242560/120518406-bf61d700-c3fb-11eb-9f11-9881ec0912b8.png)
#### 7. Buat file baru dengan nama `ubah.php`
```
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit']))
{
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        if (move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }

    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";
    if (!empty($gambar))
        $sql .= ", gambar = '{$gambar}' ";
    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);

    header('location: home.php');
    }

    $id = $_GET['id'];
    $sql = "SELECT * FROM data_barang WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);
    if (!$result) die('Error: Data tidak tersedia');
    $data = mysqli_fetch_array($result);

    function is_select($var, $val) {
        if ($var == $val) return 'selected="selected"';
        return false;
}
?>

<?php require('header.php'); ?>

<div class="content">
    <h1>Ubah Barang</h1>
    <div class="main">
        <form method="post" action="ubah.php" enctype="multipart/form-data">
            <div class="input">
                <label>Nama Barang</label>
                <input type="text" name="nama" value="<?php echo $data['nama'];?>" style="margin-left: 20px;"/>
            </div>
            <div class="input">
                <label>Kategori</label>
                <select name="kategori" style="margin-left: 58px;">
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Elektronik">Elektronik</option>
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
                </select>
            </div>
            <div class="input">
                <label>Harga Jual</label>
                <input type="text" name="harga_jual" value="<?php echo $data['harga_jual'];?>" style="margin-left: 40px;"/>
            </div>
            <div class="input">
                <label>Harga Beli</label>
                <input type="text" name="harga_beli" value="<?php echo $data['harga_beli'];?>" style="margin-left: 43px;"/>
            </div>
            <div class="input">
                <label>Stok</label>
                <input type="text" name="stok" value="<?php echo $data['stok'];?>" style="margin-left: 85px;"/>
            </div>
            <div class="input">
                <label>File Gambar</label>
                <input type="file" name="file_gambar" />
            </div>
            <div class="submit">
                <input type="hidden" name="id" value="<?php echo $data['id_barang'];?>" />
                    <input type="submit" name="submit" value="Simpan" />
            </div>
        </form>
    </div>
</div>

<?php require('footer.php'); ?>
```
![tugas 7 (1)](https://user-images.githubusercontent.com/85242560/120518758-19629c80-c3fc-11eb-8630-47a218c3eb73.png)
![tugas 7 (2)](https://user-images.githubusercontent.com/85242560/120518763-1bc4f680-c3fc-11eb-8da3-295e8512a373.png)
![tugas 7 (3)](https://user-images.githubusercontent.com/85242560/120518766-1c5d8d00-c3fc-11eb-8dc8-efabd96685e2.png)
#### 8. Buat file baru dengan nama `hapus.php`
```
<?php
include_once 'koneksi.php';
$id = $_GET['id'];
$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
header('location: home.php');
?>
```
![tugas 8 (1)](https://user-images.githubusercontent.com/85242560/120518951-5038b280-c3fc-11eb-880d-51f7a48a498e.png)
#### 9. Tambahkan CSS untuk mempercantik tampilan. Buat file baru dengan nama `style.css`
```
/* import google font */
@import
url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,600;0,700;0,800;1,300;1,400;1,600;1,700;1,800&display=swap');
@import
url('https://fonts.googleapis.com/css2?family=Open+Sans+Condensed:ital,wght@0,300;0,700;1,300&display=swap');

/* Reset CSS */
* {
    margin: 0;
    padding: 0;
}
body {
    line-height:1;
    font-size:100%;
    font-family:'Open Sans', sans-serif;
    color:#5a5a5a;
}
#container {
    width: 980px;
    margin: 0 auto;
    box-shadow: 0 0 1em #cccccc;
}

/* header */
header {
    padding: 20px;
}
header h1 {
    margin: 20px 10px;
    color: #000000;
}

/* navigasi */
nav {
    display: block;
    background-color: #af0b0b;
}
nav a {
    padding: 15px 30px;
    display: inline-block;
    color: #ffffff;
    font-size: 14px;
    text-decoration: none;
    font-weight: bold;
}
nav a.active,
nav a:hover {
    background-color: #ea2b2b;
}

/* Content Panel */
.content {
    background-color: #e4e4e5;
    padding: 50px 20px;
    margin-bottom: 20px;
}
.content h1 {
    margin-bottom: 20px;
    font-size: 35px;
}
.content p {
    margin-bottom: 20px;
    font-size: 18px;
    line-height: 25px;
}

/* footer */
footer {
    clear:both;
    background-color:#5a5a5a;
    padding:20px;
    color:#eee;
}

/* tabel */
body{
    font-family: sans-serif;
}
table{
    border-collapse: collapse;
}
th, td{
    border: 1px solid black;
    font-size: 16px;
    padding: 7px 9px;
}
table th {
    background:#af0b0b;
    color:#DCDCDC;
    font-weight:bold;
    font-size:14px;
}
table tr:nth-child(even) {
    background:#F0F8FF;
}

/* Tambah Barang */
.input{
    padding: 5px;
}
```
![tugas 9 (1)](https://user-images.githubusercontent.com/85242560/120519359-b6bdd080-c3fc-11eb-8913-4cb18b64864f.png)
![tugas 9 (2)](https://user-images.githubusercontent.com/85242560/120519364-b8879400-c3fc-11eb-84c2-4022a533ff3e.png)
![tugas 9 (3)](https://user-images.githubusercontent.com/85242560/120519369-b9202a80-c3fc-11eb-89f0-7735d93d02a6.png)
![tugas 9 (4)](https://user-images.githubusercontent.com/85242560/120519373-ba515780-c3fc-11eb-9bfa-fd95ee4f4622.png)
#### Hasil Akhir
* Halaman Home
![tugas 5 (hasil)](https://user-images.githubusercontent.com/85242560/120519621-06040100-c3fd-11eb-8426-458f37bb6b8a.png)
* Halaman Tambah Barang
![tugas 6 (hasil)](https://user-images.githubusercontent.com/85242560/120519631-09978800-c3fd-11eb-9d1b-42dddd40dde3.png)
* Halaman Ubah Barang
![tugas 7 (hasil)](https://user-images.githubusercontent.com/85242560/120519663-13b98680-c3fd-11eb-8e00-e1e590027360.png)
