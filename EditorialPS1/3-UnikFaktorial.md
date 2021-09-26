[<< Pola](2-Pola.md)

# PS1.3 - Unik Faktorial

## Penjelasan

Definisikan fungsi untuk menghitung faktorial yang dimodifikasi terlebih dahulu secara rekursif dengan formulasi sebagai berikut:

```
FUNCTION f(x):
 IF x == 0:
  RETURN 1
 IF x IS GENAP:
  RETURN x/2 * f(x - 1)
 ELSE:
  // x otomatis bernilai ganjil
  RETURN x * f(x - 1)
```

Penentuan ganjil/genap dapat menggunakan modulo (jika x % 2 bernilai 0, maka dapat disimpulkan bahwa x habis dibagi 2 sehingga x genap. Lalu jika bernilai 1, maka sebaliknya yaitu ganjil karena tidak habis jika dibagi dengan 2)

## Contoh Solusi

```c
#include <stdio.h>

/* formulasi dari f(x) */
int f(int x) {
    /* base case: 0!? = 0! = 1 */
    if (x == 0) {
        return 1;
    }

    /* jika x genap */
    if (x % 2 == 0) {
        return (x / 2) * f(x - 1);
    }
    /* jika x ganjil */
    return x * f(x - 1);
}

int main() {
    int N;

    scanf("%d", &N);
    printf("%d\n", f(N));

    return 0;
}
```

[Matriks Sempurna >>](4-MatriksSempurna.md)