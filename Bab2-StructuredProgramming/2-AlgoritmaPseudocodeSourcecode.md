# 2.2 - Algoritma, Pseudocode, dan Source Code

Dalam pembuatan program, kita pasti akan sering berhadapan dengan istilah "algoritma", "pseudocode", dan "source code". Sebenarnya apa sih perbedaan yang paling mendasar di antara mereka bertiga? Mari kita bahas semuanya di sini.

## Algoritma

Dalam menyusun suatu program, kita pasti akan berpikir terlebih dahulu tentang apa yang akan kita buat sehingga membentuk **alur program** berjalan. **Algoritma** itulah yang merupakan perwujudan dari apa yang telah kita pikirkan dan kita rancang sebelum menjadi sebuah program. Secara umum, algoritma masih berbentuk kalimat-kalimat **tidak formal** yang berisi **langkah-langkah** bagaimana program kita berjalan. Contohnya adalah sebagai berikut:

**Algoritma 1.** Berikut merupakan contoh algoritma program yang menjumlahkan dua bilangan kemudian menampilkannya ke console
```
1. Ambil angka A dari console
2. Ambil angka B dari console
3. Tampilkan hasil dari A + B ke console
```

**Algoritma 2.** Berikut merupakan contoh lain algoritma program yang menentukan kelulusan ujian suatu mahasiswa
```
1. Ambil nilai ujian salah satu mahasiswa (dari console)
2. Jika nilai tersebut:
    - 75 ke atas, maka mahasiswa tersebut lulus (tampilkan ke console)
    - Kurang dari 75, maka mahasiswa tersebut harus menjalani remidiasi (tampilkan ke console)
```

## Pseudocode

Cara lain untuk **merepresentasikan suatu algoritma** adalah dalam bentuk **pseudocode**. Pseudocode pada dasarnya merupakan potongan kode yang menggunakan sintaks (aturan penulisan) yang **tidak formal** dengan tujuan memudahkan pembaca untuk memahami algoritmanya. Tidak ada batasan khusus dalam pembuatan pseudocode, asalkan mudah dimengerti dan dipahami saja oleh orang lain sehingga dapat mengetahui algoritma yang kita buat tanpa harus meraba-raba source codenya.

Berikut merupakan contoh pseudocode program berdasarkan **Algoritma 1**
```
A = INPUT()
B = INPUT()
OUTPUT(A + B)
```

Kemudian berikut merupakan contoh pseudocode program berdasarkan **Algoritma 2**
```
nilaiMahasiswa = INPUT()
IF (nilaiMahasiswa >= 75):
    OUTPUT("Selamat!")
    OUTPUT("Anda dinyatakan lulus")
ELSE IF (nilaiMahasiswa < 75):
    OUTPUT("Maaf!")
    OUTPUT("Anda harus mengikuti remidiasi")
```

## Source Code

Yang terakhir adalah source code. **Source code** merupakan wujud implementasi dari suatu algoritma atau pseudocode dalam **sintaks yang formal** sehingga instruksi-instruksinya dapat dimengerti dan dijalankan oleh komputer. Source code dapat ditulis menggunakan bahasa pemrograman apapun (C/C++/Java/Python/dll) sehingga dapat dicompile dan/atau dijalankan oleh komputer.

Berikut merupakan contoh source code program berdasarkan **Algoritma/Pseudocode 1** dalam bahasa C
```c
#include <stdio.h>

int main() {
    int A, B;

    printf("Masukkan angka pertama: ");
    scanf("%d", &A);

    printf("Masukkan angka kedua: ");
    scanf("%d", &B);

    printf("Nilai dari %d + %d = %d\n", A, B, A + B);

    return 0;
}
```

Berikut merupakan contoh source code program berdasarkan **Algoritma/Pseudocode 2** dalam bahasa C
```c
#include <stdio.h>

int main() {
    int nilaiMahasiswa;

    printf("Masukkan nilai anda: ");
    scanf("%d", &nilaiMahasiswa);

    if (nilaiMahasiswa >= 75) {
        printf("Selamat!\n");
        printf("Anda dinyatakan lulus\n");
    } else if (nilaiMahasiswa < 75) {
        printf("Maaf!\n");
        printf("Anda harus mengikuti remidiasi\n");
    }

    return 0;
}
```
