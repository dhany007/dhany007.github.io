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

#### Hampir Setiap Operasi adalah Lokal
Sebagian besar operasi di Git hanya membutuhkan file dan sumber daya lokal untuk beroperasi - umumnya tidak diperlukan informasi dari komputer lain di dalam jaringan.

#### Git Memiliki Integritas
Semua didalam Git telah dilakukan checksum[^3] sebelum itu disimpan dan kemudian mengacu pada checksum tersebut. Ini berarti bahwa tidak mungkin untuk mengubah isi dari berkas atau direktori tanpa diketahui oleh Git. 

#### Git Umumnya Hanya Menambah Data
Ketika melakukan aksi didalam Git, hampir semuanya hanya menambahkan data ke basis data Git.

#### Git Memiliki Tiga Keadaan
Git memiliki tiga keadaan utama: committed, modified, dan staged. 
- Committed berarti datanya telah tersimpan dengan aman pada basis data lokal. 
- Modified berarti berkas telah diubah, namun belum di-commit ke basis data. 
- Staged berarti telah menandai berkas yang telah diubah ke dalam versi sekarang untuk snapshot commit selanjutnya.

Directory Git adalah di mana Git menyimpan metadata dan basis data obyek untuk proyek. Ini adalah bagian paling penting tentang Git, dan ini adalah apa yang disalin ketika menggandakan sebuah repository dari komputer lain.

Working directory adalah sebuah checkout tunggal dari satu versi milik proyek. Berkas-berkas ini ditarik dari basis data yang telah dimampatkan dalam direktori Git dan ditempatkan pada penyimpanan untuk digunakan atau disunting.

Staging area adalah sebuah berkas, umumnya berada pada direktori Git, yang menyimpan informasi tentang apa yang akan menjadi commit selanjutnya. Terkadang disebut juga sebagai index, namun juga sering disebut sebagai staging area.

Alur kerja dasar Git adalah seperti berikut:
1. Mengubah berkas dalam working directory.
2. Menyiapkan berkasnya, menambah snapshot ke staging area.
3. Melakukan commit, yang mengambil berkas-berkas yang ada pada staging area dan menyimpan snapshot tersebut secara tetap ke dalam direktori Git.

#### Memulai Git
Untuk memulai dan menginstall git, dapat dilihat di [Dokumentasi](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) Git


### GitHub
GitHub adalah penyimpanan terbesar tunggal untuk repositori Git, dan Github adalah titik pusat kolaborasi untuk jutaan pengembang dan proyek. Sebagian besar dari semua repositori Git di simpan di GitHub, dan banyak proyek open-source menggunakan Github untuk menyimpan Git, pelacakan masalah, tinjauan kode, dan hal-hal lainnya.

Untuk menggunakan Github secara efektif dapat membaca [Dokumentasi](https://git-scm.com/book/en/v2/GitHub-Account-Setup-and-Configuration) yang telah disediakan Git

### Kesimpulan
Untuk menyimpulkan perbedaan antara git vs GitHub: 
- Git adalah perangkat lunak VCS lokal yang memungkinkan pengembang untuk menyimpan snapshot proyek mereka dari waktu ke waktu. Biasanya paling baik untuk penggunaan individu. 
- GitHub adalah platform berbasis web yang menggabungkan fitur kontrol versi git sehingga dapat digunakan secara kolaboratif. Ini juga mencakup fitur manajemen proyek dan tim, serta peluang untuk jaringan dan pengkodean sosial.

Sumber:
 - [Dokumentasi Git](https://git-scm.com/)
 - [geeksforgeeks](https://www.geeksforgeeks.org/version-control-systems/?ref=lbp)


[^1]: Tempat di mana barang-barang disimpan dan dapat ditemukan. [Sumber](https://dictionary.cambridge.org/dictionary/english/repository) 
[^2]: Metode dan struktur data yang digunakan sistem operasi untuk melacak file pada disk. [Sumber](https://tldp.org/LDP/sag/html/filesystems.html) 
[^3]: Nilai yang digunakan untuk memverifikasi integritas file atau transfer data. [Sumber](https://techterms.com/definition/checksum)
