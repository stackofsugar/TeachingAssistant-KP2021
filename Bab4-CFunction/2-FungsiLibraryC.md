[<< Materi Sebelumnya (Pengenalan Function) <<](1-PengenalanFunction.md)

# 4.2 Fungsi-fungsi Dasar Library C
Library C, atau yang teman-teman mungkin sering kenal sebagai C standard library merupakan sebuah library bawaan dari instalasi compiler atau IDE C/C++ teman-teman. Library dalam dunia pemrograman merupakan sekumpulan fungsi yang sudah disediakan oleh compiler/IDE yang dapat teman-teman gunakan dalam program kalian. Salah satu contoh konkret dari library C pada materi sebelumnya adalah `printf()` dan `scanf()`.

## Letak Library C
Library C terletak pada file-file yang dinamakan *header*. File *header* ini terletak di suatu tempat pada instalasi compiler/IDE C kalian dan berisi banyak deklarasi dari fungsi C, macros, dan predefined variables yang dapat kalian gunakan, walaupun kita akan membahas mengenai fungsi terlebih dahulu. Library C bukan merupakan satu library, namun puluhan atau bahkan ratusan library. Beberapa kalian pernah melihat sebelumnya seperti library `stdio`, dan beberapa akan kita bahas lebih lanjut pada materi ini seperti library `math`.

## Penggunaan Library C
Untuk menggunakan library C, kalian harus memberi tahu compiler kalian jika kalian menggunakan library tertentu. Sebagai contoh, jika kalian ingin menggunakan fungsi `printf()`, karena printf terletak di library `stdio`, kalian harus menuliskan `#include <stdio.h` di awal kode kalian, yang pada intinya memberi tahu jika kalian akan menggunakan library tersebut di program kalian. Perhatikan contoh program di bawah.
``` c
#include <stdio.h>
// Meng-include library stdio untuk menggunakan printf

int main() {
	printf("Quack!");
	// Menggunakan printf, bagian dari stdio
}
```

## Contoh-contoh Library C
Supaya kalian dapat lebih memahami kemampuan dari library C, berikut beberapa contoh library C yang paling sering digunakan.

### 1. stdio
Library stdio mencakup fungsi-fungsi yang berhubungan dengan I/O standar menggunakan 3 jenis *stream*, yaitu input, output, dan error. Selain mencetak ke konsol, library ini juga bisa menuliskan keluarannya ke file menggunakan `FILE`. Di bawah ini merupakan fungsi-fungsi pada library `stdio` yang sering digunakan
|Nama|Perilaku|Deklarasi|
|-----------|---------------|------------------|
|`printf()`|Mencetak keluaran ke konsol pengguna|`int printf(const char *format, ...)`|
|`scanf()`|Meminta masukan keyboard pengguna lewat konsol|`int scanf(const char *format, ...)`|
|`sprintf()`|Mengirim keluaran berformat ke string|`int sprintf(char *str, const char *format, ...)`|
|`sscanf()`|Membaca keluaran berformat dari string|`int sscanf(const  char  *str,  const  char  *format,  ...)`|

Untuk list lengkap, kunjungi [laman ini](https://www.tutorialspoint.com/c_standard_library/stdio_h.htm).
<details>
<summary>Contoh penggunaan library stdio</summary>

```c
// Mendeklarasikan penggunaan library stdio
#include <stdio.h>

int main() {
    // >> Contoh 1: scanf() dan printf() <<
    char quacking[50];
    // Meminta masukan string dari user, lalu mengeluarkannya ke konsol
    printf("Masukkan sebuah kata: ");
    scanf("%s", quacking);
    printf("%s\n", quacking);

    // >> Contoh 2: sprintf() <<
    char waktu[50];
    // Mengisi variabel waktu dengan string berformat
    char hari[] = "Rabu", bulan[] = "Mei";
    int tanggal = 8, tahun = 2002;
    sprintf(waktu, "%s, %d %s %d", hari, tanggal, bulan, tahun);
    printf("Nilai dari variabel waktu: %s\n", waktu);

    // >> Contoh 3: sscanf() <<
    char waktu2[] = "Senin 22 Juli 2002";
    // Mengisi beberapa variabel dibawah dari variabel waktu2
    char hari2[10], bulan2[10];
    int tanggal2, tahun2;
    sscanf(waktu2, "%s %d %s %d", hari2, &tanggal2, bulan2, &tahun2);
    printf("Nilai dari variabel:\n");
    printf("Hari2: %s\nTanggal2: %d\nBulan2: %s\nTahun2: %d\n", hari2, tanggal2, bulan2, tahun2);
}
```
</details>

### 2. math
Library math memiliki banyak fungsi yang mempermudah pengguna dalam menggunakan operasi matematika yang tidak memiliki operator khusus, dan terdefinisikan pada file `math.h`.  Fungsi-fungsi yang ada di dalam library ini termasuk trigonometri (sin, cos, tan), invers trigonometri (asin, acos, atan), hiperbolik (sinh, cosh, tanh), pemangkatan, pengakaran, logaritmik, dan beberapa fungsi untuk menentukan hubungan matematis dari 2 atau lebih nilai. 
|Nama|Perilaku|Deklarasi|
|----|--------|---------|
|`pow()`|Mengembalikan hasil perpangkatan bilangan x oleh y (x^y)|`double pow(double x, double y)`|
|`sqrt()`|Mengembalikan hasil pengakaran kuadrat bilangan x (x akar 2)|`double sqrt(double x)`|
|`ceil()`|Mengembalikan bilangan bulat <= x|`double ceil(double x)`|
|`floor()`|Mengembalikan bilangan bulat >= x|`double floor(double x)`|
|`sin()`|Mengembalikan sinus radian dari x. Berlaku pula untuk `cos()` dan `tan()`|`double sin(double x)`|
|`log10()`|Mengembalikan logaritma basis 10 dari x, gunakan `log()` untuk basis `e` / logaritma natural|`double log10(double x)`|
  
List lengkap tersedia di [laman ini](https://www.tutorialspoint.com/c_standard_library/math_h.htm).
<details>
<summary>Contoh penggunaan library math</summary>

```c
// Mendeklarasikan penggunaan library math
#include <math.h>

// Meng-include library stdio untuk menggunakan printf
#include <stdio.h>

int main() {
    printf("20 kuadrat bernilai %lf\n", pow(20, 2));
    printf("Akar kuadrat dari 256 adalah %lf\n", sqrt(256));
    printf("Bilangan bulat terdekat kebawah dengan 5.43134 adalah %lf\n", floor(5.43134));
    printf("Bilangan bulat terdekat keatas dari 9.3234 adalah %lf\n", ceil(9.3234));
    printf("Sin, Cos, dan Tan dari radian 2 berturut-turut adalah %lf, %lf, dan %lf\n", sin(2), cos(2), tan(2));
    printf("10 Log 100 bernilai %lf\n", log10(100));
    printf("ln 10 bernilai %lf\n", log(10));
}
```
</details>

### 3. String
Library string berisi fungsi-fungsi yang sangat berguna untuk modifikasi string, seperti mengcopy isi string dan membandingkan kesamaan antara 2 string.
|Nama|Perilaku|Deklarasi|
|----|--------|---------|
|`strcpy()`|Mengcopy nilai string dari `src` menuju `dest`|`char *strcpy(char *dest, const char *src)`|
|`strcat()`|Meng-append nilai string src di belakang dest (dest + src)|`char *strcat(char *dest, const char *src)`|
|`strlen()`|Menghitung panjang dari string|`size_t strlen(const char *str)`|
|`strstr()`|Mencari keseluruhan string `needle` pada string `haystack`|`char *strstr(const char *haystack, const char *needle)`|
|`strcmp()`|Membandingkan nilai dari kedua string, mengembalikan 0 jika sama|`int strcmp(const char *str1, const char *str2)`|

Selengkapnya dapat dilihat di [laman ini](https://www.tutorialspoint.com/c_standard_library/string_h.htm).

<details>
<summary>Contoh penggunaan library string</summary>

```c
// Mendeklarasikan penggunaan library string
#include <string.h>

// Meng-include library stdio untuk menggunakan printf
#include <stdio.h>

int main() {
    // Penggunaan strcpy()
    /* Secara intuitif, fungsi ini berlaku seperti str1 = str2,
     * namun, tipe data string (char *) tidak bisa dikenakan
     * assignment operator (=) kecuali pada pendefinisian
    */
    char str2[] = "Hello from C!", str1[14];
    strcpy(str1, str2);
    printf("%s\n", str1);

    // Penggunaan strcat()
    char str3[30] = "Good Morning, ", str4[] = "How are you?";
    strcat(str3, str4);
    printf("%s\n", str3);

    // Penggunaan strlen()
    char str5[] = "1234567890";
    printf("Panjang dari \"%s\" adalah %d\n", str5, (int)strlen(str5));

    // Penggunaan strstr()
    char str6[] = "The global poor all around the world.", str7[] = "around";
    if (strstr(str6, str7) != NULL) {
        printf("Substring \"%s\" ditemukan dalam string \"%s\"\n", str7, str6);
    }

    // Penggunaan strcmp()
    char str8[] = "travel", str9[20];
    printf("Tuliskan \"%s\": ", str8);
    scanf("%s", str9);
    if (!strcmp(str8, str9)) {
        printf("Benar!\n");
    }
    else {
        printf("Salah :(\n");
    }
}
```
</details>

### 4. stdlib
Library stdlib memiliki beberapa fungsi yang mungkin akan kerap kalian pakai di program kalian, salah satunya `rand()` dengan pasangannya yaitu `srand()`. Selain itu, banyak sekali fungsi utilitas untuk mengubah bentuk variabel, seperti string ke integer dan beberapa algoritma sorting, namun tidak dibahas secara detail pada contoh. Untuk list lebih lanjut, bisa dilihat di [sini](https://www.tutorialspoint.com/c_standard_library/stdlib_h.htm).
|Nama|Perilaku|Deklarasi
|----|--------|--------|
|`rand()`|Mengembalikan bilangan bulat `pseudorandom` antara 0 dan `RAND_MAX` (tergantung implementasi compiler)|`int rand(void)`|
|`srand()`|Memberikan seed untuk generator `rand()`|`void srand(unsigned int seed)`|
|`exit()`|Mengakibatkan program untuk di-terminate / dihentikan|`void exit(int status)`|
|`system()`|Menjalankan sebuah perintah dari shell/terminal/cmd (tidak disarankan karena tidak cross-platform)|`int system(const char *string)`|

<details>
<summary>Contoh penggunaan library stdlib</summary>

```c
// Mendeklarasikan penggunaan library stdlib
#include <stdlib.h>

// Meng-include library stdio untuk menggunakan printf
#include <stdio.h>

// Meng-include library time untuk menggunakan time()
#include <time.h>

// Meng-include library string untuk komparasi string sederhana
#include <string.h>

int main() {
    // Penggunaan rand() bersama srand() untuk mendapatkan angka pseudorandom
    srand((unsigned)time(NULL));
    printf("Berikut nilai random dari 10 - 30: %d\n", (10 + (rand() % 21)));

    // exit() untuk terminasi program tanpa menyelesaikan hingga akhir main()
    char exit_consent[20];
    printf("Ketik \"halo\" untuk keluar dari program sekarang juga: ");
    scanf("%s", exit_consent);
    if (!strcmp(exit_consent, "halo")) {
        exit(EXIT_SUCCESS);
    }

    // system() untuk memanggil perintah dari terminal/shell/cmd
    /* PENTING:
     * system() harus digunakan secara bijak, karena tidak semua perintah
     * terminal merupakan perintah yang cross-platform. Misalnya, pada
     * Windows terdapat perintah cls untuk menghapus screen namun pada
     * Linux perintahnya adalah clear. Oleh karena itu, jika kalian
     * ((terpaksa)) untuk menggunakannya, pastikanlah sistem operasi
     * user kalian dicek terlebih dahulu yang akan diajarkan pada beberapa
     * pertemuan ke depan, yaitu preprocessor directives.
    */
    char delete_consent[20];
    printf("Ketik \"halo\" untuk menghapus terminal: ");
    scanf("%s", delete_consent);
    if (!strcmp(delete_consent, "halo")) {
        system("cls"); // Jika OS anda bukan Windows, hapuslah line ini
    }
    printf("Apakah sudah terhapus?");
}
```
</details>

[>> Materi Berikutnya (Rekursi) <<](4-Rekursi.md)
