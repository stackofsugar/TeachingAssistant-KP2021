[<< Silabus](../silabus.md)

# 9.1 - Pengantar File Processing

Program pada komputer tidak dapat dipisahkan dari file untuk mendukung keberjalanannya. Sebagai contoh, jika anda sedang memainkan suatu video game, pasti terdapat fitur untuk menyimpan dan melanjutkan progress game yang telah kalian jalankan. Atau contoh yang lain adalah ketika anda menyimpan setting/konfigurasi suatu program ke dalam file kemudian memuatnya lagi. Hal-hal seperti itu diimplementasikan dengan **File Processing** atau **File Handling** dalam pemrograman.

File dalam komputer terbagi menjadi dua jenis utama, yaitu: **plaintext** (sequential-access) dan **binary** (random-access). File berjenis plaintext umumnya dapat dibaca dengan jelas menggunakan aplikasi text editor seperti notepad atau yang lainnya. Kemudian file berjenis binary umumnya hanya dapat dibaca oleh program tertentu yang mengenali dan menggunakannya saja.

Seluruh operasi yang melibatkan file dalam pemrograman C berada dalam header **stdio.h**.

## File Structure

Dalam pemrograman C, suatu file yang sedang dibuka dapat direpresentasikan sebagai tipe data `FILE *` (pointer to FILE structure). Dan berikut adalah definisi dari FILE sendiri:
```c
typedef struct {
    /* Berisi member internal yang terdefinisi sendiri oleh compiler */
} FILE; /* Menggunakan type aliasing */
```

Tipe data tersebut sebenarnya merupakan suatu struct yang detail implementasinya bergantung pada jenis compiler yang digunakan. Untuk itu, anda tidak perlu mengetahui tiap-tiap membernya yang terdapat dalam struct tersebut.

## Membuka dan Menutup File

Saat membuka file dalam program, akan kita gunakan fungsi **fopen()** yang terdapat pada header `stdio.h`. Berikut adalah deklarasinya:
```c
FILE *fopen(const char *filename, const char *mode);
```

Pemanggilan fungsi akan menghasilkan (return) pointer obyek yang merepresentasikan suatu file (`FILE *`) bergantung pada `mode` yang dimasukkan (namun akan me-return `NULL` apabila terdapat error karena lokasi file tidak dapat diakses). Argumen yang harus dimasukkan ada dua, yaitu:

1. `filename` : String yang berisi path absolut/relatif kepada file yang dituju
2. `mode` : String yang memberikan keterangan tentang bagaimana file akan diakses. Lihat di bawah untuk berbagai kemungkinan opsinya

|Mode (Plaintext)|Mode (Binary)|Deskripsi|Jika lokasi file di komputer sudah ada|Jika lokasi file di komputer belum ada|
|--|--|--|--|--|
|r|rb|File dibuka hanya untuk dibaca saja (read-only)|return pointer obyek file tersebut|return `NULL`|
|w|wb|File dibuka hanya untuk ditulis saja (write-only)|file akan ter-replace dan return pointer obyek file yang baru|file dibuat secara otomatis dan return pointer obyek file tersebut|
|a|ab|File dibuka hanya untuk ditulis saja pada bagian akhir file (append-only)|return pointer obyek file tersebut|file dibuat secara otomatis dan return pointer obyek file tersebut|
|r+|rb+|File dibuka untuk dibaca dan ditulis (read/write)|return pointer obyek file tersebut|return `NULL`|
|w+|wb+|File dibuka untuk dibaca dan ditulis (read/write)|file akan ter-replace dan return pointer obyek file yang baru|file akan dibuat secara otomatis dan return pointer obyek file tersebut|
|a+|ab+|File dibuka untuk dibaca (seluruh bagian file) dan ditulis (hanya pada bagian akhir file)|return pointer obyek file tersebut|file dibuat secara otomatis dan return pointer obyek file tersebut

Jika file sudah selesai digunakan, kita dapat menyimpan semua data yang sudah ditulis dan menutup file tersebut menggunakan fungsi **fclose()**. Berikut adalah deklarasinya:
```c
int fclose(FILE *stream);
```
Fungsi di atas menyimpan dan menutup obyek file `stream` yang telah digunakan sebelumnya dan akan me-return (menghasilkan) angka 0 apabila sukses atau EOF jika tidak (namun return value ini dapat diabaikan saja).

Sebagai contoh:
```c
FILE *f;

f = fopen("settings.dat", "wb");
if (f != NULL) {
    /* lakukan suatu operasi (pengisian data, dll) pada file `f` di sini */

    /* simpan dan tutup file `f` */
    fclose(f);
} else {
    printf("Tidak dapat menyimpan ke settings.dat\n");
}
```

Kode di atas membuka file **settings.dat** dalam folder/directory yang sama dengan program anda dalam bentuk binary untuk diisi dengan data.

[Sequential Access >>](2-SequentialAccess.md)