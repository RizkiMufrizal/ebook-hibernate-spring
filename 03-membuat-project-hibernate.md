# Membuat Project Hibernate

Pada bab ini kita akan belajar bagaimana membuat sebuah project dengan menggunakan [Netbeans](https://netbeans.org/). Netbeans adalah salah satu IDE (integrated development environment) yang digunakan oleh programmer java, selain netbeans juga terdapat IDE yang lain seperti [InteliJ IDEA](https://www.jetbrains.com/idea/) dan [Eclipse](https://eclipse.org/). Project yang akan kita buat adalah project berbasis maven, mengapa berbasis maven ? dikarenakan kita membutuhkan dependency library yang akan digunakan oleh project yang akan kita buat. Selain sebagai dependency management, maven juga berfungsi sebagai build tool dimana maven dapat melakukan compile terhadap aplikasi yang kita buat.

##Membuat Project

Berikut adalah tahapan untuk membuat project hibernate dengan menggunakan netbeans.

* Buka netbeans anda kemudian pilih menu **new project**, pada bagian categories pilih **maven**, dan pada bagian project pilih **java application** seperti berikut.

![](gambar/screenshot-from-2015-12-06-16:57:52.png)

* Klik next, pada bagian project name isikan dengan **BelajarHibernate**.
* Pada bagian **Group ID** isikan dengan **com.belajar.hibernate**, Group ID ini berfungsi sebagai penamaan sebuah perusahaan atau organisasi yang membuat aplikasi.
* Pada bagian version biarkan saja dikarenakan aplikasi yang kita bangun masih tahap development maka versionnya default akan menjadi **1.0-SNAPSHOT**.
* Pada bagian **package** isikan dengan **com.belajar.hibernate** yang berfungsi sebagai nama package dari aplikasi yang akan kita buat nanti, lalu klik finish. Berikut adalah contoh pembuatan projectnya.

![](gambar/screenshot-from-2015-12-06-16:57:59.png)

##Konfigurasi Project

Karena menggunakan maven maka kita akan lakukan konfigurasi pada maven terlebih dahulu. Silahkan buka file **pom.xml** pada bagian **Project Files** maka akan tampil seperti ini.

![](gambar/Screenshot-from-2015-12-06-17:17:22.png)

untuk mengatur dependency pada project hibernate, maka ubah kodingan pada **pom.xml** seperti berikut.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="
  http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="
  http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.belajar.hibernate</groupId>
    <artifactId>BelajarHibernate</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>5.0.4.Final</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>5.0.4.Final</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.37</version>
        </dependency>
    </dependencies>

</project>
```

diatas merupakan konfigurasi dari maven, karena disini kita menggunakan hibernate maka kita masukkan dependency yang dibutuhkan oleh aplikasi kita diantaranya adalah **hibernate-core**, **hibernate-entitymanager** dan **mysql-connector-java** sebagai database yang akan kita gunakan.