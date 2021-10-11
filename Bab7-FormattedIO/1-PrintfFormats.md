[<< Kembali ke Silabus <<](../silabus.md)

# 7.1. - Printf Formats

Kalian semua pasti sudah sangat familiar dengan sebuah fungsi dalam bahasa pemrograman C yang bernama `printf()`, yang sering digunakan untuk mencetak tulisan ke _console_ pengguna. Fungsi `printf()` memberikan sebuah cara bagi kita untuk membuat keluaran yang berformat. Keluaran berformat yang dimaksud di sini adalah kita tidak mengeluarkan _string_ dan variabel yang kita berikan apa adanya, melainkan menggunakan _format specifier_ yang diperlukan supaya _compiler_ dapat memahami cara untuk mencetak _string_ dan variabel yang kita berikan. Perhatikan contoh di bawah ini.

```c
printf("Halo, %s. Hari ini tanggal %d\n", nama, tanggal);
```

Potongan kode di atas merupakan implementasi operasi keluaran berformat. `%s` dan `%d` di atas dapat dikenal sebagai _format specifier_ dan digunakan sebagai _placeholder_ atau tempat penampung bagi variabel-variabel yang akan kita pakai, secara urut. Jadi, `%s` di atas merupakan penampung bagi variabel nama, `%d` untuk variabel tanggal. Selanjutnya, `\n` diatas merupakan _escape character_ yang digunakan untuk memberikan baris baru. Jika kita asumsikan variabel `nama = "Dengklek"` dan `tanggal = 7`, jika kita jalankan potongan kode di atas kita akan mendapatkan keluaran di bawah ini.

```
Halo, Dengklek. Hari ini tanggal 7
```

Selain 2 _format specifier_ di atas, masih sangat banyak _format specifier_ lain yang dapat kalian gunakan sesuai dengan kebutuhan kalian di waktu tertentu, saat bekerja dengan berbagai macam jenis variabel. Dokumentasi lengkap dapat kalian lihat [di sini](https://www.tutorialspoint.com/format-specifiers-in-c), sedangkan beberapa yang paling sering dipakai dapat dilihat di bawah.

| _Format Specifier_ | Tipe Variabel |
| ------------------ | ------------- |
| `%c`               | `char`        |
| `%d` dan `%i`      | `int`         |
| `%ld` dan `%i`     | `long int`    |
| `%f`               | `float`       |
| `%lf`              | `double`      |
| `%s`               | `string`      |
| `%x`               | `hexadecimal` |

## Utilitas Spesial

Selain penggunaan seperti di atas, kalian dapat menggunakan _format specifier_ yang spesial untuk lebih menyesuaikan penggunaan kita.

```c
printf("%-20.5f");
```

Potongan kode di atas menggunakan beberapa utilitas spesial `printf()`. Karakter `-` digunakan untuk mengatur keluaran rata kanan, angka `20` merupakan _minimum field width_ atau minimal panjang variabel tersebut, dan jika kurang, maka akan di-append/prepend 0. `.` merupakan pemisah antara `minimum field width` dan `presicion`. Terakhir, `5` adalah nilai _presision_, di mana jika tipe data float/double, maka floating point akan dicetak hingga `5` angka signifikan, sedangkan jika tipe data _string_, maka akan dicetak hanya `5` karakter pertama dalam _string_ itu.

[>> Materi Selanjutnya (Scanf Formats) >>](2-ScanfFormats.md)
