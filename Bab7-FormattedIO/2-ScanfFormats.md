[<< Materi Sebelumnya (Prinf Formats) <<](1-PrintfFormats.md)

# 7.2. - Scanf Formats

Seperti yang sudah kalian pelajari di [materi sebelumnya](1-PrintfFormats.md), _format specifier_ digunakan di perintah `printf()` supaya _compiler_ dapat memahami bagaimana kita ingin cetak variabel yang kita berikan ke _console_ pengguna. Seperti `printf()`, fungsi `scanf()` yang biasa kita gunakan untuk menerima masukan dari pengguna juga menggunakan _format specifier_ supaya _compiler_ memahami jenis variabel yang akan kita masukkan dari masukan pengguna. Perhatikan potongan kode di bawah ini.

```c
int num;
char ch;
char str[10];
unsigned long uln;

scanf("%d %c %s %lu", &num, &ch, str, &uln);
```

Jika kita menjalankan potongan kode di atas, compiler akan meminta masukan ke pengguna sesuai dengan urutan yang kita berikan di format `scanf()`, yaitu `%d %c %s %lu`. Jadi, format digunakan pada fungsi `scanf()` dalam bahasa C untuk mengatur urutan pengambilan masukan pengguna serta memberitahu compiler akan tipe data dari variabel yang ingin kita masuki. _Format specifier_ yang digunakan di `scanf()` serupa dengan yang kita gunakan di materi sebelumnya, yang disajikan di tabel di bawah ini.

| _Format Specifier_ | Tipe Variabel |
| ------------------ | ------------- |
| `%c`               | `char`        |
| `%d` dan `%i`      | `int`         |
| `%ld` dan `%i`     | `long int`    |
| `%f`               | `float`       |
| `%lf`              | `double`      |
| `%s`               | `string`      |
| `%x`               | `hexadecimal` |

[>> Kembali ke Silabus >>](../silabus.md)
