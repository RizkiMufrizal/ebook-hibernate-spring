##Membuat Model Barang

Seperti yang telah kita ketahui bahwa agar aplikasi kita buat lebih terstruktur dan lebih bersih maka kita akan menggunakan pattern MVC (model view controller). Silahkan klik kanan pada project anda, lalu pilih new dan pilih java class, kemudian isikan seperti berikut.

![](../gambar/screenshot4.png)

maka akan dibuatkan sebuah class dengan nama **Barang**, class ini berfungsi sebagai model dimana class ini akan kita mapping ke tabel yang ada di dalam database. Didalam bahasa pemrograman java kita akan menggunakan aturan **camel case** sehingga setiap nama class akan kita buat dengan menggunakan huruf besar sedangkan jika ada dua kata maka huruf pertama untuk kata kedua juga akan dijadikan huruf besar, contohnya adalaha misalnya **makan siang** maka akan kita ubah menjadi **MakanSiang**.

Silahkan ubah kodingan pada class Barang menjadi seperti berikut :

```java
package com.belajar.hibernate.model;

import java.io.Serializable;
import java.util.Date;
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.EnumType;
import javax.persistence.Enumerated;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.Table;
import javax.persistence.Temporal;
import javax.persistence.TemporalType;
import org.hibernate.annotations.GenericGenerator;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 6, 2015
 */
@Entity
@Table(name = "tb_barang")
public class Barang implements Serializable {

    @Id
    @GenericGenerator(name = "uuid2", strategy = "uuid2")
    @GeneratedValue(generator = "uuid2")
    @Column(name = "id_barang", length = 150)
    private String idBarang;

    @Column(name = "nama_barang", length = 50)
    private String namaBarang;

    @Column(name = "jenis_barang", length = 10)
    @Enumerated(EnumType.STRING)
    private JenisBarang jenisBarang;

    @Column(name = "tanggal_kadaluarsa")
    @Temporal(TemporalType.DATE)
    private Date tanggalKadaluarsa;

}
```

maka akan muncul error pada baris **JenisBarang** silahkan anda buat sebuah class dengan nama **JenisBarang** di dalam package **com.belajar.hibernate.model** dan kemudian ubah juga menjadi codingan seperti berikut ini.

```java
package com.belajar.hibernate.model;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 6, 2015
 */
public enum JenisBarang {
    gas, padat, cair
}

```

diatas merupakan sebuah class **enum**, mengapa kita menggunakan class ini ? dikarenakan kita ingin setiap user hanya akan melakukan inputan terhadap column **jenis barang** dengan value **gas**, **cair** dan **padat** sehingga tidak ada user yang akan memasukkan inputan ke column **jenis barang** selain dari tiga kata tadi. Kembali lagi ke class **Barang**, untuk melakukan proses **encapsulasi** maka kita akan menggunakan fitur dari netbeans, silahkan pilih menu **refactor** lalu pilih **encapsulate fields**. Kemudian pilih **select all** lalu refactor maka secara otomatis netbeans akan membuatkan getter setter dari setiap variabel yang telah kita deklarasikan tadi. Getter setter ini berfungsi agar variabel yang terdapat di dalam class **Barang** dapat diakses oleh class yang lain, ini merupakan salah satu implementasi dari **encapsulasi**, variabel di dalal  class **Barang** tidak dapat diakses dikarenakan semua variabel ini menggunakan Access Modifier private sehingga hanya bisa diakses oleh class itu sendiri.

Berikut adalah penjelasan sekilas mengenai kodingan diatas.

- **@Entity** berfungsi mendeklarasikan bahwa class ini merupakan sebuah class entity yang akan di mapping oleh hibernate.
- **@Table** berfungsi untuk mendeklarasikan nama tabel.
- **@Id** berfungsi untuk mendeklarasikan bahwa property tersebut merupakan primary key.
- **@GenericGenerator** berfungsi sebagai generator dari UUID, UUID ini adalah sebuah string yang digenerate secara random sehingga sangat cocok untuk dijadikan sebagai primary key.
- **@GeneratedValue** berfungsi untuk memasukkan string UUID ke dalam variabel **idBarang**
- **@Column** berfungsi untuk mendeklarasikan definisi dari sebuah kolom. di dalam **@Column** terdapat **name** yang berfungsi sebagai nama column yang akan dibuat di dalam database, sedangkan **length** berfungsi sebagai panjang dari column tersebut.
- **@Enumerated** berfungsi untuk mendeklarasikan bahwa field tersebut adalah berisi value yang hanya dapat dipilih.
- **@Temporal** berfungsi untuk mendeklarasikan tanggal.