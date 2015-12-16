#Bab 1 : Landasan Teori

##Object Relational Mapping

Object Relational Mapping (ORM) adalah sebuah framework yang dapat menjembatani perbedaan sistem basis data yang bersifat relational dengan paradigma pengembangan aplikasi yang berorientasi objek. Setiap objek yang akan memetakan menjadi tabel-tabel pada basis data relasional dibungkus oleh suatu interface dengan menerapkan konsep design pattern. Hal tersebut bertujuan untuk memudahkan lapisan aplikasi mengakses data tersebut. Object Relational Mapping merupakan teknik otomasi dan transparansi dari object persistence ke dalam tabel pada basis data, menggunakan metadata yang mendeskripsikan pemetaan antara objek dan basis data. ORM berperan dalam lapisan model dalam konsep MVC. Model adalah sebuah lapisan yang paling dekat dengan sumber data, baik itu berasal dari basis data, webservice, maupun file system.

Object Relational Mapping (ORM) juga mengatasi perbedaan sistem basis data yang bersifat relational dengan paradigma pengembangan aplikasi yang berorientasi objek. Selain itu, ORM juga menjembatani dialek SQL yang digunakan, sehingga apapun produk RDBMS yang digunakan tidak berpengaruh terhadap kode program. ORM merupakan solusi yang mengatasi perbedaan aspek-aspek ketidaksesuaian antara konsep pemrograman berorientasi objek dengan konsep basis data relasional.

##Hibernate

Project hibernate dimulai pada tahun 2001 oleh Gavin King, project ini mulai mendapat tanggapan serius setelah Gavin King dipekerjakan oleh Jboss dan Jboss mulai mengerahkan pasukan lebih banyak lagi untuk mengelola Hibernate secara serius. Keberhasilan Hibernate sangat fenomenal, bahkan di satu titik Hibernate justru lebih terkenal dibanding konsep ORM itu sendiri.

Hibernate + Spring benar-benar menohok EJB 2.1 secara telak, sehingga dalam rilis versi berikutnya, EJB 3.0, diperkenalkan konsep JPA yang mengambil ilham dari Hibernate. Sekarang ini Hibernate, bersama iBatis, sudah menjadi pemimpin pasar di backend framework untuk mengkabstraksi JDBC. Semenjak versi 3.5 hibernate dilengkapi dengan Hibernate Annotation dan juga Hibernate secara resmi menjadi salah satu implementasi JPA. Sedangkan JPA sendiri pada dasarnya hanya API yang wujud nyatanya adalah sekumpulan interface seperti halnya JDBC. Implementasi JPA yang dikenal selain Hibernate adalah Toplink.

Annotation dengan Hibernate bisa diimplementasikan dengan tiga cara: menggunaka JPA annotation, menggunakan murni Hibernate Annotation atau mencampur antara keduanya. Bagaimana membedakan hibernate annotation dan JPA annotation? Cukup dilihat import dari annotationya, jika diimport dari javax.persistence berarti JPA annotation, kalau diimport dari org.hibernate.mapping berarti Hibernate annotation.Feature dari Hibernate annotation lebih lengkap dibanding JPA annotation. Pendekatan yang digunakan dalam buku ini adalah secara default menggunakan JPA Annotation, jika ada feature mapping yang tidak ada di dalam JPA annotation, maka baru digunakan Hibernate annotation. Anda tidak perlu bingung harus menggunakan yang mana, karena pada dasarnya implementasi di belakang annotation ini ya Hibernate itu sendiri, jadi menggunakan cara yang manapun
hasilnya sama saja. Secara teknis tidak ada bedanya, hanya masalah pilihan saja.

Project Hibernate mempunyai pengaruh yang sangat besar, selain mempengaruhi EJB dengan dilahirkanya JPA, Hibernate project juga menghasilkan Hibernate Validation yang merupakan cikal bakal Beans Validation yang akhirnya masuk JSR. Selain itu ada project Hibernate Search yang bertujuan untuk membuat full text indexing dari table-table yang dikelola Hibernate, sehingga bisa dilakukan full text search terhadap table tersebut, sangat powerfull. Project berikutnya adalah Hibernate Shards, project ini bertujuan untuk memberikan kemampuan
pemisahan table dalam bebebrapa instance database, alias distributed database.

##Spring Framework

Spring adalah salah satu application framework untuk aplikasi berbasis Java, tepatnya JEE. Spring merupakan sebuah framework (kerangka kerja) yang digunakan untuk membangun sebuah aplikasi Enterprise. Spring termasuk framework yang lightweight (ringan) untuk mendukung secara penuh dalam pengembangan aplikasi Enterprise siap pakai.

Spring adalah Dependency Injection (DI) atau Inversion of Control (IoC). Tugas utama Spring adalah memanage objek - objek yang dibutuhkan dalam aplikasi. Misalnya SessionFactory dan Session adalah objek - objek yang diperlukan untuk bekerja dengan Hibernate, Spring dapat membantu memanage objek - objek ini sehingga kode infransturktur (boiler code) dapat dikurangi secara signifkan karena dihandle oleh Spring.

Kode infrasturktur (boiler plate code) contohnya adalah membuka dan menutup Sesssion, menangani transaction seperti transaction begin, commit dan rollback. Spring akan mengambil alih tanggung jawab untuk memanage kode infrastruktur ini dari tangan developer, hal ini sangat strategis karena developer seringkali lupa untuk menulis kode infrastruktur yang dapat mengakibatkan memory leak atau merusak konsistensi data.

Peranan utama Spring dalam aplikasi cukup besar, salah satu tugas utama Spring adalah memanage Hibernate agar developer tidak perlu secara manual harus membuat kode untuk membuka menutup session (transparent Session management) dan menangani transaction (declarative transaction). Transaction yang ditangani secara manual dengan kode disebut gaya pemrograman Programatic Transaction, sedangkan gaya pemrograman yang menyerahkan penanganan transaction ke framework disebut Declarative Transaction.

Spring dapat digunakan untuk melakukan pengaturan deklarasi manajemen transaksi, remote access dengan menggunakan RMI atau layanan web lainnya, fasilitas mailing, dan beragam opsi untuk pengaturan data ke database. Spring juga memungkinkan kita menggunakan hanya modul-modul tertentu sehingga kita tidak usah menggunakan semua modul Spring dalam aplikasi apabila tidak diperlukan.

Spring mempunyai feature Aspect Oriented Programming (AOP) yang menjadi tulang punggung dibalik implementasi declarative transaction dan transparent Session management. AOP memungkinkan Spring menyisipkan kode untuk memulai transaction kemudian membuka session pada saat sebuah method dalam service akan dieksekusi, kemudian disisipkan pula kode untuk merollback dan menutup session ketika method dalam service muncul exception, dan setelah method selesai dilaksanakan Spring menyisipkan kode untuk mengcommit transaction plus menutup session. Semua proses penyisipan kode ini dilakukan secara runtime dan transparan terhadap developer. Sehingga developer cukup berkonsentrasi untuk mengimplementasikan bussiness logic tanpa harus khawatir lupa mengcommit transaction atau menutup Session.

**Fitur-fitur dari Spring framework :**

1. Transaction Management
  Spring framework menyediakan sebuah layer abstrak yang generik untuk manajemen transaksi, sehingga memudahkan para developer dalam melakukan manajemen transaksi.

2. JDBC Exception Handling
  Layer abstrak JDBC menawarkan exception yang bersifat hierarki sehingga memudahkan penanganan error.

3. Integration with Hibernate, JDO, and iBatis
  Spring menawarkan layanan integrasi terbaik dengan Hibernate, JDO dan iBatas.

4. AOP framework
  Spring merupakan framework AOP Terbaik yang pernah ada.

5. MVC framework
  Spring hadir dengan framework aplikasi web MVC, yang dibangun di atas inti Spring. Spring merupakan framework yang sangat fleksibel dalam pengaturan strategi interface, dan mengakomodasi beberapa teknologi view seperti JSP, Velocity, Tiles, iText, dan POI.

**Arsitektur Spring :**

1. Spring AOP
  Salah satu komponen utama Spring adalah AOP framework, AOP framework digunakan untuk

    * Untuk menyediakan layanan Enterprise, terutama sebagai pengganti EJB. Layanan terpenting dalam layanan            ini adalah untuk mendekralif manajemen transaksi, yang telah disediakan dalam abstraksi Spring  transaction.
    
    * Untuk memungkinkan pengguna dalam menerapkan AOP dalam penggunaan OOP.

2. Spring ORM
  Spring ORM berhubungan dengan akses database dan menyediakan lapisan layer terintegrasi dengan ORM yang populer termasuk JDO, Hibernate dan iBatis.

3. Spring Web
  Merupakan bagian dari modul pengembangan web Spring termasuk Spring Web MVC.

4. Spring DAO
  DAO (Data Access Object) mendukung standarisasi akses data yang menggunakan teknologi seperti JDBC, Hibernate dan JDO.

5. Spring Context
  Paket ini didasari pada paket beans untuk menambah dukungan sumber pesan dan untuk pola desain Observer, dan kemampuan untuk mendapatkan sumber daya yang konsisten dengan menggunakan API.

6. Spring Web MVC
  Menyediakan implementasi MVC untuk aplikasi web.

7. Spring Core
  Paket Spring Core ini merupakan komponen paling penting dari Spring framework. Komponen ini menyediakan fitur Dependency Injection. BeanFactory memisahkan dependency seperti inisialisasi, pembentukan dan akses objek dari logika program anda.

##Apache Maven

Apache maven adalah salah satu build tool yang sangat terkenal. Apache maven berfungsi untuk manajemen dependecy librari sebuah project. Berdasarkan konsep Project Object Model (POM), Maven dapat mengelola membangun sebuah proyek, pelaporan dan dokumentasi dari sepotong pusat informasi.