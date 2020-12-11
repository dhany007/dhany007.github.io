## Git dan Github

***

### Tentang Version Control
Version control adalah sebuah sistem yang merekam perubahan-perubahan dari sebuah berkas atau sekumpulan berkas dari waktu ke waktu sehingga  dapat menilik kembali versi khusus suatu saat nanti.

Version Control System (VCS) memperbolehkan untuk mengembalikan berkas-berkas ke keadaan sebelumnya, mengembalikan seluruh proyek kembali ke keadaan sebelumnya, membandingkan perubahan-perubahan di setiap waktu, melihat siapa yang terakhir mengubah sesuatu yang mungkin menimbulkan masalah, siapa dan kapan yang mengenalkan sebuah isu dan banyak lagi.

Tipe Version Control Systems:

- Local Version Control Systems

  Metode version control yang banyak dipilih oleh orang-orang dengan cara menyalin berkas-berkas ke direktori lain. Pendekatan ini sangat umum karena ini sangat sederhana, namun ini juga sangat rentan terkena kesalahan. Mudah sekali untuk lupa pada direktori mana berada dan menulis ke berkas yang salah atau menyalin setiap berkas yang tidak sengaja.

- Centralized Version Control Systems

  Metode version control ini membuat kolaborasi antara pengembang. Setiap orang tahu hingga pada tahapan apa yang orang lain sedang kerjakan di dalam proyek. Ini memungkinkan administrator untuk mengontrol siapa yang dapat melakukan apa.

  Kelemahan dari metode ini adalah jika kegagalan yang diwakili oleh repositori terpusat, kolaborasi dan menyimpan perubahan tidak dapat dilakukan. Jika tempat penyimpanan pusat menjadi rusak, dan cadangan yang memadai belum tersimpan, maka memiliki resiko untuk kehilangan semuanya.

- Distributed Version Control Systems
  
  Sistem kontrol versi terdistribusi berisi banyak repositori[^1]. Setiap pengembang memiliki repositori dan salinan pekerjaan mereka sendiri. jika ada salah satu server yang mati, dan sistem-sistem ini bekerja bersama melalui server itu, setiap repository milik pengembang dapat disalin kembali ke server untuk memulihkannya.

### Git

Git adalah sistem kontrol versi terdistribusi gratis dan open source yang dirancang untuk menangani semuanya mulai dari proyek kecil hingga sangat besar dengan kecepatan dan efisiensi.

#### 'Snapshots', Bukan 'setiap perubahan'
Perbedaan besar antara Git dan VCS lainnya (Subversion dan sejenisnya) adalah tentang cara Git berpikir tentang datanya. Sistem lain menyimpan informasi sebagai sebuah daftar dari perubahan-perubahan yang dibuat kepada tiap berkas sepanjang waktu.

Git menyimpan datanya lebih seperti sekumpulan snapshot dari sebuah miniatur filesystem[^2]. Setiap kali menyimpan keadaan dari proyek di Git, pada dasarnya itu mengambil sebuah gambar tentang bagaimana tampilan semua berkas pada saat itu dan menyimpan acuan kepada snapshot tersebut.

[^1]: https://dictionary.cambridge.org/dictionary/english/repository
[^2]: https://tldp.org/LDP/sag/html/filesystems.html

Sumber:
 - https://git-scm.com/
 - https://www.geeksforgeeks.org/version-control-systems/?ref=lbp