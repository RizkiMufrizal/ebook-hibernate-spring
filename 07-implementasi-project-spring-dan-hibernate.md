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


