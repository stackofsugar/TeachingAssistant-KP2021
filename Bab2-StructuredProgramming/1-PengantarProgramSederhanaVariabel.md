[<< Materi Sebelumnya (Silabus) <<](../silabus.md)
# 2.1 - Pengantar (Program Sederhana, Variabel, dan Basic I/O)
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

## Basic I/O
I/O, yang memiliki kepanjangan Input/Output adalah separuh hati dari banyak program. I/O membuat program yang kalian buat dapat berinteraksi dengan dunia luar, baik dengan file, program lain, atau pengguna/manusia. Untuk kali ini, kita hanya akan membahas I/O yang melibatkan pengguna/manusia.
### Basic Output
Salah satu output (keluaran) yang paling mendasar yang dapat dibuat oleh program C adalah perintah *print to console* atau mencetak *console*. Seperti yang telah kita bahas pada sub-subbab sebelumnya mengenai [memahami kode *hello world*](#program-sederhana), kita dapat menggunakan perintah `printf()` untuk mencetak apapun yang kita mau ke konsol. 
```c
printf("Hello, World!");
printf("Hello 1234");
```
Sejauh ini, kita baru mempelajari cara mencetak data yang langsung kita berikan sebagai *string* atau tulisan mentah. Bagaimana jika kita ingin mencetak nilai dari sebuah variabel? Caranya adalah dengan menggunakan format. Perhatikan kode di bawah ini.
```c
#include <stdio.h>  
int main() {
	char name[8] = "Michael";  
	int number = 150;
	
	printf("Your Variables: %s %d \n", name, number);
	// '\n' adalah "newline", sama seperti "enter"
	return  0;  
}
```
*Output* pada *console*:
```
Your Variables: Michael 150
```
Pada contoh program di atas, kita menggunakan format pada fungsi `printf()` kita untuk mencetak variabel `name[]` dan `number`, di mana `name[]` bertipe *char array* atau string, sedangkan `number` bertipe integer. Seperti yang dapat kita lihat, konstanta format (`%s` dan `%d`) merupakan sebuah placeholder atau tempat dari variabel yang kita berikan di sebelah kanan. `%s` berkorespondensi dengan variabel `name`, sedangkan `%d` dengan `number`. Format bagi masing-masing tipe data berbeda-beda. Lihat tabel dan potongan kode di bawah ini.

|Placeholder|Tipe Data|Penjelasan|
|:---------:|---------|----------|
|%s|string / *char array*|Tulisan alfanumerik|
|%d|integer|Angka/bilangan|
|%f|floating point|Bilangan real|

```c
#include <stdio.h>  
int main() {
	char name[9] = "Everglow";  
	int number = 42;
	float real = 3.14;

	printf("Your Variables: %s %d %f \n", name, number, real);
	// Pada compiler modern, return pada main() tidak harus dituliskan
	// Referensikan ke perintah dosen kalian mengenai penulisan return pada main()
}
```
*Output* pada *console*:
```
Your Variables: Everglow 42 3.14
```
> Cara terbaik untuk memahami Basic I/O adalah terus mencoba dan bereksperimen pada IDE kalian!

### Basic Input
Jika kita sudah mengetahui bagaimana cara mencetak variabel yang telah kita definisikan, sekarang kita akan mempelajari cara meminta pengguna program kita untuk mengisi sebuah variabel. Perhatikan contoh kode di bawah.
```c
#include <stdio.h>  
int main() {
	char name[100];  
	int number;
	float real;

    printf("Enter a value: ");
    scanf("%s %d %f", name, &number, &real);
	
	printf("Your Inputs: %s %d %f \n", name, number, real);
}
```
*Output* pada *console*:
```
Enter a value: Halo 12 43.93
Your Inputs: Halo 12 43.93
```
> Note: "Halo 12 43.93" adalah nilai yang dimasukkan oleh pengguna

Dapat kita lihat bahwa fungsi yang "menangkap" masukan/input pengguna dari *console*, yaitu `scanf()`, menggunakan format placeholder yang sama dengan fungsi `printf()`.
```c
scanf("%s %d %f", name, &number, &real);
```
Potongan fungsi di atas akan menangkap masukan pengguna yang dibatasi oleh spasi, dan urut berupa string, integer, dan float, dari kiri ke kanan. Dengan menginput `Halo 12 43.93`, program akan memasukkan "Halo" ke variabel `name`, 12 ke variabel `number`, dan 43.93 ke variabel `real`.  Diperlukan *ampersand* (`&`) di depan variabel berjenis integer/floating point, namun tidak akan dijelaskan alasannya sekarang. *Do as above*
Fungsi `scanf()` yang kita gunakan ini memiliki sebuah kekurangan, yaitu tidak bisa menerima *string* yang ber-spasi. Namun, kita akan tetap menggunakan metode ini untuk sekarang.
> Cobalah bereksperimen dengan memberikan masukan ber spasi, atau menghapus ampersand (&) di awal variabel integer dan floating point!

<br />

[>> Materi Berikutnya (Algoritma, Pseudocode, dan Source Code) >>](2-AlgoritmaPseudocodeSourcecode.md)
