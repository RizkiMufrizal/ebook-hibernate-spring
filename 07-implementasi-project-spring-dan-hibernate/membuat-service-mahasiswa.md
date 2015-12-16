##Membuat Service Mahasiswa

Setelah melewati langkah pembuatan class `Dao` selanjutnya adalah membuat class service. Class service ini berfungsi sebagai bisnis proses atau logic dalam aplikasi yang akan kita buat misalnya seperti transaction, cache, hash password, perhitungan dan sebagainya. Ketika kita menggunakan spring dan hibernate maka class service dan class dao akan banyak sekali digunakan, di dalam aplikasi skala enterprise akan ada ratusan class service dan class dao tersebut, tujuannya adalah untuk mempermudah pengembangan aplikasi dan aplikasi terlihat lebih rapi. Silahkan buat sebuah class interface dengan nama `MahasiswaService` seperti berikut ini.

![](../gambar/screenshot20.png)

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

![](../gambar/screenshot21.png)

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