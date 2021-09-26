[<< Silabus](../silabus.md)

# PS1.1 - Jarak Manhattan

## Penjelasan

Seperti yang sudah tertera pada soal, program harus menerima input 4 bilangan terurut: x1, y1, x2, dan y2, kemudian menghitung jarak manhattan dari titik 1 (x1, y1) ke titik 2 (x2, y2) menggunakan rumus `abs(x1 - x2) + abs(y1 - y2)` yang mana fungsi `abs` didapat dari header `stdlib.h` atau dapat mengimplementasikannya sendiri menggunakan if-else (jika bilangan negatif, maka ambil minusnya sehingga menjadi positif)

## Contoh Solusi

```c
#include <stdio.h>
#include <stdlib.h> /* menggunakan fungsi abs() pada stdlib.h */

int main() {
    int x1, y1;
    int x2, y2;

    scanf("%d%d", &x1, &y1);
    scanf("%d%d", &x2, &y2);
    printf("%d\n", abs(x1 - x2) + abs(y1 - y2));

    return 0;
}
```

[Pola >>](2-Pola.md)