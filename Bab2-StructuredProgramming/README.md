# 2.1 - Pengantar (Program Sederhana, Variabel)
## Program Sederhana
Seperti yang sudah ditunjukkan pada perkuliahan teori pertemuan pertama, program C pertama yang teman-teman kenal biasanya dikenal sebagai program *hello world* yang terlihat seperti di bawah ini.
```c
/* Menggunakan library stdio.h */
#include <stdio.h>

// Masuk ke fungsi main
int main() {
    printf("Hello, World!");
    return 0;
}
```
### Memahami kode
Mari kita pisahkan dan pahami masing-masing baris dari kode tersebut, dimulai dari baris paling atas.
```c 
#include <stdio.h>
 ```
 Perintah `#include` merupakan sebuah perintah untuk menggunakan sebuah *library* bawaan C yang dinamakan `stdio.h`, yang memiliki banyak fungsi didalamnya, salah satunya adalah `printf`. Baris kode di atas sering disebut *preprocessor directive*. Ingat, tidak seperti baris kode C pada umumnya, *preprocessor directive* tidak memerlukan titik koma (`;`) pada akhir barisnya.

```c
int main() {
    // ...
}
```
Selanjutnya, fungsi `main()` di atas adalah fungsi utama dalam sebuah kode C.  Kalian akan menulis kode utama dari program kalian di bawah fungsi ini. Di belakang fungsi ini terdapat kata kunci `int` yang menandakan *return value* dari kode kalian yang bertipe *int* atau bilangan bulat. Kita akan membahas *return value* dan tipe data di pertemuan mendatang. Untuk sekarang, gunakanlah kode diatas untuk memulai program kalian.
```c
printf("Hello, World!");
```
Fungsi `printf()` di atas adalah fungsi bawaan C yang terdapat pada *library* `stdio.h`. Fungsi ini digunakan untuk mencetak *string* atau tulisan yang kalian masukkan sebagai parameter (di dalam kurung fungsi) ke *console* kalian (misal Windows cmd). Di contoh tersebut, kita mencetakkan tulisan **"Hello, World!"** ke *console* kita.
```c
return 0;
```
Kata kunci `return` digunakan untuk menghentikan sebuah fungsi (dalam kasus ini `main()`) dan mengembalikan kontrol ke pemanggil fungsi. Karena `main()` merupakan fungsi utama, maka memanggil return akan menghentikan program. Angka `0` yang terdapat setelah `return` menandakan kode program. Jika program berjalan lancar, biasanya kode yang dipakai adalah `0`.
```c
// Masuk ke fungsi main
/* Menggunakan library stdio.h */
```
Terakhir, 2 baris di atas merupakan baris komentar yang tidak akan digunakan pada program. Komentar dapat menjadikan kode kalian lebih mudah dipahami, khususnya untuk pemrogram lain. Komentar dalam C mengikuti *syntax* seperti di atas, dengan menambahkan `//` sebelum komentar, atau mengapit komentar dengan `/*` dan `*/`.

## Variabel dan Tipe Data C
Pada hampir semua bahasa pemrograman, terdapat sebuah sistem yang bernama variabel. Seperti pada aljabar, variabel adalah sebuah ekspresi yang berfungsi untuk menyimpan sebuah data. Pada aljabar, variabel dapat digambarkan di bawah ini.
```
x + y = 10
2x + 5y = 38
```
Dari contoh di atas, dapat disimpulkan bahwa `x` bernilai 4 dan `y` bernilai 6. Pada bahasa C, terdapat juga variabel yang memiliki fungsi yang mirip seperti di atas, namun dengan berbagai macam jenis, masing-masing memiliki jenis data apa yang dapat disimpan dalam variabel tersebut. Lihat tabel di bawah ini

### Tipe data C
|Tipe Data|Jenis Data|Pendefinisian|
|--|--|--|
|Integer|Bilangan bulat|`char`, `short`, `int`, `long`, dan `long long`|
|Unsigned Integer|Bilangan bulat non-negatif|Sama dengan atas, diberi imbuhan depan `unsigned`|
|Floating Point|Bilangan real|`float` dan `double`|
|Structure|Tipe data buatan pengguna|Buatan pengguna|

Setiap tipe data di atas memiliki rentang (nilai maksimal dan minimal yang dapat disimpan dalam sebuah variabel) masing-masing. Contohnya, `char` hanya dapat menyimpan -128 hingga 127, sedangkan `long` hingga 2 milyar tergantung pada implementasinya. Tipe data `unsigned` tidak dapat merepresentasikan bilangan negatif, namun rentang atasnya dua kali dari bilangan bulat. Floating point dapat menyimpan bilangan real seperti `3.14` atau `12.345`.

### Pendefinisian Variabel C
Variabel di bahasa pemrograman C harus didefinisikan sebelum dipakai pada program. Sebagai contoh, kita akan mendefinisikan sebuah variabel bernama `bejo` dan `dengklek` yang menyimpan nilai `42` dan `68`. Untuk nilai yang berupa angka, kita biasa menggunakan tipe data `int`.
```c
int bejo = 42;
int dengklek 68;
```
Kita coba untuk mendefinisikan variabel di atas dengan gaya yang berbeda.
```c
int bejo = 42, dengklek = 68;
```
Kita coba untuk mendefinisikan variabel di atas, namun tidak memberikan nilai untuknya.
```c
int bejo, dengklek;
```

### Materi Berikutnya
[Algoritma, Pseudocode, dan Source Code](https://github.com/stackofsugar/TeachingAssistant-KP2021/blob/main/Bab2-StructuredProgramming/2-AlgoritmaPseudocodeSourcecode.md)
