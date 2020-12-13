## Conflicts Pada Github

***

Version Control System adalah tentang mengelola kontribusi antara beberapa Developer yang terdistribusi. Terkadang beberapa Developer mungkin mencoba mengedit konten yang sama. Jika Developer A mencoba untuk mengedit kode yang Developer B sedang edit, `conflict` mungkin terjadi. Untuk meringankan terjadinya `conflict`, Developer akan bekerja di `branch` terpisah yang terpisah . `git merge` bertanggung jawab untuk menggabungkan `branch` terpisah dan menyelesaikan setiap `conflict`.

### Tentang `merge conflicts`

`merge` dan `conflict` adalah bagian umum dari pengalaman Git. `conflict` di alat kontrol versi lain seperti SVN bisa jadi mahal dan memakan waktu. Git membuat `merge` menjadi sangat mudah. Sering kali, Git akan mencari cara untuk mengintegrasikan perubahan baru secara otomatis.

`conflict` umumnya muncul ketika dua orang mengubah baris yang sama dalam sebuah file, atau jika satu Developer menghapus file sementara Developer lain memodifikasinya. Dalam kasus ini, Git tidak dapat secara otomatis menentukan apa yang benar. `conflict` hanya memengaruhi Developer yang melakukan `merge`, anggota tim lainnya tidak menyadari `conflict` tersebut. Git akan menandai file sebagai `conflict` dan menghentikan proses `merge`. Ini kemudian menjadi tanggung jawab Developer untuk menyelesaikan `conflict`.

### Jenis  `merge conflicts`

`merge` dapat memasuki status `conflict` di dua titik terpisah. Saat memulai dan selama proses `merge`. Berikut ini adalah pembahasan tentang bagaimana menangani masing-masing skenario `conflict` tersebut.

#### Git gagal memulai `merge`

`merge` akan gagal dimulai ketika Git melihat ada perubahan baik di direktori kerja atau area staging dari proyek saat ini. Git gagal memulai `merge` karena perubahan yang menunggu keputusan ini dapat ditimpa oleh `commit` yang digabungkan. Jika hal ini terjadi, bukan karena `conflict` dengan Developer lain, tetapi `conflict` dengan perubahan lokal yang tertunda. Keadaan lokal akan perlu distabilkan menggunakan `git stash`, `git checkout`, `git commit` atau `git reset`. Kegagalan `merge` saat mulai akan menampilkan pesan kesalahan berikut:

`error: Entry '<fileName>' not uptodate. Cannot merge. (Changes in working directory)`

#### Git gagal selama `merge`

Kegagalan selama `merge` menunjukkan `conflict` antara `branch` lokal saat ini dan `branch` yang digabungkan. Ini menunjukkan `conflict` dengan kode Developer lain. Git akan melakukan yang terbaik untuk menggabungkan file tetapi akan membiarkan hal-hal yang Anda selesaikan secara manual di file yang mengalami `conflict`. Kegagalan selama `merge` akan menampilkan pesan kesalahan berikut:

`error: Entry '<fileName>' would be overwritten by merge. Cannot merge. (Changes in staging area)`

### Simulasi `merge conflict`

Untuk memahami `merge conflict`, lebih baik mensimulasikan `conflict` untuk diperiksa dan diselesaikan.

#### Membuat Repository  `merge conflict`

- Buat direktori baru dengan nama merge-conflict, masuk kedalam direktori tersebut, dan inisialisasi sebagai repositori Git baru.
  ```
  $ mkdir merge-conflict
  $ cd merge-conflict
  $ git init .
  ```
- Buat file teks baru `README.md` dengan beberapa konten di dalamnya. Tambahkan `README.md`ke repositori dan lakukan `commit`.
  ```
  $ mkdir merge-conflict
  $ cd merge-conflict
  $ git init .
  $ touch README.md //dapat mengisi konten apa saja didalam file
  $ git add README.md
  $ git commit -m "initial content"
  [master (root-commit) bcdbedf] initial content
  1 file changed, 1 insertion(+)
  create mode 100644 README.md
  ```
- Sebagai contoh, di [LINK](https://github.com/dhany007/merge-conflict.git) berikut adalah contoh repository yang berhasil di `commit`
  
Sekarang kita memiliki repositori baru dengan satu cabang master dan file `README.md` dengan konten di dalamnya. Selanjutnya, kita akan membuat cabang baru untuk digunakan sebagai penggabungan yang berkonflik.



- Buat dan `checkout` `branch` baru bernama new_branch_to_merge_later
  ```
  $ git checkout -b new_branch_to_merge_later
  ```
- Edit dan timpa konten di `README.md`,
  ```
  // edit file README.md
  ``` 
- `commit` konten baru.
  ```
  $ git add README.md
  $ git commit -m "edited the content of README.md to cause a conflict"
  [new_branch_to_merge_later 1841eea] edited the content of  to cause a conflict
  1 file changed, 1 insertion(+), 1 deletion(-)
  ```
Dengan cabang baru ini: new_branch_to_merge_later, kita telah membuat `commit` yang menimpa konten`README.md`


Switched to branch 'master'
echo "content to append" >> `README.md`
git commit -am"appended content to `README.md`"
[master 24fbe3c] appended content to merge.tx
1 file changed, 1 insertion(+)

- `checkout` ke `branch` master
  ```
  $ git checkout master
  Switched to branch 'master'
  Your branch is up to date with 'origin/master'.
  ```
- Tambahkan konten ke `README.md`, dan `commit`. 
  ```
  // edit file README.md
  $ git add README.md
  $ git commit -m "tambahan konten"
  [master 09198e3] tambahan konten
  1 file changed, 1 insertion(+), 1 deletion(-)
  ```

Repository kita dalam keadaan di mana kita memiliki 2 komit baru. Satu di `branch` master dan satu lagi di `branch` new_branch_to_merge_later. Pada saat ini mari `git merge new_branch_to_merge_later` dan lihat apa yang terjadi!
```
  $ git merge new_branch_to_merge_later
  Auto-merging README.md
  CONFLICT (content): Merge conflict in README.md
  Automatic merge failed; fix conflicts and then commit the result.
```
Konflik muncul.

#### Msengidentifikasi `merge conflict`
Seperti yang kita alami dari contoh diatas, Git akan menghasilkan beberapa keluaran deskriptif yang memberitahu kita bahwa `conflict` telah terjadi. Kita bisa mendapatkan wawasan lebih jauh dengan menjalankan perintah `git status`
```
  $ git status
  On branch master
  Your branch is ahead of 'origin/master' by 1 commit.
    (use "git push" to publish your local commits)

  You have unmerged paths.
    (fix conflicts and run "git commit")
    (use "git merge --abort" to abort the merge)

  Unmerged paths:
    (use "git add <file>..." to mark resolution)
    both modified:   README.md

  no changes added to commit (use "git add" and/or "git commit -a")
```
Output dari `git status` menunjukkan bahwa ada jalur yang tidak digabungkan karena `conflict`. File README.md sekarang muncul dalam keadaan dimodifikasi. Mari kita periksa file tersebut dan lihat apa yang dimodifikasi.
```
  $ cat README.md
  <<<<<<< HEAD
  Hallo Semuanya, ini adalah konten baru
  =======
  Hallo Semuanya, ini akan terjadi conflict
  >>>>>>> new_branch_to_merge_later

```

Di sini kami telah menggunakan perintah `cat` untuk mengeluarkan konten file README.md. Kami dapat melihat beberapa tambahan baru yang aneh

Baris baru tersebut disebut sebagai `conflict dividers`. Baris `=======` adalah "pusat" dari konflik. Semua konten antara pusat dan baris `<<<<<<< HEAD` adalah konten yang ada di master `branch` saat ini. Atau semua konten antara pusat dan `>>>>>>> new_branch_to_merge_later` konten yang ada di `merging branch`.

#### Cara menyelesaikan `merge conflicts` menggunakan `command line`
Cara paling langsung untuk menyelesaikan `merge conflicts` dengan mengedit file `conflicts`. Buka merge.txtfile di editor favorit Anda. Sebagai contoh, ini adalah contoh hasil file yang telah di-edit:

```
  Kita akan menghilangkan conflict ini.
  keep learn, sleep well, eat well.
```
s
Setelah file diedit, gunakan `git add README.md` . Untuk menyelesaikan `merge`, lakukan `commit` baru

```
  $ git commit -m "resolve conflict"
  [master e88093e] resolve conflict
```

Git akan melihat bahwa konflik telah diselesaikan dan membuat `merge commit` baru untuk menyelesaikan `merge`.

```
  $ git merge new_branch_to_merge_later
  Already up to date.
```

### Kesimpulan
`merge conflicts` bisa menjadi pengalaman yang ditakuti. Untungnya, Git menawarkan alat yang lebih baik untuk membantu menavigasi dan menyelesaikan `conflict`. Git dapat menangani sebagian besar penggabungan sendiri dengan fitur penggabungan otomatis. `conflict` muncul ketika dua cabang terpisah telah melakukan pengeditan pada baris yang sama dalam sebuah file, atau ketika sebuah file telah dihapus di satu cabang tetapi diedit di cabang lainnya. `conflict` kemungkinan besar akan terjadi saat bekerja di lingkungan tim.

Ada banyak alat untuk membantu menyelesaikan `merge conflicts`. Git memiliki banyak alat baris perintah yang digunakan yaitu `git log`, `git reset`, `git status`, `git checkout`, dan `git reset`. Selain Git, banyak alat pihak ketiga menawarkan fitur dukungan `merge conflicts` yang disederhanakan.

SUMBER : 
- [Dokumentasi GitHUB](https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/about-merge-conflicts)
- [Atlassian](https://www.atlassian.com/git/tutorials/using-branches/merge-strategy)
- [Repository](https://github.com/dhany007/merge-conflict) 