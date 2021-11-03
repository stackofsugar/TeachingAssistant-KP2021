[<< Silabus](../silabus.md)

# 10.1 - Array dan Linked List

Koleksi (kumpulan obyek atau elemen) dalam program dapat disimpan menggunakan struktur data **array** (yang biasa kita pakai sebelumnya) dan **linked list**. Kita akan membahas tentang perbandingan array dan linked list pada materi ini.

## Array

Elemen-elemen yang berada di dalam koleksi disimpan secara berjejeran dalam memori (dengan kata lain, lokasi suatu elemen pada RAM/memori berjejeran langsung dengan lokasi elemen sebelumnya dan berikutnya).

### Definisi

Deklarasi array seperti biasa
```c
int price_list[100];
int item_count; /* untuk kasus dynamic size, tambahkan variable yang menunjukkan jumlah item */
```

### Mengakses Elemen

Digunakan untuk mengakses elemen tertentu. Bisa langsung menggunakan indeks, contoh:
```c
printf("M4A1 price: %d\n", price_list[3]); /* akses indeks ke-3 */
```

### Memodifikasi Elemen

Digunakan untuk memodifikasi nilai elemen tertentu. Bisa langsung menggunakan indeks, contoh:
```c
price_list[3] = 3100; /* akses indeks ke-3 */
```

### Iterasi Seluruh Elemen Array

Dapat menggunakan **for** dengan control variable berupa indeks yang sedang dikunjungi, misal:
```c
int i; /* control variable: indeks yang sedang dikunjungi */

/* ... */

/* Penjelajahan array `price_list` */
for (i = 0; i < item_count; i++) {
    printf("Harga barang ke-%d : %d\n", (i + 1), price_list[i]);
}
```

## Linked List

Elemen-elemen yang berada di dalam koleksi disimpan secara terpisah dalam memori (dengan kata lain, lokasi suatu elemen pada RAM/memori tidak berjejeran langsung dengan lokasi elemen sebelumnya dan berikutnya). Untuk menentukan suatu lokasi elemen pada linked list, diperlukan informasi pada salah satu obyek/elemennya yang menunjukkan pointer yang mengarah pada lokasi elemen berikutnya/sebelumnya.

Konsep linked list tidak terpisah dari pointer (termasuk dynamic memory allocation). Apabila anda belum memahami pointer, diharapkan untuk membaca lagi supaya tidak kesulitan dalam memahami materi ini.

Dalam materi ini, kita akan membahas untuk kasus **Doubly Linked List** (tiap nodenya terdapat pointer ke elemen sebelum dan sesudahnya) karena bisa sangat serbaguna untuk berbagai kasus penerapan (misal **stack** dan **queue** yang akan dibahas pada topik berikutnya).

### Definisi

Definisikan tipe elemen koleksinya sebagai **node** berupa *self-referential structure* yang berisi data informasi tentang elemennya terlebih dahulu, misal untuk kasus koleksi dari `struct Weapon`:
```c
struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

/* Merepresentasikan tiap elemen dalam linked list dalam bentuk node */
struct WeaponNode {
    /* data elemen yang tersimpan dalam node */
    struct Weapon data;

    /* pointer menuju elemen/node sebelumnya dalam koleksi */
    /* beri nilai NULL apabila sudah tidak ada elemen lagi (dlm kata lain, elemen pertama) */
    struct WeaponNode *prev;

    /* pointer menuju elemen/node berikutnya dalam koleksi */
    /* beri nilai NULL apabila sudah tidak ada elemen lagi (dlm kata lain, elemen terakhir) */
    struct WeaponNode *next;
};

/* Representasi linked list yang menyatakan koleksi dari `struct Weapon` */
struct WeaponList {
    /* pointer menuju elemen pertama dalam linked list */
    /* beri nilai NULL apabila linked list masih kosongan */
    struct WeaponNode *first;

    /* pointer menuju elemen terakhir dalam linked list */
    /* beri nilai NULL apabila linked list masih kosongan */
    struct WeaponNode *last;
};
```

Kemudian untuk variabel bertipe koleksi `struct Weapon` menggunakan linked list, perhatikan contoh berikut:
```c
struct WeaponList weapons;

/* keadaan awal : linked list masih kosongan */
weapons.first = NULL;
weapons.last = NULL;
```

### Menambahkan Elemen

Dalam menambahkan elemen ke dalam linked list, untuk kasus `struct Weapon`, gunakan code berikut:
```c
/* akan menambah elemen setelah `after` */
/* `after` dapat diperoleh dari penjelajahan/iterasi seluruh node dalam linked list */
/* jika after bernilai `NULL`, maka tambahkan ke awal list */
void insertWeapon(struct WeaponList *list, struct WeaponNode *after, const struct Weapon *data) {
    if (after != NULL) {
        /* tambahkan node baru setelah `after` */

        struct WeaponNode *newNode, *oldNext;

        /* ciptakan elemen baru */
        newNode = (struct WeaponNode *)malloc(sizeof(struct WeaponNode));
        newNode->data = *data;
        newNode->prev = after; /* selaraskan rantai linked list */
        newNode->next = after->next; /* selaraskan rantai linked list */

        /* selaraskan rantai linked list */
        after->next = newNode;

        /* cek untuk kasus penambahan di akhir linked list */
        /* sesuai definisi, `next` bernilai NULL apabila merupakan elemen terakhir linked list */
        if (newNode->next == NULL) {
            /* selaraskan juga pointer elemen terakhir */
            list->last = newNode;
        } else {
            /* jika penambahan terjadi di tengah, selaraskan rantai linked listnya */
            newNode->next->prev = newNode;
        }
    } else {
        /* tambahkan node baru pada awal linked list */

        struct WeaponNode *newNode;

        /* ciptakan elemen baru */
        newNode = (struct WeaponNode *)malloc(sizeof(struct WeaponNode));
        newNode->data = *data;
        newNode->prev = NULL; /* sesuai definisi, beri NULL apabila merupakan elemen pertama */
        newNode->next = list->first; /* selaraskan rantai linked list */

        /* atur pointer elemen pertama ke node yang baru saja ditambahkan */
        list->first = newNode;

        /* cek untuk kasus transisi dari linked list yang tadinya kosong menjadi terisi 1 elemen */
        if (list->last == NULL) {
            /* atur pointer elemen terakhir ke node yang baru saja ditambahkan */
            list->last = newNode;
        } else {
            /* jika sebelumnya linked list masih terisi, selaraskan rantai linked list */
            newNode->next->prev = newNode;
        }
    }
}
```

### Menghapus Elemen

Dalam menghapus elemen dari linked list, untuk kasus `struct Weapon`, gunakan code berikut:
```c
/* akan menghapus elemen `node` pada linked list */
/* `node` dapat diperoleh dari penjelajahan/iterasi seluruh node dalam linked list */
void deleteWeapon(struct WeaponList *list, struct WeaponNode *node) {
    /* pastikan linked list tidak dalam keadaan kosong */
    if (list->first != NULL) {
        /* cek lokasi penghapusan terlebih dahulu */
        /* apakah berada di awal linked list, di akhir linked list, atau di tengah linked list */
        if (node == list->first) {
            /* kasus menghapus elemen di awal linked list */

            struct WeaponNode *oldNext;

            /* catat elemen setelah elemen pertama terlebih dahulu */
            oldNext = list->first->next;

            /* hapus elemen pertama dari memori */
            free(list->first);

            /* selaraskan pointer elemen pertama */
            list->first = oldNext;

            if (list->first == NULL) {
                /* jika keadaan akhir linked list menjadi kosong */
                /* selaraskan juga pointer elemen terakhir linked list */
                list->last = NULL;
            } else {
                /* jika keadaan akhir linked list masih terisi */
                /* selaraskan pointer elemen pertama */
                list->first->prev = NULL;
            }
        } else if (node == list->last) {
            /* kasus menghapus elemen di akhir linked list */

            struct WeaponNode *oldPrev;

            /* catat elemen sebelum elemen terakhir terlebih dahulu */
            oldPrev = list->last->prev;

            /* hapus elemen terakhir dari memori */
            free(list->last);

            /* selaraskan pointer elemen terakhir */
            list->last = oldPrev;

            if (list->last == NULL) {
                /* jika keadaan akhir linked list menjadi kosong */
                /* selaraskan juga pointer elemen pertama linked list */
                list->first = NULL;
            } else {
                /* jika keadaan akhir linked list masih terisi */
                /* selaraskan pointer elemen terakhir */
                list->last->next = NULL;
            }
        } else {
            /* kasus menghapus elemen di tengah linked list */

            struct WeaponNode *oldPrev, *oldNext;

            /* catat elemen sebelum dan sesudah `node` terlebih dahulu */
            oldPrev = node->prev;
            oldNext = node->next;

            /* hapus elemen `node` dari memori */
            free(node);

            /* selaraskan rantai linked list */
            oldPrev->next = oldNext;
            oldNext->prev = oldPrev;
        }
    }
}
```

### Iterasi Seluruh Node Linked List

Untuk kasus `struct Weapon`, gunakan code berikut untuk melakukan iterasi
```c
struct WeaponList list;
struct WeaponNode *iterator;

/* ... */

for (iterator = list.first; iterator != NULL; iterator = iterator->next) {
    /* lakukan sesuatu dengan `iterator` */
    print_weapon(&iterator->data);
}
```

Atau menggunakan while loop (kasus penghapusan elemen tertentu):
```c
struct WeaponList list;
struct WeaponNode *iterator;

/* hapus semua senjata yang memiliki harga di atas 3000 */
iterator = list.first;
while (iterator != NULL) {
    struct WeaponList *next;

    next = iterator->next;
    if (iterator->data.price > 3000) {
        deleteWeapon(iterator);
    }
    iterator = next;
    /* `iterator = iterator->next` akan error apabila `iterator` sudah terhapus dengan `deleteWeapon` */
}
```

### Contoh Penggunaan

```c
void printWeapons(struct WeaponList *list) {
    if (list->first != NULL) {
        struct WeaponNode *iterator;

        for (iterator = list->first; iterator != NULL; iterator = iterator->next) {
            printf("Weapon: %s ($: %d, %%: %d, n: %d)\n", iterator->data.name, iterator->data.price, iterator->data.damage, iterator->data.rounds);
        }
    } else {
        printf("(list is empty)\n");
    }
    printf("\n");
}

int main() {
    struct WeaponNode *iterator;
    struct WeaponList list;
    struct Weapon wpn;

    list.first = NULL;
    list.last = NULL;

    strcpy(wpn.name, "Desert Eagle");
    wpn.price = 750;
    wpn.damage = 35;
    wpn.rounds = 7;
    insertWeapon(&list, list.last, &wpn);

    strcpy(wpn.name, "M4A1");
    wpn.price = 3100;
    wpn.damage = 20;
    wpn.rounds = 30;
    insertWeapon(&list, list.last, &wpn);

    strcpy(wpn.name, "H&K MP5");
    wpn.price = 1500;
    wpn.damage = 15;
    wpn.rounds = 30;
    insertWeapon(&list, list.last, &wpn);

    strcpy(wpn.name, "AK-47");
    wpn.price = 2500;
    wpn.damage = 25;
    wpn.rounds = 30;
    insertWeapon(&list, list.last, &wpn);

    printWeapons(&list);

    printf("Menghapus elemen pertama...\n");
    deleteWeapon(&list, list.first);
    printWeapons(&list);

    printf("Menghapus elemen terakhir...\n");
    deleteWeapon(&list, list.last);
    printWeapons(&list);

    printf("Menambahkan AWP...\n");
    strcpy(wpn.name, "AWP Magnum");
    wpn.price = 4750;
    wpn.damage = 100;
    wpn.rounds = 10;
    insertWeapon(&list, list.last, &wpn);
    printWeapons(&list);

    printf("Menghapus senjata yang harganya lebih dari $3000...\n");
    iterator = list.first;
    while (iterator != NULL) {
        struct WeaponNode *next;

        next = iterator->next;
        if (iterator->data.price > 3000) {
            deleteWeapon(&list, iterator);
        }
        iterator = next;
    }
    printWeapons(&list);

    printf("Menghapus elemen pertama...\n");
    deleteWeapon(&list, list.first);
    printWeapons(&list);

    return 0;
}

/*
Output:

Weapon: Desert Eagle ($: 750, %: 35, n: 7)
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)
Weapon: AK-47 ($: 2500, %: 25, n: 30)

Menghapus elemen pertama...
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)
Weapon: AK-47 ($: 2500, %: 25, n: 30)

Menghapus elemen terakhir...
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)

Menambahkan AWP...
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)
Weapon: AWP Magnum ($: 4750, %: 100, n: 10)

Menghapus senjata yang harganya lebih dari $3000...
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)

Menghapus elemen pertama...
(list is empty)

*/
```

## Kelebihan dan Kekurangan Masing-Masing

Array memiliki kelebihan yaitu dapat mengakses suatu elemen posisi tertentu dengan cepat dan mudah hanya berdasarkan indeks angka. Namun kekurangannya adalah proses penambahan/penghapusan elemen sulit dilakukan secara efektif. Cocok digunakan apabila ukuran koleksi tidak berubah-ubah dan dapat diidentifikasi dengan suatu indeks angka (dalam kata lain, pengaksesan suatu elemen berdasarkan indeks juga dipertimbangkan)

Kemudian linked list memiliki kelebihan yaitu proses penambahan/penghapusan elemen mudah dilakukan secara efektif. Namun kekurangannya adalah untuk mengakses suatu elemen/node tidak bisa langsung berdasarkan indeks namun harus melalui proses iterasi terlebih dahulu untuk menemukan elemen/node yang cocok. Cocok digunakan apabila ukuran koleksi berubah-ubah dan tidak perlu mengidentifikasi elemen berdasarkan indeks (dalam kata lain, hanya operasi iterasi seluruh elemen saja yang dipertimbangkan).

[Stack dan Queue >>](2-StackQueue.md)
