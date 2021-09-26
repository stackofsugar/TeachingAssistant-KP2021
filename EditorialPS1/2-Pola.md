[<< Jarak Manhattan](1-JarakManhattan.md)

# PS1.2 - Pola

## Penjelasan

Disediakan input bilangan N, anda diminta untuk mengeluarkan pola berbentuk segitiga siku-siku yang diisi oleh digit-digit dari 0 sampai 9 secara berulang. Hal tersebut bisa diperoleh dengan menerapkan loop di dalam loop (loop bercabang).

## Contoh Solusi

```c
#include <stdio.h>

int main() {
    int N; /* input */
    int i, j; /* loop control */
    int k = 0; /* angka yang tertampil di layar */
    
    scanf("%d", &N);

    /* tampilkan sebanyak N baris dikontrol oleh i (mulai dari 1) */
    for (i = 1; i <= N; i++) {
        /* tampilkan sebanyak i kolom dikontrol oleh j */
        for (j = 1; j <= i; j++) {
            printf("%d", k); /* tampilkan nilai dari k */

            /* tambahkan nilai k dengan 1 kemudian di-modulo dengan 10 */
            /* sehingga saat mencapai 10, kembali lagi ke nilai 0 */
            k = (k + 1) % 10;
        }
        printf("\n"); /* pindah ke baris baru */
    }
    return 0;
}
```

[Unik Faktorial >>](3-UnikFaktorial.md)