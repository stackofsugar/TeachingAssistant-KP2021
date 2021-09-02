[<< Materi Sebelumnya (Operasi Assignment dan Aritmatika) <<](3-OperasiAssignmentDanAritmatika.md)
# 2.4 - Pemilihan dan Perulangan Sederhana

Salah satu hal yang paling fundamental dalam pemrograman adalah adanya operasi pemilihan dan perulangan.

**Pemilihan** (atau pengambilan keputusan/decision making) adalah tindakan yang akan dilakukan oleh program apabila dihadapkan pada beberapa pilihan atau kondisi yang akan memproduksi instruksi yang berbeda.

Kemudian **perulangan** adalah kemampuan program untuk **melakukan sekumpulan instruksi yang sama berulang kali** selama **kondisi tertentu memenuhi**. Apabila kondisi perulangan tersebut **selalu memenuhi**, maka yang dikhawatirkan adalah terjadinya **infinite loop** atau program akan berjalan selamanya sehingga berpotensi crash/hang. Oleh karena itu, perhatikan betul dalam menggunakan operasi perulangan.

Operasi pemilihan yang akan digunakan di sini adalah **if - else**, sedangkan operasi perulangan yang digunakan adalah **while**.

## Pemilihan: if - else

Format penggunannya yaitu:
```c
if (/* kondisi */) {
    /* perintah... */
}
/* opsional: */
else if (/* kondisi lain */) {
    /* perintah... */
}
else if (/* kondisi lainnya lagi) {
    /* perintah... */
}
/* else if ... */
else {
    /* perintah... */
}
```

Contoh penggunaan if-else dalam program C adalah sebagai berikut:

Potongan kode berikut menampilkan "Bagus!" di layar ketika `nilaiSaya` **memiliki value 100**
```c
if (nilaiSaya == 100) {
    printf("Bagus!\n");
}
```

Potongan kode berikut menampilkan "Bagus!" di layar ketika `nilaiSaya` memiliki value **lebih dari atau sama dengan 85**, atau "Coba lagi!" jika tidak
```c
if (nilaiSaya >= 85) {
    printf("Bagus!\n");
} else {
    printf("Coba lagi\n");
}
```

Potongan kode berikut menampilkan "Bagus!" di layar ketika `nilaiSaya` memiliki value **lebih dari atau sama dengan 85**, "Cukup" ketika `nilaiSaya` **kurang dari 85** tetapi **lebih besar dari atau sama dengan 50**, "Coba lagi" jika tidak memenuhi semuanya
```c
if (nilaiSaya >= 85) {
    printf("Bagus!\n");
} else if ((nilaiSaya < 85) && (nilaiSaya >= 50)) {
    printf("Cukup\n");
} else {
    printf("Coba lagi\n");
}
```

Potongan kode berikut menampilkan "Lulus" di layar ketika `nilaiSaya` memiliki value **lebih dari atau sama dengan 50** dan "Tidak lulus" apabila memiliki value **kurang dari 50**
```c
if (nilaiSaya >= 50) {
    printf("Lulus\n");
} else if (nilaiSaya < 50) {
    printf("Tidak lulus\n");
}
```

### Operator Pembanding

|Operator|Keterangan|Penjelasan|
|--|--|--|
|A == B|sama dengan|cek jika A sama dengan B|
|A != B|tidak sama dengan|cek jika A tidak sama dengan B|
|A > B|lebih besar dari|cek jika A lebih besar dari B|
|A >= B|lebih besar dari atau sama dengan|cek jika A lebih besar dari atau sama dengan B|
|A < B|kurang dari|cek jika A kurang dari B|
|A <= B|kurang dari atau sama dengan|cek jika A kurang dari atau sama dengan B|

### Konjungsi

|Operator|Keterangan|Penjelasan|
|--|--|--|
|!A|tidak (NOT)|dijalankan apabila kondisi A tidak bernilai benar|
|A && B|dan (AND)|dijalankan apabila kondisi A dan B semuanya benar|
|A \|\| B|atau (OR)|dijalankan apabila kondisi A bernilai benar atau B bernilai benar (salah satu dari A dan B bernilai benar)|

### Tips

- Selalu gunakan tanda kurung ( dan ) apabila diperlukan untuk mempertegas urutan evaluasi. Jika tidak diberi tanda kurung, program akan mengevaluasi operasi NOT atau `!` terlebih dahulu, kemudian operasi AND atau `&&`, kemudian yang terakhir operasi OR atau `||`.

### Source Code

<details>
<summary>Contoh source code (full)</summary>

```c
#include <stdio.h>
int main() {
    int nilaiSaya;
    
    printf("Masukkan nilai anda: ");
    scanf("%d", &nilaiSaya);

    if (nilaiSaya >= 85) {
        printf("Bagus!\n");
    } else if ((nilaiSaya < 85) && (nilaiSaya >= 50)) {
        printf("Cukup\n");
    } else {
        printf("Coba lagi\n");
    }

    return 0;
}

/*
Output:

Masukkan nilai anda: 80
Cukup
*/
```
</details>

## Perulangan: while

Format penggunaannya yaitu:
```c
while (/* kondisi */) {
    /* perintah... */
}
```

Contoh penggunaan while dalam program C adalah sebagai berikut:

Potongan kode berikut menampilkan "Quack!" sebanyak 10 kali di layar console
```c
int i = 1;
while (i <= 10) {
    printf("Quack!\n");
    i++;
}
```

Analisa kode di atas:

1. Variabel `i` dideklarasikan kemudian diisi dengan nilai 1
2. Selagi `i` bernilai kurang dari atau sama dengan 10, maka jalankan perintah `printf("Quack!\n")` kemudian `i++`. Dalam tahap ini, sembari mengulang operasi, program menampilakn "Quack!" ke console kemudian nilai dari variabel `i` di-*increment* (ditambah dengan 1) kemudian kedua perintah tersebut diulang terus menerus sampai tidak memenuhi kondisi `i <= 10` (variabel `i` bernilai 11 dan 11 <= 10 tentu tidak benar) sehingga program dapat keluar dari perulangan.

**Q:** Bagaimana bisa keluar dari perulangan?

**A:** Karena saat `i` mencapai nilai 10, maka akan di-*increment* supaya nilainya menjadi 11 dan dengan demikian, ulangan berikutnya sudah tidak dijalankan lagi karena kondisinya sudah bernilai salah (`i <= 10` untuk nilai `i = 11`).

Potongan kode berikut menampilkan pola 2 4 6 8 ... 100 di layar console
```c
int i = 2;
while (i < 102) {
    printf("%d ", i);
    i = i + 2;
}
```

Analisa kode di atas:

1. Variabel `i` dideklarasikan kemudian diisi dengan nilai awal pola yaitu 2
2. Selagi `i` bernilai kurang dari 102, maka jalankan perintah `printf("%d ", i)` kemudian `i = i + 2`. Dalam tahap ini, sembari mengulang operasi, nilai dari variabel `i` ditampilkan di layar kemudian ditambah dengan 2 dan kedua perintah tersebut diulang terus menerus sampai keluar dari perulangan.

**Q:** Bagaimana bisa keluar dari perulangan?

**A:** Ada yang bisa menjelaskan?

### Source code

<details>
<summary>Contoh source code (full)</summary>

```c
#include <stdio.h>
int main() {
    int i, count;
    
    printf("Masukkan jumlah quack: ");
    scanf("%d", &count);
    
    i = 1;
    while (i <= count) {
        printf("Quack! ");
        i++;
    }
    printf("\n");

    return 0;
}

/*
Output:

Masukkan jumlah quack: 3
Quack! Quack! Quack!
*/
```
</details>

Bab 1 selesai. [Kembali ke silabus](../silabus.md)
