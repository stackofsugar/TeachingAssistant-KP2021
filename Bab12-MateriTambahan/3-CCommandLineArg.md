[<< Materi Sebelumnya (Variable Length Argument) <<](2-VariableLengthArg.md)

# C Command Line Argument

## Pendahuluan

Kalian mungkin sudah pernah melihat beberapa program yang dapat menerima argumen dari command line bukan? Jika kalian menggunakan compiler GCC dari command line, jika kalian ingin mengcompile sebuah program C menuju executable, kalian mungkin akan menuliskan perintah di bawah ini

```
gcc sourceCode.c -o program.exe
```

Jika kalian perhatikan dengan baik, kalian pasti akan mengetahui bahwa `gcc` merupakan sebuah program, dan `sourceCode.c`, `-o`, dan `program.exe` merupakan argumen-argumen yang diberikan untuk perogram `gcc`. Pertanyaan yang mungkin muncul adalah bagaimana cara sebuah program C "menangkap" argumen yang diberikan pada command line? Bab ini akan membahas itu. Kemampuan sebuah program untuk menangkap argumen yang diberikan oleh pengguna akan membuka peluang yang besar dalam optimisasi program. Misalnya, jika program kalian awalnya harus meminta masukan pengguna menggunakan `scanf()`, kalian dapat mengubahnya untuk menerima argumen command line saja.

## Syntax

Penggunaan command line argument dalam C cenderung sangat mudah. Kalian hanya perlu "menginisiasi" dua variabel sebagai argument `main()`. Inisiasi dapat dilakukan seperti pada potongan kode di bawah ini:

```c
int main(int argc, char **argv) {
    /* ... */
}
```

Sebagai tambahan, `char **argv` merupakan array dua dimensi bertipe `char`, sehingga potongan kode di atas dapat ditulis kembali seperti di bawah ini:

```c
int main(int argc, char *argv[]) {
    /* ... */
}
```

Nah, seperti yang dapat dilihat, kita memberikan dua buah parameter ke fungsi `main()` kita. Kedua parameter tersebut dapat kita breakdown di bawah ini:

-   `int argc`: Merupakan variabel yang akan memuat jumlah argumen yang diberikan kepada program **ditambah satu**.
-   `char **argv`: Merupakan sebuah array char dua dimensi (yang dapat diartikan sebagai array string) yang akan memuat argumen-argumen yang diberikan kepada program.

## Analisis

Perhatikan command line di bawah ini. Asumsikan bahwa `program.exe` merupakan program yang kalian buat, yang dapat menerima dan membaca command line argument

```
./program.exe anjing dan kucing
```

Jika kalian masuk ke dalam program kalian dan membaca variabel `argc` serta `argv`, nilai di bawah akan kalian dapatkan:

-   `argc`: 3
-   `argv[0]`: Full path (atau short path, tergantung compiler dan versi) ke executable kalian, tergantung dari penempatan kalian. Misalnya C:\progBuilds\c\program.exe
-   `argv[1]`: anjing
-   `argv[2]`: dan
-   `argv[3]`: kucing

Cukup intuitif dan mudah dipahami bukan? Kalian dapat mengetes teori di atas dengan contoh kode di bagian berikut.

## Contoh Penggunaan

```c
#include <stdio.h>

int main(int argc, char **argv) {
    if (argc > 0) {
        printf("Jumlah argumen: %d\n", argc);
        for (int i = 0; i < argc; i++) {
            printf("Argumen ke %d: %s\n", i, argv[i]);
        }
    }
}
```

Cara menggunakan:

1. Compile kode tersebut, misalkan ke `commandline.exe`
2. Jalankan program kalian dengan menambahkan argumen di belakang `./[program kalian]` misalkan `commandline.exe halo dunia`
3. Perhatikan keluaran program

Misal masukan adalah

```
./namaProgram.exe anjing dan kucing
```

Keluarannya adalah

```
Jumlah argumen: 4
Argumen ke 0: F:\***\namaProgram.exe
Argumen ke 1: anjing
Argumen ke 2: dan
Argumen ke 3: kucing
```

[>> Kembali ke Silabus >>](../silabus.md)