[<< Materi Sebelumnya (Scope)](3-Scope.md)

# 4.4 - Rekursi

Secara sederhana, rekursi adalah suatu perilaku di mana suatu fungsi **memanggil dirinya sendiri**

Coba perhatikan kode di bawah:

```c
#include <stdio.h>

void quack() {
    printf("Quack!\n");
    quack(); /* memanggil dirinya sendiri */
}

int main() {
    quack();
    return 0;
}
```

Bagaimana output dari program di atas menurut prediksi anda?

## Base Case

Supaya tidak terjadi **infinite loop**, maka perlu adanya **base case** untuk menghentikan proses rekursi yang sedang berjalan. Kode di atas dapat dimodifikasi menjadi:

```c
#include <stdio.h>

/* tambahkan parameter `n` */
void quack(int n) {
    /* ini merupakan base case (ketika n == 0, maka rekursi berhenti) */
    if (n == 0) {
        return;
    }

    printf("Quack!\n");
    quack(n - 1); /* nilai n dikurangi terus untuk setiap pemanggilan terhadap dirinya */
}

int main() {
    /* Tampilkan Quack! sebanyak lima kali */
    quack(5);
    return 0;
}

/*
Output:

Quack!
Quack!
Quack!
Quack!
Quack!
*/
```

## Contoh Kasus

Berikut adalah program untuk menghitung nilai dari 1+2+3+...+n secara rekursif

```c
#include <stdio.h>

/* fungsi untuk menghitung 1+2+3+...+n */
int hitung(int n) {
    if (n == 1) {
        return 1;
    }
    return hitung(n - 1) + n;
}

int main() {
    int angka, hasil;

    printf("Masukkan angka (n) : ");
    scanf("%d", &angka);

    /* hasil = 1+2+3+...+angka */
    hasil = hitung(angka);
    printf("Hasil perhitungan : %d\n", hasil);

    return 0;
}

/*
Output:

Masukkan angka (n) : 5
Hasil perhitungan : 15
*/
```

Analisis rekursi di atas untuk `n = 5` yaitu:

1. hitung(5) berarti hitung(4) + 5
2. hitung(4) berarti hitung(3) + 4
3. hitung(3) berarti hitung(2) + 3
4. hitung(2) berarti hitung(1) + 2
5. hitung(1) berarti 1 (rekursi berhenti)
6. maka nilai dari hitung(2) = hitung(1) + 2 = 1 + 2 = 3
7. maka nilai dari hitung(3) = hitung(2) + 3 = 3 + 3 = 6
8. maka nilai dari hitung(4) = hitung(3) + 4 = 6 + 4 = 10
9. maka nilai dari hitung(5) = hitung(4) + 5 = 10 + 5 = 15

Sehingga hasilnya 15 untuk n = 5 dan memenuhi 1+2+3+4+5 = 15

[Menuju Silabus >>](../silabus.md)
