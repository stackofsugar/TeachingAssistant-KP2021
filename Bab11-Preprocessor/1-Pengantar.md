[<< Silabus](../silabus.md)

# 11.1 - Pengantar Preprocessor

## Apa Itu Preprocessor?

**Preprocessor** adalah serangkaian instruksi yang dijalankan oleh compiler **sebelum** melakukan proses compile pada suatu source code dengan tujuan untuk **memrosesnya** terlebih dahulu (mentransformasikan source code) dan dengan demikian dikatakan preprocessor karena tindakan tersebut.

Dalam bahasa C/C++, perintah-perintah pada preprocessor (atau biasa disebut **directive**) diawali dengan tanda **#** (hashtag).

## Contoh Preprocessor Yang Umum

### #include directive

Berguna untuk memuat isi dari suatu file source code (umumnya header suatu library). Contoh:
```c
#include <stdio.h> /* muat isi dari stdio.h */
#include <stdlib.h> /* muat isi dari stdlib.h */
```

### #define directive

Berguna untuk mendefinisikan suatu konstanta simbolik yang mensubstitusi seluruh simbol yang merujuk pada konstanta tersebut pada source code. Contoh:
```c
#define PI 3.14 /* seluruh simbol PI di source code disubstitusi dengan 3.14 */
#define OPEN_READ_BINARY "rb" /* seluruh simbol OPEN_READ_BINARY di source code disubstitusi dengan "rb" */
#define OUTPUT(x) printf(x) /* seluruh simbol OUTPUT(<suatu isi>) di source code disubstitusi dengan printf(<suatu isi>) */
```

### #if, #elif, dan #endif directive

Sama seperti decision making (if-else) pada program, namun beroperasi pada preprocessor, bukan compiler. Penggunaan ini sering disebut dengan conditional compilation. Contoh:
```c
/* Asumsi menggunakan compiler berbasis GNU GCC */
/* Code di bawah tidak akan bekerja sesuai yang diharapkan di compiler Microsoft Visual C++ */
#if defined(_WIN32)
    printf("Anda menggunakan sistem operasi Windows\n");
#elif defined(__linux__)
    printf("Anda menggunakan sistem operasi Linux\n");
#elif defined(__APPLE__)
    printf("Anda menggunakan sistem operasi macOS X\n");
#else
    printf("Anda menggunakan sistem operasi yang lain\n");
#endif
```
Atau contoh lain:
```c
int Y = 0;
for (i = 0; i < 5; i++) {
    int y;
    y = 2*i + 1;
#if !defined(NDEBUG) /* jika debugging mode menyala pada saat compile */
    printf("f(%d): %d\n", i, y);
#endif
    Y = Y + y;
}
printf("Hasil: %d\n", Y);
```

[Symbolic Constant dan Macro >>](2-Symbolic-Constant-dan-Macro.md)