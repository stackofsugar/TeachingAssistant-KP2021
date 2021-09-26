[<< Unik Faktorial](3-UnikFaktorial.md)

# PS1.4 - Matriks Sempurna

## Penjelasan

Taukah anda? Ternyata soal ini juga bisa diselesaikan jengan jarak manhattan, yaitu dengan menghitung jarak manhattan antara titik yang memuat angka 1 dengan titik tengah (yaitu baris ke-3 kolom ke-3).

## Contoh Solusi

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int i, j; /* loop control */
    int baris_1 = 0, kolom_1 = 0; /* koordinat dari angka 1 */
    int distance;

    /* mendapatkan input baris 1 sampai 5 */
    for (i = 1; i <= 5; i++) {
        /* mendapatkan input kolom 1 sampai 5 */
        for (j = 1; j <= 5; j++) {
            int input;

            /* mendapatkan input baris ke-i kolom ke-j */
            scanf("%d", &input);

            /* cek jika input bernilai 1, masukkan koordinat baris dan kolomnya */
            if (input == 1) {
                baris_1 = i;
                kolom_1 = j;
            }
        }
    }

    /* hitung jarak manhattan dari koordinat angka 1 dengan titik tengah (baris ke-3 dan kolom ke-3) */
    distance = abs(baris_1 - 3) + abs(kolom_1 - 3);
    printf("%d\n", distance);

    return 0;
}
```

[Town Square >>](5-TownSquare.md)