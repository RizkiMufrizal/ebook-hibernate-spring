# Implementasi Project Spring Dan Hibernate

Setelah melewati tahap pembuatan project, selanjutnya kita akan mulai melakukan coding dengan hibernate dan spring. Pada bab ini kita akan membuat sebuah aplikasi untuk data mahasiswa.

##Membuat Model Mahasiswa

Sama seperti project sebelumnya kita akan mulai terlebih dahulu untuk membuat class `model`. Silahkan buat sebuah class dengan nama `Mahasiswa` seperti berikut.

![](gambar/screenshot17.png)

Setelah selesai lalu masukkan codingan seperti berikut ini.

```java
package com.belajar.springHibernate.model;

import java.io.Serializable;
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Table;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 15, 2015
 */

@Entity
@Table(name = "tb_mahasiswa")
public class Mahasiswa implements Serializable{

    @Id
    @Column(name = "npm", length = 8)
    private String npm;
    
    @Column(name = "nama", length = 50)
    private String nama;
    
    @Column(name = "kelas", length = 10)
    private String kelas;
    
    @Column(name = "alamat", length = 150)
    private String alamat;

    /**
     * @return the npm
     */
    public String getNpm() {
        return npm;
    }

    /**
     * @param npm the npm to set
     */
    public void setNpm(String npm) {
        this.npm = npm;
    }

    /**
     * @return the nama
     */
    public String getNama() {
        return nama;
    }

    /**
     * @param nama the nama to set
     */
    public void setNama(String nama) {
        this.nama = nama;
    }

    /**
     * @return the kelas
     */
    public String getKelas() {
        return kelas;
    }

    /**
     * @param kelas the kelas to set
     */
    public void setKelas(String kelas) {
        this.kelas = kelas;
    }

    /**
     * @return the alamat
     */
    public String getAlamat() {
        return alamat;
    }

    /**
     * @param alamat the alamat to set
     */
    public void setAlamat(String alamat) {
        this.alamat = alamat;
    }
    
}

```

Pada class diatas terdapat 4 variabel dimana variabel ini akan berfungsi sebagai column yang terdapat didalam database. Penjelasan untuk annotation silahkan anda baca kembali pada bab implementasi project hibernate.

##Membuat Dao Mahasiswa

Setelah membuat class `model mahasiswa` langkah selanjutnya adalah membuat class `dao` untuk mahasiswa, class ini berfungsi sebagai class yang akan melakukan akses `query` ke database. Silahkan buat sebuah class interface dengan nama `MahasiswaDao` seperti berikut ini.

![](gambar/screenshot18.png)

kemudian ubah kodingan tersebut seperti berikut ini.

```java
package com.belajar.springHibernate.dao;

import com.belajar.springHibernate.model.Mahasiswa;
import java.util.List;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 15, 2015
 */
public interface MahasiswaDao {

    public void save(Mahasiswa mahasiswa);

    public void update(Mahasiswa mahasiswa);

    public void delete(Mahasiswa mahasiswa);

    public Mahasiswa getMahasiswa(String npm);

    public List<Mahasiswa> getMahasiswas();
}
```

Setelah membuat class interface selanjutnya kita ingin melakukan implementasi terhadap class dao tersebut, silahkan buat sebuah class java dengan nama `MahasiswaDaoImpl` seperti berikut ini.

![](gambar/screenshot19.png)

kemudian ubah kodingannya menjadi seperti berikut ini.

```java
package com.belajar.springHibernate.dao;

import com.belajar.springHibernate.model.Mahasiswa;
import java.util.List;
import org.hibernate.SessionFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 15, 2015
 */
@Repository
public class MahasiswaDaoImpl implements MahasiswaDao {

    @Autowired
    private SessionFactory sessionFactory;

    @Override
    public void save(Mahasiswa mahasiswa) {
        sessionFactory.getCurrentSession().save(mahasiswa);
    }

    @Override
    public void update(Mahasiswa mahasiswa) {
        sessionFactory.getCurrentSession().update(mahasiswa);
    }

    @Override
    public void delete(Mahasiswa mahasiswa) {
        sessionFactory.getCurrentSession().delete(mahasiswa);
    }

    @Override
    public Mahasiswa getMahasiswa(String npm) {
        return sessionFactory.getCurrentSession().get(Mahasiswa.class, npm);
    }

    @Override
    public List<Mahasiswa> getMahasiswas() {
        return sessionFactory.getCurrentSession().createCriteria(Mahasiswa.class).list();
    }

}
```

Dapat dilihat terdapat perbedaan yang sangat signifikan ketika kita hanya menggunakan hibernate dan ketika kita menggunakan hibernate dan spring. Bisa dilihat pada class `MahasiswaDaoImpl` kita menggunakan annotation spring yaitu `@Repository` artinya class ini akan dimanage oleh spring dan juga dengan menggunakan annotation menandakan bahwa class ini merupakan sebuah class `dao`.

Pada baris selanjutnya terdapat annotation `@Autowired`, annotation ini merupakan berasal dari class spring yang berfungsi untuk melakukan injection, pada bab penjelasan konsep dependency injection dijelaskan jika secara manual kita membutuhkan beberapa konfigurasi, jika menggunakan spring kita hanya perlu menggunakan annotation `@Autowired` sehingga spring akan menanage object `SessionFactory`, bisa dilihat bahwa sebelum kita menggunakan spring, kita diharuskan membuat constructor agar object `SessionFactory` bisa diinject. Setelah menggunakan spring maka kita tidak lagi melakukan inject secara manual akan tetapi cukup deklarasikan annotation `@Repository` dan gunakan annotation `@Autowired` untuk object yang akan dilakukan injecti biasanya object tersebut berasal dari class interface contohnya adalah class `SessionFactory` merupakan class interface.

##Membuat Service Mahasiswa

Setelah melewati langkah pembuatan class `Dao` selanjutnya adalah membuat class service. Class service ini berfungsi sebagai bisnis proses atau logic dalam aplikasi yang akan kita buat misalnya seperti transaction, cache, hash password, perhitungan dan sebagainya. Ketika kita menggunakan spring dan hibernate maka class service dan class dao akan banyak sekali digunakan, di dalam aplikasi skala enterprise akan ada ratusan class service dan class dao tersebut, tujuannya adalah untuk mempermudah pengembangan aplikasi dan aplikasi terlihat lebih rapi. Silahkan buat sebuah class interface dengan nama `MahasiswaService` seperti berikut ini.

![](gambar/screenshot20.png)

kemudian masukkan codingan seperti berikut ini.

```java
package com.belajar.springHibernate.service;

import com.belajar.springHibernate.model.Mahasiswa;
import java.util.List;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 15, 2015
 */
public interface MahasiswaService {

    public void save(Mahasiswa mahasiswa);

    public void update(Mahasiswa mahasiswa);

    public void delete(Mahasiswa mahasiswa);

    public Mahasiswa getMahasiswa(String npm);

    public List<Mahasiswa> getMahasiswas();
}
```

Sama seperti class `dao` kita akan membuat class lagi untuk melakukan implementasi class `MahasiswaService`, silahkan buat sebuah class dengan nama `MahasiswaServiceImpl` seperti berikut.

![](gambar/screenshot21.png)

kemudian ubah codingan menjadi seperti berikut.

```java
package com.belajar.springHibernate.service;

import com.belajar.springHibernate.dao.MahasiswaDao;
import com.belajar.springHibernate.model.Mahasiswa;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

/**
 * @Author Rizki Mufrizal
 * @Since Dec 15, 2015
 */
@Service("MahasiswaService")
@Transactional(readOnly = true)
public class MahasiswaServiceImpl implements MahasiswaService {

    @Autowired
    private MahasiswaDao mahasiswaDao;

    @Transactional
    @Override
    public void save(Mahasiswa mahasiswa) {
        mahasiswaDao.save(mahasiswa);
    }

    @Transactional
    @Override
    public void update(Mahasiswa mahasiswa) {
        mahasiswaDao.update(mahasiswa);
    }

    @Transactional
    @Override
    public void delete(Mahasiswa mahasiswa) {
        mahasiswaDao.delete(mahasiswa);
    }

    @Override
    public Mahasiswa getMahasiswa(String npm) {
        return mahasiswaDao.getMahasiswa(npm);
    }

    @Override
    public List<Mahasiswa> getMahasiswas() {
        return mahasiswaDao.getMahasiswas();
    }

}
```

Pada class ini kita menggunakan annotation `@Service` menandakan bahwa ini adalah class service, di dalam annotation `@Service` terdapat nama `MahasiswaService` tujuannya adalah nama ini akan digunakan sebagai sebuah bean dimana bean ini nantikan akan diinject ke kelas yang membutuhkannya.

Annotation `@Transactional` kita gunakan sebagai transaction management, berbeda sekali dengan class `dao` tanpa spring, kita diharuskan membuat transaction dan try catch secara manual. Dengan menggunakan spring maka transaction akan dihandle oleh spring dengan menggunakan annotation `@Transactional`, setiap method yang akan dieksekusi secara otomatis spring akan melakukan transaction atau sering disebut dengan `Declarative Transaction`. Untuk membuat `Declarative Transaction` maka spring menggunakan konsep `AOP (aspect oriented programming)`.

Annotation `@Transactional` pada bagian class terdapat perintah `readOnly = true` berfungsi untuk method yang tidak melakukan manipulasi data seperti method `getMahasiswa` dan `getMahasiswas` sedangkan untuk method `save`, `update` dan `delete` kita hanya menggunakan annotation `@Transactional` karena secara default annotation `@Transactional` dikhususkan untuk method yang melakukan query sehingga default perintahnya adalah `readOnly = false`.