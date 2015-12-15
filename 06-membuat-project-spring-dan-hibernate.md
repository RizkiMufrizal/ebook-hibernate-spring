# Membuat Project Spring Dan Hibernate

Pada bagian ini kita akan membuat dan malakukan konfigurasi project dengan menggunakan framework spring dan hibernate. Apa perbedaan antara spring dan hibernate ? apakah spring dan hibernate dapat digabung menjadi sebuah project ?

Hibernate adalah framework yang berbasis ORM sehingga hibernate akan mengurus semua masalah yang bersangkutan dengan basis data atau database sedangkan spring adalah framework yang berbasis dependency injection sehingga memudahkan dalam melakukan manajemen terhadap sebuah object. Spring dan hibernate merupakan dua framework yang memiliki konsep yang berbeda akan tetapi kedua framework ini dapat digabungkan karena salah satu dari mereka membutuhkan framework yang lain. Jika kita menggunakan framework hibernate tanpa menggunakan framework spring ibaratnya seperti kita makan nasi tanpa lauk, mengapa demikian ? karena dengan menggunakan spring maka project yang akan dibangun semakin baik, rapi, dan salah satu keunggulannya adalah konsep AOP sehingga mempermudah transaction management. Mungkin agak sedikit bingung tentang penjelasan AOP, nanti akan dibahas pada bagian implementasi project spring dan hibernate.

##Membuat Project

Sama seperti sebelumnya klik menu `new project` lalu pada bagian categories pilih `maven` dan pada bagian project pilih `java application`. Berikut adalah gambar konfigurasinya

![](gambar/screenshot16.png)

