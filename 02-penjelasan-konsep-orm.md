#Penjelasan Konsep ORM

Di bagian teori penulis telah menulis mengenai teori mengenai ORM sehingga penulis menyimpulkan bahwa Object Relational Mapping atau lebih sering disebut ORM adalah sebuah konsep dimana sebuah object merupakan representasi dari basis data yang berbasis relational.

di dalam basis data yang relational kita mengenal adanya tabel seperti dibawah ini.

| Id Barang | Nama Barang | Jenis Barang | Tanggal Kadaluarsa |
|:----------|:------------|:-------------|:------------------:|
|A001       | Rinso       | Cair         | 1 Januari 2016     |
|A002       | Tango       | Padat        | 12 September 2015  |

dengan menggunakan sintak SQL maka querynya adalah sebagai berikut

```sql
create table Barang(
    idBarang varchar(150) not null,
    namaBarang varchar(45),
    jenisBarang varchar(10),
    tanggalKadaluarsa date,
    primary key (idBarang)
)Engine=InnoDB;
```

diatas adalah contoh dengan menggunakan basis data relational, maka berikutnya bagaimana kita menghubungkan dengan pemrograman berorientasi objek. Berikut adalah contoh jika kita membuatnya ke dalam pemrograman berorientasi objek.

```java
public class Barang {
  private String idBarang;
  private String namaBarang;
  private String jenisBarang;
  private String tanggalKadaluarsa;

  //getter setter
}
```

Dapat disimpulkan bahwa sebuah class adalah representasi dari sebuah tabel dan sebuah property atau variabel adanya representasi dari kolom pada basis data. Banyak framework dari berbagai bahasa pemrograman yang telah melakukan implementasi dari konsep ORM ini, diantaranya adalah

- Hibernate (Java)
- Spring Data JPA (Java)
- MyBatis (Java)
- JPA (Java)
- Ebean (Java & Scala)
- Waterline (Node JS / Javascript)
- ActiveRecord Ruby On Rails (Ruby)
- ActiveRecord CodeIgniter (PHP)
- Eloquent ORM Laravel (PHP)
- Gas ORM (PHP)
- dan lain - lain