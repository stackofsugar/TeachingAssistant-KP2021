[<< Matriks Sempurna](4-MatriksSempurna.md)

# PS1.5 - Town Square

## Penjelasan

Disediakan town square berdimensi N * M (anggap saja N adalah jumlah baris dan M adalah jumlah kolom) yang akan diisi ubin berukuran persegi A * A. Formula untuk mendapatkan jumlah ubin adalah `CEIL(N/A) * CEIL(M/A)` di mana `CEIL(x)` menghasilkan nilai `x` jika dibulatkan ke atas.

Namun kali ini, kita coba mengoperasikan menggunakan bilangan bulat menggunakan pendekatan yang sedikit berbeda di mana `CEIL(X/Y)` mempunyai algoritma:
```
1. Jika X habis dibagi Y, maka kembalikan hasil baginya eksaknya
2. Jika X tidak habis dibagi Y, maka kembalikan hasil bagi integernya ditambah dengan angka 1
```
Ingat bahwa pembagian integer selalu menghasilkan pembulatannya ke bawah, misal 10 dibagi 4 sama dengan 2 (dibanding dengan nilai eksaknya 2.5, karena ia bukan merupakan bilangan bulat (integer))

Penjelasan lebih lanjut dapat dilihat pada contoh solusinya

## Contoh Solusi

Menggunakan tipe data `long long` (dengan format `%lld`) karena `int` saja tidak cukup dan akan menghasilkan wrong answer.

```c
#include <stdio.h>

int main() {
    long long n, m; /* ukuran town square, n = baris, m = kolom */
    long long a; /* ukuran ubin */
    long long r, c; /* r = jumlah baris ubin yg diperlukan, c = jumlah kolom ubin yg diperlukan */

    scanf("%lld%lld", &n, &m);
    scanf("%lld", &a);

    /* hitung jumlah baris ubin yg diperlukan dengan pembagian integer */
    r = n / a;
    /* jika n dibagi a tidak bersisa, maka seluruh area baris sudah pasti tertutup */
    /* jika n dibagi a masih bersisa, maka tidak seluruh area baris tertutup */
    if (n % a > 0) {
        /* tambah 1 jika masih ada area baris yang belum ditutupi */
        r = r + 1;
    }

    /* hitung jumlah kolom ubin yg diperlukan dengan pembagian integer */
    c = m / a;
    /* jika m dibagi a tidak bersisa, maka seluruh area kolom sudah pasti tertutup */
    /* jika m dibagi a masih bersisa, maka tidak seluruh area kolom tertutup */
    if (m % a > 0) {
        /* tambah 1 jika masih ada area kolom yang belum ditutupi */
        c = c + 1;
    }

    /* jumlah ubin = (baris ubin yg diperlukan) * (kolom ubin yg diperlukan) */
    printf("%lld", (r * c));

    return 0;
}
```

[Silabus >>](../silabus.md)