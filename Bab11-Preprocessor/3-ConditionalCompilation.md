[<< Materi Sebelumnya (Symbolic Constant dan Macro) <<](2-Symbolic-Constant-dan-Macro.md)

# 11.3 - Conditional Compilation

## Definisi

Conditional compilation adalah sebuah mekanisme pada bahasa-bahasa pemrograman level sedang-rendah yang berfungsi untuk hanya mengcompile bagian dari kode yang diinginkan oleh pengguna saja berdasarkan sebuah kondisi. Conditional compilation ini bisa dibayangkan seperti pengecekan `if-else` yang dijalankan sewaktu masa preprocessing, sebelum compilation. Terdapat beberapa conditional compilation directive yang dapat digunakan seperti `#if`, `#ifdef`, `#ifndef`, `#else`, dan `#elif`. Beberapa directive ini akan dibahas satu-persatu, lalu akan ditunjukkan cara pemakaian secara konkret yang dapat kalian terapkan dalam kode kalian.

## `#if` Directive

Bagian pertama yang akan dibahas adalah `#if` directive. Directive ini memiliki syntax di bawah ini:

```c
#if constant_expression
```

Directive ini mengecek apakah `constant_expression` yang diberikan bernilai `true` atau nonzero (bukan nol). Operand yang digunakan pada `constant_expression` haruslah berupa nilai konstan yang tidak memiliki operasi-operasi seperti decrement, increment, cast, pointer, dan address (`&`). Seperti pada percabangan `if-else`, `#if` directive akan menjalankan blok kode dibawahnya jika `constant_expression` bernilai bukan nol.

## `#ifdef` Directive

Selanjutnya, `#ifdef` directive memiliki syntax di bawah ini:

```c
#ifdef identifier
```

Directive ini mengecek apakah `identifier` yang diberikan sudah didefinisikan. `identifier` dapat didefinisikan dengan `#define` directive (lihat bab sebelumnya) atau dari command line saat user mengcompile sebuah source code, misal di gcc/g++ menggunakan option `-D` untuk mendefinisikan sesuatu secara global. Jika `identifier` telah didefinisikan, `#ifdef` directive akan menjalankan blok kode dibawahnya.

## `#ifndef` Directive

`#ifndef` dapat dikatakan sebagai kebalikan dari directive sebelumnya. Perhatikan syntax di bawah ini:

```c
#ifndef identifier
```

Directive ini mengecek apakah `identifier` yang diberikan sudah didefinisikan. Namun, berkebalikan dengan `#ifdef` directive, `#ifndef` akan menjalankan blok kode dibawahnya jika `identifier` **belum** didefinisikan.

## `#else` Directive

Directive ini memiliki syntax di bawah ini:

```c
#else
```

Jika `#if`, `#ifdef`, dan `#ifndef` dapat digambarkan sebagai percabangan `if` pada kode, maka `#else` directive dapat digambarkan sebagai percabangan `else`. `#else` directive merupakan sebuah directive yang **opsional**, yang akan menjalankan blok kode dibawahnya jika `#if`, `#ifdef`, dan/atau `#ifndef` di atasnya bernilai `false`.

## `#elif` Directive

Perhatikan syntax dari `#elif` directive di bawah ini:

```c
#elif constant_expression
```

Directive ini dapat digambarkan seperti percabangan `else if` pada kode. `#elif` merupakan directive yang **opsional**, yang akan menjalankan blok kode dibawahnya jika `#if`, `#ifdef`, `#ifndef`, atau `#elif` lain diatasnya bernilai `false`.

## `#endif` Directive

Directive ini memiliki syntax di bawah ini:

```c
#endif
```

Seperti halnya percabangan `if-else` pada C harus ditutup dengan kurung kurawal, semua directive yang sudah dijelaskan sebelumnya **harus** ditutup dengan sebuah `#endif` directive. Jika directive yang digunakan adalah nested (seperti `if-else` didalam `if-else`) maka pastikan bahwa `#endif` yang digunakan sudah cukup untuk menutup semua directive seperti contoh di bawah ini.

```c
#if constant_expression
/* ... */
#elif constant_expression
/* ... */
#endif
```

Contoh lainnya, jika digunakan nested directive

```c
#if constant_expression
/* ... */
#elif constant_expression
    #if constant_expression
    /* ... */
    #else
    /* ... */
    #endif
#else
    #if constant_expression
    /* ... */
    #else
    /* ... */
    #endif
#endif

// Indentasi diberikan untuk mempermudah pemahaman
```

## Tambahan: Operator `defined`

Operator `defined` dapat digunakan menggunakan syntax di bawah ini:

```c
defined name
// atau
defined (name)
```

`defined` merupakan sebuah operator yang dapat digunakan bersama dengan `#if` directive, dan akan sangat berguna jika user butuh untuk mengecek banyak kondisi pada `#if` directive dalam satu baris. Untuk melihat cara penggunaan dari `defined` dan directive lain, perhatikan contoh di bawah ini.

## Cara Penggunaan

1. If - Else Sederhana

```c
#define DLIMIT 100

#if DLIMIT < 100
// Bagian kode ini akan dijalankan jika DLIMIT bernilai dibawah 100
dlimitLowHandler();
#elif DLIMIT > 200
// Bagian kode ini akan dijalankan jika DLIMIT bernilai diatas 200
dlimitHighHandler();
#else
// Bagian kode ini akan dijalankan jika kedua #if dan #elif bernilai false
dlimitMidHandler();
#endif
```

2. Penggunaan `#ifdef` dan kawan-kawannya

```c
#define DEBUG

// Jika DEBUG terdefinisi, definisikan PRODUCTION. Jika tidak, definisikan DEPLOYMENT
#ifdef DEBUG
#define PRODUCTION
#else
#define DEPLOYMENT
#endif

int main() {
    int Y = 0;
    for (i = 0; i < 5; i++) {
        int y;
        y = 2*i + 1;
    #ifdef DEBUG
        // Jika DEBUG terdefinisi, eksekusi blok kode di bawah hingga #endif berikutnya
        printf("f(%d): %d\n", i, y);
    #endif
        Y = Y + y;
    }
    printf("Hasil: %d\n", Y);
}
```

3. Penggunaan `defined`

```c
#define DEBUG

#ifdef DEBUG
doSomething();
#endif

#if defined(DEBUG)
doSomething();
#endif

// Kedua blok #ifdef dan #if di atas memiliki perilaku yang sama
```
