[<< Pengenalan Pointer](1-Pengenalan.md)

# 6.2 - Pass By Reference

Sekarang kita tinjau kembali masalah yang ada pada topik pengantar sebelumnya
```c
#include <stdio.h>

int kurangi_health(int jumlah);

int main() {
    int health = 100;

    printf("Health awal: %d\n", health);

    /* Asumsikan anda ingin mengurangi nilai dari `health` sebesar 20 */
    /* Akan tetapi anda tidak ingin mengurangkannya langsung di sini, melainkan melalui suatu function */
    kurangi_health(20);

    printf("Health akhir: %d\n", health);

    return 0;
}

int kurangi_health(int jumlah) {
    /* Namun terdapat suatu masalah di sini, yaitu scopenya berbeda dengan main() */
    /* Sehingga pada area ini, `health` tidak terdefinisi dan kode di bawah akan memproduksi error */

    health = health - jumlah; /* ERROR: compiler tidak dapat menemukan variabel `health` */
}
```

Suatu fungsi dapat menerima argumen berupa **pointer** dengan cara mengatur tipe data salah satu parameter menjadi pointer. Karena pointer memiliki kemampuan untuk memanipulasi nilai suatu variabel bahkan yang terletak di luar scope yang bersangkutan, maka penerapan pointer sebagai parameter dalam fungsi dapat menyelesaikan permasalahan tersebut.

Kode di atas dapat dimodifikasi menjadi:
```c
#include <stdio.h>

/* Tambah parameter berupa pointer */
int kurangi_health(int *health_ptr, int jumlah);

int main() {
    int health = 100;

    printf("Health awal: %d\n", health);

    /* Asumsikan anda ingin mengurangi nilai dari `health` sebesar 20 */
    /* Akan tetapi anda tidak ingin mengurangkannya langsung di sini, melainkan melalui suatu function */
    /* Perubahan nilai menggunakan pass-by-reference yang mana fungsi menerima argumen berjenis pointer */
    kurangi_health(&health, 20);

    printf("Health akhir: %d\n", health);

    return 0;
}

int kurangi_health(int *health_ptr, int jumlah) {
    /* Akses variabel yang dirujuk oleh `health_ptr` */

    *health_ptr = *health_ptr - jumlah;
}

/*
Output:

Health awal: 100
Health akhir: 80
*/
```

[Dynamic Memory Allocation >>](3-DMA.md)