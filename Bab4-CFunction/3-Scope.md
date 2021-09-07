[<< Materi Sebelumnya (Function Scope) <<](2-FungsiLibraryC.md)

# 4.3 - Aturan Scope

Apa itu scope? **Scope** (atau ruang lingkup) menandakan keterlihatan (visibility) dari suatu **variabel** supaya dapat diakses oleh kode yang membutuhkan

Perhatikan contoh berikut:
```c
if (pilihan == 2) {
    int kode; /* variabel `kode` */

    printf("Masukkan kode: ");
    scanf("%d", &kode);

    /* `kode` dapat digunakan di sini */
    printf("Kode anda: %d\n", kode);

    if (kode == 111) {
        /* `kode` juga masih dapat digunakan di sini, begitu juga seterusnya */
        printf("Kode anda lagi: %d\n", kode);
    }
}
/* tetapi `kode` tidak dapat digunakan di sini, karena perbedaan "scope" */
printf("Kode yang anda masukkan: %d\n", kode /* akan error */);
```

Secara sederhana, semua variabel yang didefinisikan di dalam suatu **block** (`{ ... }`) hanya dapat digunakan dalam ruang lingkup block itu sendiri dan dalamnya. Apabila kita mencoba untuk mengakses variabel yang bersangkutan di luar block tempat didefinisikannya variabel tersebut, maka akan memproduksi error.

## Global Scope

Kita dapat mendefinisikan suatu variabel **di luar** sebuah fungsi dan dengan demikian, variabel tersebut memiliki jenis scope yaitu **global scope**, perhatikan contoh berikut:

```c
#include <stdio.h>

/* variabel `kode` pada global scope */
int kode;

void tampilkan_kode() {
    /* menggunakan variabel `kode` pada global scope */
    printf("Kode anda adalah: %d\n", kode);
}

int main() {
    printf("Masukkan kode: ");
    scanf("%d", &kode); /* menampung ke variabel `kode` pada global scope */

    tampilkan_kode();

    return 0;
}

/*
Output:

Masukkan kode: 555
Kode anda adalah: 555
*/
```

[Materi Berikutnya (Rekursi) >>](4-Rekursi.md)
