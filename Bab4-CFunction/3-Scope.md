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

[Materi Berikutnya (Rekursi) >>](4-Rekursi.md)
