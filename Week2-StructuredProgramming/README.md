# Week 2 - Structured Programming
### Laman ini sedang dalam pengembangan. Gunakan dengan hati-hati.

![Page under construction. Use with caution!!!](https://hsdn.co.id/wp-content/uploads/under-construction-scaled.jpg)

## Subtopik yang Akan Dibahas
1. [Program C Pertama](#program-c-pertama)

## Program C Pertama
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
Mari kita pisahkan dan pahami masing-masing baris dari kode tersebut, dimulai dari baris paling atas
```c 
#include <stdio.h>
 ```
 Perintah `#include` merupakan sebuah perintah untuk menggunakan sebuah *library* bawaan C yang dinamakan `stdio.h`, yang memiliki banyak fungsi didalamnya, salah satunya adalah `printf`. Baris kode di atas sering disebut *preprocessor directive*

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
Terakhir, kata kunci `return` digunakan untuk menghentikan sebuah fungsi (dalam kasus ini `main()`) dan mengembalikan kontrol ke pemanggil fungsi. Karena `main()` merupakan fungsi utama, maka memanggil return akan menghentikan program. Angka `0` yang terdapat setelah `return` menandakan kode program. Jika program berjalan lancar, biasanya kode yang dipakai adalah `0`.
```c
// Masuk ke fungsi main
/* Menggunakan library stdio.h */
```
Terakhir, 2 baris di atas merupakan baris komentar yang tidak akan digunakan pada program. Komentar dapat menjadikan kode kalian lebih mudah dipahami, khususnya untuk pemrogram lain. Komentar dalam C mengikuti *syntax* seperti di atas, dengan menambahkan `//` sebelum komentar, atau mengapit komentar dengan `/*` dan `*/`.

# TO DO LIST
1. Menambah materi. Materi yang bisa ditambahkan mencakup
	- Data types (termasuk defining dll)
	- Pendefinisian variabel
	- Operators
	- printf type specifier
	- scanf
