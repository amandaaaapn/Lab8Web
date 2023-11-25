# Lab8Web

Nama            : Amanda Puspa Negara

NIM             : 312210129

Kelas           : TI.22.A.1

Mata Kuliah     : Pemrograman Web 1

Dosen Pengampu  : Agung Nugroho, S.Kom., M.Kom

# Instruksi Praktikum

1. Persiapkan text editor misalnya VSCode.
   
2. Buat folder baru dengan nama lab8_php_database pada docroot webserver (htdocs)

3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.

# Langkah-Langkah Praktikum

# Persiapan

Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah database server menggunakan MySQL. Pastikan MySQL Server sudah dapat dijalankan melalui XAMPP.

# Menjalankan MySQL Server

Untuk menjalankan MySQL Server dari menu XAMPP Contol.

![Screenshot 2023-11-19 104247](https://github.com/amandaaaapn/Lab8Web/assets/115678845/f51f9c1f-2f71-4700-a499-67a6f7528ad9)

# Mengakses MySQL Client menggunakan PHP MyAdmin

Pastikan webserver Apache dan MySQL server sudah dijalankan. Kemudian buka melalui browser: http://localhost/phpmyadmin/

# Membuat Database: Studi Kasus Data Barang

# Membuat Database

        CREATE DATABASE latihan1;

# Membuat Tabel

          CREATE TABLE data_barang (
            id_barang int(10) auto_increment Primary Key,
            kategori varchar(30),
            nama varchar(30),
            gambar varchar(100),
            harga_beli decimal(10,0),
            harga_jual decimal(10,0),
            stok int(4)
          );

![Screenshot 2023-11-25 114641](https://github.com/amandaaaapn/Lab8Web/assets/115678845/81df9a25-343a-4641-be20-8bc11d0f20cc)

# Menambahkan Data

          INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
          VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
          ('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
          ('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);

# Membuat Program CRUD

1. Buat folder lab8_php_database pada root directory web server (c:\xampp\htdocs)

![Screenshot 2023-11-25 114830](https://github.com/amandaaaapn/Lab8Web/assets/115678845/dd9639a3-533f-445e-9593-24e43e207f4b)


2. Kemudian untuk mengakses direktory tersebut pada web server dengan mengakses URL: 
 http://localhost/lab8_php_database/

![database](https://github.com/amandaaaapn/Lab8Web/assets/115678845/a943fdf6-9fc0-4c76-9127-ca88f697831d)

# Membuat File Koneksi Database

1. Buat file baru dengan nama koneksi.php

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
            } else echo "Koneksi berhasil";
            ?>

2. Buka melalui browser untuk menguji koneksi database (untuk menyampilkan pesan koneksi berhasil, uncomment pada perintah echo “koneksi berhasil”;
   
![Screenshot 2023-11-25 115508](https://github.com/amandaaaapn/Lab8Web/assets/115678845/f660d55c-5b3e-4b1d-9cb7-12d7fb9581e3)

# Membuat File Index Untuk Menampilkan Data (Read)

* Buat file baru dengan nama index.php

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
                      <link href="style.css" rel="stylesheet" type="text/css" />
                      <title>Data Barang</title>
                </head>
                <body>
                    <div class="container">
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
                                    <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=
                $row['nama'];?>"></td>
                                    <td><?= $row['nama'];?></td>
                                    <td><?= $row['kategori'];?></td>
                                    <td><?= $row['harga_beli'];?></td>
                                    <td><?= $row['harga_jual'];?></td>
                                    <td><?= $row['stok'];?></td>
                                    <td><?= $row['id_barang'];?></td>
                              </tr>
                              <?php endwhile; else: ?>
                              <tr>
                                  <td colspan="7">Belum ada data</td>
                              </tr>
                              <?php endif; ?>
                              </table>
                          </div>
                    </div>
                </body>
                </html>

* Buat file baru lagi untuk dengan nama style.css

            body {
              font-family: Arial, sans-serif;
              background-color: #f4f4f4;
              margin: 0;
              padding: 0;
            }
            
            .container {
              max-width: 800px;
              margin: 20px auto;
              background-color: #fff;
              padding: 20px;
              box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            }
            
            h1 {
              text-align: center;
            }
            
            .main {
              margin-top: 20px;
            }
            
            .tambah {
              display: inline-block;
              padding: 15px 15px;
              background-color: #0151f2;
              color: #fff;
              text-decoration: none;
              border-radius: 10px;
            }
            
            .table, td, th {
                border: 1px solid;
                border: 1px solid #ddd;
                padding: 12px;
                text-align: left;
              }
              
              table {
                width: 100%;
                border-collapse: collapse;
                margin-top: 15px;
              }
            
              img {
                max-width: 80px;
                height: auto;
            }

  ![Screenshot 2023-11-25 115733](https://github.com/amandaaaapn/Lab8Web/assets/115678845/d18f9b65-c402-4876-a6ce-2c598fd70d10)

# Menambahkan Data (Create)

* Buat file baru dengan nama tambah.php

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
              $sql = 'INSERT INTO data_barang (nama, kategori,harga_jual, harga_beli,
          stok, gambar) ';
              $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}',
          '{$harga_beli}', '{$stok}', '{$gambar}')";
              $result = mysqli_query($conn, $sql);
              header('location: index.php');
          }
          ?>
          <!DOCTYPE html>
          <html lang="en">
          <head>
              <meta charset="UTF-8">
              <link href="style.css" rel="stylesheet" type="text/css" />
              <title>Tambah Barang</title>
          <style>
           body {
                      font-family: Arial, sans-serif;
                      background-color: #f4f4f4;
                      margin: 0;
                      padding: 0;
                  }
          
          input[type=text], select, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            box-sizing: border-box;
          }
          
          label {
            padding: 12px 12px 12px 0;
            display: inline-block;
          }
          
          input[type=submit] {
            background-color: #0000FF;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
          }
          
          input[type=submit]:hover {
            background-color: #4169E1;
          }
          
          .container {
            border-radius: 5px;
            background-color: #f2f2f2;
            padding: 20px;
          }
          </style>
          </head>
          <body>
          <div class="container">
              <h1>Tambah Barang</h1>
              <div class="main">
                  <form method="post" action="tambah.php"
          enctype="multipart/form-data">
                      <div class="input">
                          <label>Nama Barang</label>
                          <input type="text" name="nama" />
                      </div>
                      <div class="input">
                          <label>Kategori</label>
                          <select name="kategori">
                              <option value="Komputer">Komputer</option>
                              <option value="Elektronik">Elektronik</option>
                              <option value="Hand Phone">Hand Phone</option>
                          </select>
                      </div>
                      <div class="input">
                          <label>Harga Jual</label>
                          <input type="text" name="harga_jual" />
                      </div>
                      <div class="input">
                          <label>Harga Beli</label>
                          <input type="text" name="harga_beli" />
                      </div>
                      <div class="input">
                          <label>Stok</label>
                          <input type="text" name="stok" />
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
          </body>
          </html>

![Screenshot 2023-11-25 120221](https://github.com/amandaaaapn/Lab8Web/assets/115678845/71b682b9-112f-45aa-9c53-5900abfd5f81)

# Mengubah Data (Update)

* Buat file baru dengan nama ubah.php

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
            $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok
        = '{$stok}' ";
            if (!empty($gambar))
                $sql .= ", gambar = '{$gambar}' ";
            $sql .= "WHERE id_barang = '{$id}'";
            $result = mysqli_query($conn, $sql);
        if (!$result) {
            die('Error: ' . mysqli_error($conn));
        } else {
            header('location: index.php');
        }
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
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <link href="style.css" rel="stylesheet" type="text/css" />
            <title>Ubah Barang</title>
        <style>
        body {
                    font-family: Arial, sans-serif;
                    background-color: #f4f4f4;
                    margin: 0;
                    padding: 0;
                }
        
        input[type=text], select, textarea {
          width: 100%;
          padding: 8px;
          border: 1px solid #ccc;
          box-sizing: border-box;
        }
        
        label {
          padding: 12px 12px 12px 0;
          display: inline-block;
        }
        
        input[type=submit] {
          background-color: #0000FF;
          color: white;
          padding: 12px 20px;
          border: none;
          border-radius: 4px;
          cursor: pointer;
        }
        
        input[type=submit]:hover {
          background-color: #4169E1;
        }
        
        .container {
          border-radius: 5px;
          background-color: #f2f2f2;
          padding: 20px;
        }
        </style>
        </head>
        <body>
        <div class="container">
            <h1>Ubah Barang</h1>
            <div class="main">
                <form method="post" action="ubah.php"
        enctype="multipart/form-data">
                    <div class="input">
                        <label>Nama Barang</label>
                        <input type="text" name="nama" value="<?php echo
        $data['nama'];?>" />
                    </div>
                    <div class="input">
                        <label>Kategori</label>
                        <select name="kategori">
                            <option <?php echo is_select
        ('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
                            <option <?php echo is_select
        ('Komputer', $data['kategori']);?> value="Elektronik">Elektronik</option>
                            <option <?php echo is_select
        ('Komputer', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
                        </select>
                    </div>
                    <div class="input">
                        <label>Harga Jual</label>
                        <input type="text" name="harga_jual" value="<?php echo
        $data['harga_jual'];?>" />
                    </div>
                    <div class="input">
                        <label>Harga Beli</label>
                        <input type="text" name="harga_beli" value="<?php echo
        $data['harga_beli'];?>" />
                    </div>
                    <div class="input">
                        <label>Stok</label>
                        <input type="text" name="stok" value="<?php echo
        $data['stok'];?>" />
                    </div>
                    <div class="input">
                        <label>File Gambar</label>
                        <input type="file" name="file_gambar" />
                    </div>
                    <div class="submit">
                        <input type="hidden" name="id" value="<?php echo
        $data['id_barang'];?>" />
                        <input type="submit" name="submit" value="Simpan" />
                    </div>
                </form>
            </div>
        </div>
        </body>
        </html>

![Screenshot 2023-11-25 120449](https://github.com/amandaaaapn/Lab8Web/assets/115678845/54ea14b5-50ee-4584-9ff6-54776109b72f)

# Menghapus Data (Delete)

* Buat file baru dengan nama hapus.php

          <?php
          include_once 'koneksi.php';
          $id = $_GET['id'];
          $sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
          $result = mysqli_query($conn, $sql);
          header('location: index.php');
          ?>

# Sekian dan Terima Kasih
