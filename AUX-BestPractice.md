[Kembali ke Silabus](silabus.md)

# Best Practice C Programming

## Daftar Topik

- [Return int Untuk Fungsi Main](#return-int-untuk-fungsi-main)
- [Nama Variabel yang Bermakna](#nama-variabel-yang-bermakna)
- [Hindari Implicit Declaration](#hindari-implicit-declaration)
- [Hidupkan Semua Warning](#hidupkan-semua-warning)
- [Rapikan Kode](#rapikan-kode)
- [Hindari Fungsi system](#hindari-fungsi-system)
- [Hindari Penggunaan goto](#hindari-penggunaan-goto)

## Return int Untuk Fungsi Main

Salah:
```c
void main() {
    /* ... */
}
```

Benar:
```c
int main() {
    /* ... */
    return 0;
}
```

**TUJUAN.** Compiler C kuno tertentu memperbolehkan, akan tetapi tidak disarankan untuk compiler yang lebih modern (misal compiler C++) dan kadang akan menimbulkan warning bahkan error

## Nama Variabel yang Bermakna

Salah:
```c
int a, b, c;
```

Benar:
```c
int panjang, lebar, tinggi;
```

**TUJUAN.** Di dalam pekerjaan sebagai programmer atau software developer, anda pasti akan berkolaborasi dengan orang lain. Pastikan kode yang anda tulis dapat dipahami oleh programmer lain. Selain itu, hal ini akan memudahkan anda juga pada saat debugging apabila bertemu dengan error.

## Hindari Implicit Declaration

Salah:
```c
int main() {
    printf("Hello world!\n"); /* compiler tidak akan tahu di mana sumber dari printf */
    return 0;
}
```

Benar:
```c
#include <stdio.h> /* include header yang dibutuhkan printf (stdio.h) */
int main() {
    printf("Hello world!\n");
    return 0;
}
```

Salah:
```c
#include <stdio.h>
int main() {
    foo(); /* compiler belum menemukan deklarasi dari foo() */
    return 0;
}
void foo() {
    printf("FOO!\n");
}
```

Benar:
```c
#include <stdio.h>
void foo(); /* buat deklarasinya terlebih dahulu */
int main() {
    foo();
    return 0;
}
void foo() {
    printf("FOO!\n");
}
```

**TUJUAN.** Dalam compiler yang modern, hal ini akan menjadi warning dan tentunya praktik yang buruk. Dalam C++ juga tidak diperbolehkan. Semua instruksi dalam source code harus jelas dan eksplisit.

## Hidupkan Semua Warning

Hidupkan semua warning pada saat akan mengcompile (bisa diatur melalui compiler options). Mungkin kita bisa menyepelekan warning, namun sangat dianjurkan apabila program yang kita buat bebas dari segala warning yang ada.

**TUJUAN.** Supaya kode yang kita hasilkan berkualitas tinggi dan minim kecacatan.

## Rapikan Kode

Salah:
```c
#include <stdio.h>
int main() {
    int foo = 5;
    if (foo == 5) {
    printf("Hello world!\n");
}
return 0;
}
```

Benar:
```c
#include <stdio.h>
int main() {
    int foo = 5;
    if (foo == 5) {
        printf("Hello world!\n");
    }
    return 0;
}
```

**TUJUAN.** Supaya kode enak dibaca dan jika terdapat suatu error, kita tidak kesulitan dalam debugging.

## Hindari Fungsi system

Fungsi `system` tidak akan berjalan seperti yang diminta dalam berbagai platform (misalkan jika anda memanggil `system("pause")` pada sistem operasi Linux, maka akan muncul error saat pemanggilan command. **Kecuali** anda hanya menargetkan program anda untuk bekerja hanya pada Windows atau sistem operasi tertentu.

Selain itu, keamanan juga menjadi alasan karena apabila program dijalankan dengan opsi "Run As Administrator", maka program memiliki potensi untuk menjalankan command yang berbahaya apabila input tidak disaring terlebih dahulu.

## Hindari Penggunaan goto

Penggunaan `goto` sangat jarang di bahasa pemrograman populer seperti Java, Go, JavaScript, C#, dan lain-lain. Oleh sebab itu, diharapkan untuk menggunakan paradigma pemrograman terstruktur dan program control dalam mengontrol alur dari program yang anda buat. Dengan demikian, anda harus terbiasa dengan pemrograman terstruktur yang mana juga diterapkan di bahasa pemrograman lain.


[Kembali ke Silabus](silabus.md)