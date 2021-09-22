[<< Kembali Ke Silabus](../silabus.md)

# 5.1 - Pengenalan Array

Apa itu array? **Array** (atau larik) adalah sebuah struktur data berukuran tertentu yang memiliki kegunaan untuk menampung kumpulan data (elemen) dengan tipe yang sama (misalnya kumpulan dari nilai integer, kumpulan dari nilai float, kumpulan dari string, dll). Tentunya jumlah data yang disimpan harus sesuai dengan ukuran kapasitasnya.

## Deklarasi

Array dapat dideklarasikan dengan format:
```c
/*TipeData*/ /*NamaVariabel*/[/*Kapasitas*/];
```

Sebagai contoh:
```c
int price_list[5];
```
Kode di atas membuat variabel bernama `price_list` bertipe array of (int)eger (kumpulan bilangan bulat) yang memiliki kapasitas atau ukuran sebesar 5 elemen (sehingga maksimal menampung 5 data bilangan bulat)

## Inisialisasi

Setelah variabel berjenis array dideklarasikan, untuk menginisialisasi (mengisi dengan data awal) variabel tersebut dapat dilakukan dengan 2 cara:

### Secara Langsung

Inisialisasi secara langsung (menggunakan `{Elemen1, Elemen2, Elemen3, ...}`) bersamaan dengan deklarasi, contoh:
```c
int price_list[5] = {2500, 3100, 1500, 750, 4750};
```
Kode di atas mengisi array `price_list` dengan nilai: 2500, 3100, 1500, 750, dan 4750 secara urut dari elemen pertama sampai elemen terakhir

Angka yang menunjukkan kapasitas dapat dihilangkan, sehingga menjadi:
```c
/* Kapasitas array: 5 (otomatis) */
int price_list[] = {2500, 3100, 1500, 750, 4750};
```

### Satu-Persatu

Inisialisasi satu-persatu untuk tiap elemen (terpisah dengan deklarasi), contoh:
```c
int price_list[5];

/* ... */

/* Isi elemen pertama sampai terakhir */
price_list[0] = 2500; /* urutan/indeks/posisi elemen selalu dimulai dari nol */
price_list[1] = 3100;
price_list[2] = 1500;
price_list[3] = 750;
price_list[4] = 4750;
```

## Mengakses dan Mengubah Nilai Elemen

### Mengakses elemen

Untuk mendapatkan nilai dari elemen suatu array, perhatikan contoh berikut:
```c
int price_list[5] = {2500, 3100, 1500, 750, 4750};
int m4a1_price;

/* ... */

/* mendapatkan nilai elemen ke-2 dari array `price_list` */
/* kemudian memasukkannya ke variabel `m4a1_price` */
m4a1_price = price_list[1];

/* dan juga menampilkannya ke console: */
printf("m4a1_price : %d\n", m4a1_price);
/* atau bisa juga: */
printf("price_list[1] : %d\n", price_list[1]);

/*
Output:

m4a1_price : 3100
price_list[1] : 3100
*/
```

### Mengubah elemen

Untuk mengubah nilai elemen suatu array, perhatikan contoh berikut:
```c
int price_list[5] = {2500, 3100, 1500, 750, 4750};

/* ... */

/* mengubah nilai elemen ke-3 dari array `price_list` menjadi 2000 */
price_list[2] = 2000;

/* Isi array `price_list` sekarang: {2500, 3100, 2000, 750, 4750} */
```

### Catatan

Selalu perhatikan kapasitas dari array jika ingin mengakses atau mengubah nilai elemen suatu array. Pastikan posisi elemennya tidak melebihi kapasitas yang dapat ditampung oleh array. Jika mencoba untuk mengakses posisi di luar batas kapasitas, maka yang terjadi adalah program akan berpotensi crash dan memproduksi error.

## Variasi Ukuran Array

Dalam pemrograman, seringnya ukuran dari array pasti berubah-ubah seiring dengan jalannya program menyesuaikan dengan penambahan elemen dan penghapusan elemen selama program berjalan.

Namun dalam bahasa C, kapasitas array tidak dapat diubah jika sudah ditetapkan secara fixed (meskipun terdapat cara lain untuk mengubah kapasitas array yang menggunakan konsep memory management, namun tidak dibahas dalam topik ini). Sebagai contoh, `int price_list[5]` sudah pasti memiliki kapasitas maks 5 elemen dan tidak dapat diubah-ubah (misal menjadi 10 elemen, 3 elemen, atau yang lain).

Untuk menangani variasi ukuran array dalam pemrograman C, perlu adanya variabel tambahan yang menyatakan ukuran array pada saat itu. Dengan demikian, kodenya dapat dimodifikasi menjadi:
```c
int price_list[100]; /* maksimal menampung 100 elemen */
int price_list_count = 0; /* jumlah elemen dari `price_list`, inisialisasikan dengan 0 (array belum terisi sama sekali) */
int i;

/* ... */

printf("Masukkan jumlah item: ");
scanf("%d", &price_list_count);
for (i = 0; i < price_list_count; i++) {
    printf("Masukkan harga item ke-%d: ", (i + 1));
    scanf("%d", &price_list[i]);
}
printf("=== LIST HARGA (Jml: %d) ===\n", price_list_count);
for (i = 0; i < price_list_count; i++) {
    printf("Harga item ke-%d: %d\n", (i + 1), price_list[i]);
}

/*
Output:

Masukkan jumlah item: 3
Masukkan harga item ke-1: 1500
Masukkan harga item ke-2: 2500
Masukkan harga item ke-3: 3100
=== LIST HARGA (Jml: 3) ===
Harga item ke-1: 1500
Harga item ke-2: 2500
Harga item ke-3: 3100
*/
```
Dalam program di atas, jumlah item bergantung pada input saat program dijalankan dan bukan ditetapkan pada source codenya. Dengan demikian, ukuran input yang dimasukkan bisa bervariasi asalkan tidak melebihi kapasitas maksimumnya (100 elemen).

Ukuran array juga dapat di-*increment* ketika terjadi penambahan elemen:
```c
int price_list[100]; /* maksimal menampung 100 elemen */
int price_list_count = 0; /* jumlah elemen dari `price_list`, inisialisasikan dengan 0 (array belum terisi sama sekali) */
int i;

/* ... */

while (1) {
    int operation;

    printf("Masukkan 1 untuk menambah harga, atau 0 untuk berhenti : ");
    scanf("%d", &operation);

    if (operation == 1) {
        printf("Masukkan harga item ke-%d : ", (price_list_count + 1));
        scanf("%d", &price_list[price_list_count]);

        price_list_count++; /* Perbarui jumlah item */
    } else if (operation == 0) {
        break;
    }
}
printf("=== LIST HARGA (Jml: %d) ===\n", price_list_count);
for (i = 0; i < price_list_count; i++) {
    printf("Harga item ke-%d: %d\n", (i + 1), price_list[i]);
}

/*
Output:

Masukkan 1 untuk menambah harga, atau 0 untuk berhenti : 1
Masukkan harga item ke-1 : 1500
Masukkan 1 untuk menambah harga, atau 0 untuk berhenti : 1
Masukkan harga item ke-2 : 2500
Masukkan 1 untuk menambah harga, atau 0 untuk berhenti : 1
Masukkan harga item ke-3 : 3100
Masukkan 1 untuk menambah harga, atau 0 untuk berhenti : 0
=== LIST HARGA (Jml: 3) ===
Harga item ke-1: 1500
Harga item ke-2: 2500
Harga item ke-3: 3100
*/
```

### INGAT!!!

Coba amati kode di bawah dan cari letak kesalahannya:
```c
int count;
int i;

printf("Masukkan jumlah item: ");
scanf("%d", &count);

int price_list[count];
for (i = 0; i < count; i++) {
    printf("Masukkan harga item ke-%d: ", (i + 1));
    scanf("%d", &price_list[i]);
}
printf("=== LIST HARGA ===\n");
for (i = 0; i < count; i++) {
    printf("- Harga item ke-%d: %d\n", (i + 1), price_list[i]);
}
```

Sekilas kode di atas nampak benar-benar saja dan bisa dijalankan **apabila dicompile dengan MinGW/GCC** (compiler yang dimiliki oleh DevC++, CodeBlocks, dll). Namun kode tersebut **tidak bisa dicompile menggunakan Microsoft Visual C++ Compiler** (compiler yang dimiliki oleh Microsoft Visual Studio). Ternyata setelah ditelusuri, penyebab compiler error pada Visual C++ adalah kesalahan yang terletak pada deklarasi array `int price_list[count]`. Dalam bahasa pemrograman C, praktik seperti itu (mengatur kapasitas array berdasarkan **variabel**) tidak ada dalam spesifikasi atau standar pemrograman bahasa C. Oleh karena itu, **hindari** pendeklarasian array dengan kapasitas diambil dari suatu variabel. Selalu gunakan kapasitas berupa **angka konstan** saat menulis code dimanapun supaya kode yang anda tulis dapat dicompile di berbagai compiler modern. Solusi alternatif untuk ini adalah mendeklarasikan array dengan kapasitas konstan yang cukup besar dan menggunakan variabel baru yang menyatakan ukuran array, seperti yang tertera di kode pada topik yang telah dibahas sebelumnya.

## Contoh Source Code

<details>
<summary>Contoh Source Code (Ukuran Tetap)</summary>

```c
#include <stdio.h>

int main()
{
    char item_list[5][50] = {"AK-47", "M4A1 Carbine", "H&K MP-5", "Desert Eagle", "AWP Magnum"};
    int price_list[5] = {2500, 3100, 1500, 750, 4750};
    int i;

    printf("=== LIST HARGA ===\n");
    for (i = 0; i < 5; i++) {
        printf("- %s : $%d\n", item_list[i], price_list[i]);
    }

    return 0;
}

/*
Output:

=== LIST HARGA ===
- AK-47 : $2500
- M4A1 Carbine : $3100
- H&K MP-5 : $1500
- Desert Eagle : $750
- AWP Magnum : $4750
*/
```
</details>

<details>
<summary>Contoh Source Code (Ukuran Bervariasi)</summary>

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char item_list[100][50]; /* maksimal 100 item yang masing-masing berupa string dengan kapasitas 50 char */
    int price_list[100];
    int item_count = 0;
    int i;

    while (1) {
        int operation;
    
        printf("Masukkan 1 untuk menambah item, atau 0 untuk berhenti : ");
        scanf("%d", &operation);
    
        if (operation == 1) {
            char name[50];
            int price;

            printf("- Nama item ke-%d : ", (item_count + 1));
            scanf("%s", name);

            printf("- Harga item ke-%d : ", (item_count + 1));
            scanf("%d", &price);

            /* Masukkan input ke dalam array */
            strcpy(item_list[item_count], name);
            price_list[item_count] = price;

            item_count++; /* Perbarui jumlah item */
        } else if (operation == 0) {
            break;
        }
    }

    printf("=== LIST HARGA (Jml: %d) ===\n", item_count);
    for (i = 0; i < item_count; i++) {
        printf("- %s: $%d\n", item_list[i], price_list[i]);
    }

    return 0;
}

/*
Output:

Masukkan 1 untuk menambah item, atau 0 untuk berhenti : 1
- Nama item ke-1 : AK47
- Harga item ke-1 : 2500
Masukkan 1 untuk menambah item, atau 0 untuk berhenti : 1
- Nama item ke-2 : M4A1_Carbine
- Harga item ke-2 : 3100
Masukkan 1 untuk menambah item, atau 0 untuk berhenti : 1
- Nama item ke-3 : H&K_MP5
- Harga item ke-3 : 1500
Masukkan 1 untuk menambah item, atau 0 untuk berhenti : 0
=== LIST HARGA (Jml: 3) ===
- AK47: $2500
- M4A1_Carbine: $3100
- H&K_MP5: $1500
*/
```
</details>

[Materi Berikutnya (Array Multidimensi) >>](2-ArrayMultidimensi.md)
