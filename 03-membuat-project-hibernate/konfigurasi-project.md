##Konfigurasi Project

Karena menggunakan maven maka kita akan lakukan konfigurasi pada maven terlebih dahulu. Silahkan buka file **pom.xml** pada bagian **Project Files** maka akan tampil seperti ini.

![](gambar/screenshot3.png)

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