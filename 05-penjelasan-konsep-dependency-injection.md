#Penjelasan Konsep Dependency Injection

[Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection) merupakan salah satu implementasi dari konsep [Inversion Of Control (IoC)](https://en.wikipedia.org/wiki/Inversion_of_control). Dependency Injection berfungsi agar suatu class tidak terikat dengan class yang lain sehingga dependency injection akan memberikan injeksi kepada class yang membutuhkan dependency. Dependency Injection dapat diimplementasikan dengan menggunakan 3 cara yaitu

* Constructor :
* Getter Setter
* Class Interface

Berikut adalah contoh sederhana untuk memudahkan pemahaman tentang dependency injection. Misalkan penulis mempunyai sebuah class **Mahasiswa** sebagai model seperti berikut.

```java
package model;
 
public class Mahasiswa {
    private String npm;
    private String nama;
    private String asalSekolah;
    private String alamat;
 
    public String getNpm() {
        return npm;
    }
 
    public void setNpm(String npm) {
        this.npm = npm;
    }
 
    public String getNama() {
        return nama;
    }
 
    public void setNama(String nama) {
        this.nama = nama;
    }
 
    public String getAsalSekolah() {
        return asalSekolah;
    }
 
    public void setAsalSekolah(String asalSekolah) {
        this.asalSekolah = asalSekolah;
    }
 
    public String getAlamat() {
        return alamat;
    }
 
    public void setAlamat(String alamat) {
        this.alamat = alamat;
    }
}
```

dan class untuk dao nya seperti berikut.

```java
package dao;
 
import com.mysql.jdbc.jdbc2.optional.MysqlDataSource;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
import model.Mahasiswa;

public class MahasiswaDao {
    MysqlDataSource dataSource;
    Connection connection;
    
    public MahasiswaDao() throws SQLException {
        dataSource=new MysqlDataSource();
        dataSource.setServerName("localhost");
        dataSource.setUser("root");
        dataSource.setPassword("");
        dataSource.setDatabaseName("belajar");
        
        connection=dataSource.getConnection();
    }
    
    public void tambahMahasiswa(Mahasiswa mahasiswa) throws SQLException {
        PreparedStatement ps=connection.prepareStatement("INSERT 
        INTO mahasiswa values(?,?,?,?)");
        ps.setString(1, mahasiswa.getNpm());
        ps.setString(2, mahasiswa.getNama());
        ps.setString(3, mahasiswa.getAsalSekolah());
        ps.setString(4, mahasiswa.getAlamat());
        ps.execute();
        connection.close();
    }
     
}
```

Sekilas dari codingan diatas tidak ada yang salah, karena kodingan telah benar hanya saja kurang elegan, Mengapa demikian ? perhatikan baik - baik pada bagian **constructor** class **MahasiswaDao** disana terdapat konfigurasi database sehingga dia memerlukan dependency **connection**. Jika pada aplikasi berskala besar maka akan terdapat ratusan class **xxxDao** sehingga setiap kali kita membuat class **xxxDao** maka kita diharuskan membuat koneksi ke database dan apabila terjadi perubahan database atau migrasi ke database maka kita diharuskan mengubah seluruh class **xxxDao** sehingga membutuhkan waktu yang lama. Bagaimana cara mengatasinya ? maka kita akan gunakan dependency injection melalui constructor. Jika kita ubah maka akan jadi seperti berikut.

```java
package dao;
 
import com.mysql.jdbc.jdbc2.optional.MysqlDataSource;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;
import model.Mahasiswa;
 
public class MahasiswaDao {
    Connection connection;
    
    public MahasiswaDao(connection) {
        this.connection=connection;
    }
    
    public void tambahMahasiswa(Mahasiswa mahasiswa) throws SQLException {
        PreparedStatement ps=connection.prepareStatement("INSERT INTO mahasiswa values(?,?,?,?)");
        ps.setString(1, mahasiswa.getNpm());
        ps.setString(2, mahasiswa.getNama());
        ps.setString(3, mahasiswa.getAsalSekolah());
        ps.setString(4, mahasiswa.getAlamat());
        ps.execute();
        connection.close();
    }
     
}
```

Setelah dibuat konfigurasi diatas maka class **MahasiswaDao** membutuhkan depent dari class lain yang berupa konfigurasi database/class connection, konfigurasi database/class connection tersebut akan diinject ke class **MahasiswaDao**. Berikut adalah kodingan untuk melakukan inject ke class **MahasiswaDao**.

```java
public class TestMahasiswaDao {
    public static void main(String[] args) {
        Mahasiawa m = new Mahasiswa()
        m.setNpm("58412085");
        m.setNama("Rizki Mufrizal");
        m.setAsalSekolah("MAS JEUMALA AMAL");
        m.setAlamat("Aceh");
 
        MysqlDataSource dataSource = new MysqlDataSource();
        dataSource=new MysqlDataSource();
        dataSource.setServerName("localhost");
        dataSource.setUser("root");
        dataSource.setPassword("");
        dataSource.setDatabaseName("belajar");
        Connection connection = dataSource.getConnection();
 
        MahasiswaDao mahasiswaDao = new MahasiswaDao(connection);
        mahasiswaDao.tambahMahasiswa(m);
    }
}
```

Bisa dilihat dari codingan diatas bahwa kita melakukan inject ke class **MahasiswaDao** dengan **connection** bisa dilihat pada bagian **MahasiswaDao mahasiswaDao = new MahasiswaDao(connection);** sehingga bisa dibilang bahwa kita melakukan injeksi terhadap class **MahasiswaDao** dengan class connection dan class **MahasiswaDao** membutuhkan depent dari class **connection**. Dengan menggunakan dependency injection maka aplikasi akan lebih rapi dan mudah dikonfigurasikan.