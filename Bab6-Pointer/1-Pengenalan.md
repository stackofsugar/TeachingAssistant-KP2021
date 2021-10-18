[<< Silabus](../silabus.md)

# 6.1 - Pengenalan Pointer

Apa itu pointer? **Pointer** merupakan sebuah **modifikasi** pada suatu tipe data tertentu sehingga nilainya berupa **alamat memori** yang merujuk pada suatu **variabel/data**.

Apa pentingnya belajar pointer? Pointer memungkinkan kita untuk **mengganti** nilai dari suatu **variabel** yang **tidak berada pada scope yang sama** (jika kalian belum paham apa itu scope, lihat [referensi ini](../Bab4-CFunction/3-Scope.md)). Sebagai contoh, perhatikan kode berikut:

```c
#include <stdio.h>

void kurangi_health(int jumlah);

int main() {
    int health = 100;

    printf("Health awal: %d\n", health);

    /* Asumsikan anda ingin mengurangi nilai dari `health` sebesar 20 */
    /* Akan tetapi anda tidak ingin mengurangkannya langsung di sini, melainkan melalui suatu function */
    kurangi_health(20);

    printf("Health akhir: %d\n", health);

    return 0;
}

void kurangi_health(int jumlah) {
    /* Namun terdapat suatu masalah di sini, yaitu scopenya berbeda dengan main() */
    /* Sehingga pada area ini, `health` tidak terdefinisi dan kode di bawah akan memproduksi error */

    health = health - jumlah; /* ERROR: compiler tidak dapat menemukan variabel `health` */
}
```

Oke jadi kode di atas merupakan contoh permasalahan yang dapat diselesaikan menggunakan teknik atau konsep **pointer** sebagai motivasi anda dalam belajar pointer supaya mengetahui pentingnya pointer dalam bahasa C. Solusi dari permasalahan tersebut akan ada pada topik berikutnya, yaitu **Pass By Reference**.

## Deklarasi Pointer

Pointer dapat dideklarasikan dengan format sebagai berikut:
```
<Tipe Data> *<Nama Variabel>;
```

Sebagai contoh:
```c
int *health_ptr;
```
Kode di atas mendeklarasikan variabel `health_ptr` yang bertipe **pointer to int(eger) value**. Sehingga data yang ada di dalam pointer tersebut memiliki tipe data **int**.

Penulisan di bawah juga memiliki arti yang sama. Sesuaikan saja dengan style penulisan masing-masing individu.
```c
int* health_ptr;
```

Jika ingin mendeklarasikan banyak pointer sekaligus di satu baris untuk mempersingkat penulisan, perhatikan contoh berikut:
```c
int *health_ptr, *ammo_ptr;
```
Kode di atas mendeklarasikan variabel `health_ptr` dan `ammo_ptr` yang keduanya bertipe **pointer to int(eger) value**

**TETAPI INGAT!!**

Perhatikan kode di bawah
```c
int* health_ptr, ammo_ptr;
```
Kode tersebut **tidak** menganggap `ammo_ptr` sebagai pointer sehingga yang dianggap pointer hanyalah `health_ptr` saja. Dengan demikian, pemberian tanda asterisk (*) harus diperhatikan apabila ingin mendeklarasikan banyak pointer sekaligus.

## Inisialisasi Pointer

Setelah pointer dideklarasikan, tidak mungkin pointer tersebut langsung mengarah ke variabel tertentu. Oleh karena itu, harus di-inisialisasikan terlebih dahulu. Sebagai contoh:
```c
int health = 100;
int *health_ptr;

/* ... */

/* Buat `health_ptr` merujuk ke variabel `health` */
health_ptr = &health;
```
Kode di atas membuat pointer `health_ptr` supaya mengarah ke variabel `health` dengan operasi _referencing_ (tanda &). Dengan demikian, variabel `health` juga dapat diakses melalui pointer `health_ptr`.


## Membaca (Read) Data dari Pointer

Nilai variabel yang ada dalam pointer dapat dibaca menggunakan operasi _dereferencing_ (tanda * pada prefiks suatu variabel bertipe pointer yang telah dideklarasikan). Sebagai contoh:
```c
int health = 100;
int *health_ptr = &health;

/* ... */

/* Membaca nilai dari variabel yang dirujuk oleh pointer `health_ptr` */
/* Menggunakan operasi dereferencing (*) */
printf("Health sekarang: %d\n", *health_ptr);

health = 50; /* Ganti nilai variabel `health` */

/* Nilai hasil dereferencing selalu menyesuaikan nilai dari variabel yang dirujuknya */
/* Sehingga perubahan apapun pada variabel yang dirujuk, juga mempengaruhi hasil dereferencingnya */
printf("Health sekarang: %d\n", *health_ptr);

/*
Output:

Health sekarang: 100
Health sekarang: 50
*/
```

## Menulis (Write) Data ke Pointer

Nilai dari variabel yang ada dalam pointer dapat ditulis (write) atau dimanipulasi menggunakan operasi _dereferencing_ juga, sama halnya membaca data dari pointer. Sebagai contoh:
```c
int health = 100;
int *health_ptr = &health;

/* ... */

/* Tampilkan nilai awal sebelum dimanipulasi */
printf("Health sekarang: %d\n", health);

/* Menulis/memanipulasi nilai variabel yang dirujuk oleh pointer `health_ptr` */
/* Menggunakan operasi dereferencing (*) */
*health_ptr = 75;

/* Print variabel `health`, nilainya sudah berubah */
/* Karena telah dimanipulasi melalui pointer `health_ptr` */
printf("Health sekarang: %d\n", health);

/*
Output:

Health sekarang: 100
Health sekarang: 75
*/
```

## NULL Pointer

Pointer dapat diberikan nilai khusus yaitu **NULL**. Hal ini berguna apabila anda tidak ingin meng-insialisasi pointer tersebut, melainkan memberinya dengan nilai NULL dan beberapa saat kemudian, program anda mengecek apakah pointer masih kosong (NULL) atau sudah merujuk ke suatu variabel. Jika compiler tidak bisa menemukan kata kunci NULL, pastikan untuk meng-include header **stddef.h** terlebih dahulu. Sebagai contoh:
```c
#include <stddef.h> /* Supaya NULL terdefinisi dengan jelas */

/* ... */

int health = 100;
int *health_ptr;
int choice;

printf("Masukkan 1 untuk bertarung, 0 untuk keluar : ");
scanf("%d", &choice);

if (choice == 1) {
    /* Isi pointer `health_ptr` dengan referensi pada variabel `health` */
    health_ptr = &health;
} else {
    /* Atur `health_ptr` menjadi NULL pointer */
    health_ptr = NULL;
}

if (health_ptr != NULL) {
    /* Area ini dijalankan jika `health_ptr` sudah tidak NULL */
    /* Yang mana artinya `health_ptr` sudah merujuk ke variabel tertentu */

    printf("Anda memilih untuk bertarung\n");

    *health_ptr = 85;
} else {
    /* Area ini dijalankan jika `health_ptr` bernilai NULL */
    /* Yang mana artinya `health_ptr` tidak merujuk ke variabel apapun */

    printf("Anda memilih untuk keluar dari permainan\n");
}

printf("Health akhir anda : %d\n", health);

/*
Output #1:

Masukkan 1 untuk bertarung, 0 untuk keluar : 1
Anda memilih untuk bertarung
Health akhir anda : 85

Output #2:
Masukkan 1 untuk bertarung, 0 untuk keluar : 0
Anda memilih untuk keluar dari permainan
Health akhir anda : 100
*/
```

## Constant Pointer

Akses menuju variabel melalui pointer dapat dibatasi menjadi hanya membaca saja (read-only) dengan menerapkan kata kunci **const**. Sebagai contoh:
```c
int health = 100;
const int *health_ptr; /* Read-only pointer */

/* ... */

health_ptr = &health; /* Atur supaya mengarah ke variabel `health` */

/* Membaca (read) pointer `health_ptr` */
printf("Health sekarang: %d\n", *health_ptr);

/* Menulis (write) pointer `health_ptr` */
*health_ptr = 50; /* ERROR: Pointer `health_ptr` hanya read-only, tidak bisa write */

/* Membaca (read) lagi pointer `health_ptr` */
printf("Health sekarang: %d\n", *health_ptr);
```

[Pass By Reference >>](2-PassByRef.md)
